---
inclusion: manual
---
# UI Kit V6 (Prisma) - Formularios (vee-validate + Yup)

Cómo construir formularios validados sobre componentes `cns-` (Shadow DOM) en Vue 3.
Stack: **vee-validate + Yup**, Composition API, `<script setup>`. Si el proyecto migró a
otra librería de validación, actualizar este archivo antes de usarlo.

> **Origen de esta guía**: Los patrones aquí documentados se extrajeron de implementaciones
> reales en producción (cotizadores multi-paso). No provienen del Storybook oficial de Prisma
> sino de la experiencia resolviendo la integración vee-validate + Shadow DOM en proyectos
> del equipo. Validar contra la versión actual del componente si hay discrepancias.

> El reto central: los `cns-` son web components con Shadow DOM. vee-validate no "ve"
> sus inputs internos, así que el puente entre el evento del componente y el estado del
> formulario hay que cablearlo explícitamente.

## Regla de oro: el valor viaja en `event.detail`

Los `cns-` no emiten `input`/`change` nativos del DOM con `target.value` utilizable.
El valor llega en `event.detail`. Por eso se sincroniza manualmente con `useField`.

```vue
<script setup>
import { useField } from 'vee-validate'

const { value: rut, errorMessage: rutError } = useField('rut')

// Puente: del evento del componente al estado de vee-validate
const onRut = (e) => { rut.value = e.detail }
</script>

<template>
  <cns-input
    type="rut"
    label="RUT"
    :value="rut"
    :error="!!rutError"
    :validation="rutError"
    @input="onRut"
  />
</template>
```

## Interceptar eventos del Shadow DOM con `capture: true`

Cuando un evento del componente no burbujea como se espera (o se necesita atraparlo antes
que un handler interno), registrar el listener en fase de captura. Evita perder el primer
cambio o que un wrapper intermedio lo consuma.

```vue
<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue'

const el = ref(null)
const handler = (e) => { /* leer e.detail */ }

onMounted(() => el.value?.addEventListener('input', handler, { capture: true }))
onBeforeUnmount(() => el.value?.removeEventListener('input', handler, { capture: true }))
</script>

<template>
  <cns-input ref="el" type="text" label="..." />
</template>
```

## Timing: `nextTick` al setear valores programáticos

Al hidratar el formulario (precarga, reset, autocompletado) el `cns-` necesita un tick para
re-renderizar su Shadow DOM antes de leer/validar. Setear valor y validar en el mismo tick
produce estados desincronizados.

```js
import { nextTick } from 'vue'

setFieldValue('comuna', comunaPrecargada)
await nextTick()        // dejar que el cns- pinte el nuevo valor
await validateField('comuna')
```

## RUT chileno

No reimplementar la validación: `cns-input type="rut"` ya formatea. Para la regla de dígito
verificador en Yup, usar un validador propio (módulo 11) y delegar el formato al componente.

```js
import * as yup from 'yup'

const rutValido = (rut) => {
  if (!rut) return false
  const limpio = rut.replace(/[.\-]/g, '').toUpperCase()
  const cuerpo = limpio.slice(0, -1)
  const dv = limpio.slice(-1)
  let suma = 0, mul = 2
  for (let i = cuerpo.length - 1; i >= 0; i--) {
    suma += parseInt(cuerpo[i], 10) * mul
    mul = mul === 7 ? 2 : mul + 1
  }
  const res = 11 - (suma % 11)
  const dvCalc = res === 11 ? '0' : res === 10 ? 'K' : String(res)
  return dv === dvCalc
}

const schema = yup.object({
  rut: yup.string().required('Ingresa tu RUT').test('rut', 'RUT inválido', rutValido),
})
```

## Selectores en cascada (región → ciudad → comuna)

Resetear los hijos cuando cambia el padre y poblar de forma asíncrona con watchers. Limpiar
el valor del hijo en cada cambio del padre para no arrastrar selecciones inválidas.

```vue
<script setup>
import { ref, watch } from 'vue'
import { useField } from 'vee-validate'

const { value: region } = useField('region')
const { value: comuna, setValue: setComuna } = useField('comuna')
const comunas = ref([])

watch(region, async (nueva) => {
  setComuna('')                       // limpiar hijo
  comunas.value = []
  if (!nueva) return
  comunas.value = await fetchComunas(nueva)   // poblar async
})
</script>
```

## Esquemas dinámicos: `yup.lazy` + `useFieldArray`

Para listas de tamaño variable (pasajeros, acompañantes, beneficiarios) usar `useFieldArray`
y un esquema que se adapta al número de ítems con `yup.lazy`.

```js
import * as yup from 'yup'

const pasajeroSchema = yup.object({
  nombre: yup.string().required('Nombre requerido'),
  rut: yup.string().required().test('rut', 'RUT inválido', rutValido),
})

const schema = yup.object({
  pasajeros: yup.lazy((arr) =>
    yup.array().of(pasajeroSchema).min(1, 'Agrega al menos un pasajero')
  ),
})
```

```vue
<script setup>
import { useFieldArray } from 'vee-validate'
const { fields, push, remove } = useFieldArray('pasajeros')
</script>

<template>
  <div v-for="(field, idx) in fields" :key="field.key">
    <cns-input :value="field.value.nombre" label="Nombre"
               @input="(e) => field.value.nombre = e.detail" />
    <cns-button label="Quitar" variant="tertiary" @cnsclick="remove(idx)" />
  </div>
  <cns-button label="Agregar pasajero" variant="secondary" @cnsclick="push({ nombre:'', rut:'' })" />
</template>
```

## Checklist de un cotizador multi-paso

- Estado de pasos con `cns-stepper`; marcar `complete: true` al avanzar (ver `prisma-stepper.md`).
- Validar el paso actual antes de permitir avanzar (`validate()` por sección o por campos).
- Errores de campo: pasar `errorMessage` al `:validation`/`:error` del `cns-input`.
- Resumen de errores al enviar: `cns-alert type="section" variant="error"`.
- Botones de navegación con `@cnsclick`; el de envío con `loading` mientras corre la API.
- Al precargar datos: `setValues()` + `await nextTick()` antes de cualquier validación.
