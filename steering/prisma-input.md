---
inclusion: manual
---
# UI Kit V6 (Prisma) - Input

**Versión**: 6.1.0
**Paquete**: `@ui-kit/input-v6`

Input permite ingresar datos de manera sencilla y personalizable.

## Instalación

```bash
npm install @ui-kit/input-v6
```

Registro global en `main.ts`:

```typescript
import { registerInput } from '@ui-kit/input-v6'
registerInput()
```

O desde la librería global:

```typescript
import { CnsInput } from '@ui-kit/components-v6';
CnsInput();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `label` | string | - | Etiqueta que describe el campo |
| `helper` | string | - | Texto de ayuda bajo el input |
| `validation` | string | - | Mensaje de validación o error |
| `placeholder` | string | - | Texto cuando no hay valor ingresado |
| `required` | boolean | - | Campo obligatorio (muestra texto "requerido" en rojo) |
| `disabled` | boolean | - | Deshabilita el componente |
| `readonly` | boolean | - | Solo lectura, sin edición |
| `size` | string | - | Altura en px: `40`, `48`, `56` |
| `state` | string | - | Estado visual del input |
| `prefix` | string | - | Texto/símbolo antes del valor |
| `suffix` | string | - | Texto/símbolo después del valor |
| `iconleft` | string | - | Ícono SVG a la izquierda |
| `iconright` | string | - | Ícono SVG a la derecha |
| `type` | string | - | Tipo de input: `text`, `password`, `number`, `email`, `phone`, `rut`, `miles`, `date`, `time` |
| `value` | string | - | Valor actualmente ingresado (solo para inicializar; no usar para binding reactivo) |
| `showTooltip` | boolean | - | Muestra ícono de tooltip |
| `optional` | boolean | - | Campo opcional (muestra "opcional") |
| `optionalText` | string | - | Texto personalizado para opcional/requerido |
| `maxlength` | number | - | Máximo de caracteres permitidos |
| `minlength` | number | - | Mínimo de caracteres requeridos |
| `max` | any | - | Valor máximo (numéricos o fecha) |
| `min` | any | - | Valor mínimo (numéricos o fecha) |
| `error` | boolean | - | Aplica estilos de error |
| `success` | boolean | - | Aplica estilos de éxito |
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `name` | string | - | Nombre del campo en formularios |

## Lectura de valores (patrón obligatorio)

`cns-input` es un **web component nativo** (`defineCustomElement` + Shadow DOM). Esto tiene implicancias directas en cómo se leen los valores:

### ⚠️ v-model NO funciona

Con `isCustomElement: tag => tag.includes('cns-')` en `vite.config.js`, Vue trata los tags `cns-*` como custom elements del DOM. Esto significa:

- **`v-model` no establece binding bidireccional** — Vue no lo procesa como componente Vue
- **`@input` con `e.detail`** captura el evento nativo `input` del `<input>` interno del Shadow DOM, no el `CustomEvent` del componente. El valor en `e.detail` puede ser `undefined` o un array, no un string
- **`:value` como prop reactiva** puede causar warnings de tipo (`Expected String, got Array`)

### ✅ Patrón recomendado: leer del Shadow DOM

La forma confiable de obtener el valor es acceder directamente al `<input>` dentro del Shadow DOM al momento de necesitar el dato (ej: al enviar un formulario):

```js
const getValue = (id) => {
  const el = document.querySelector(`#${id}`)
  return el?.shadowRoot?.querySelector('input')?.value ?? ''
}
```

### Ejemplo completo de formulario

```vue
<template>
  <section>
    <cns-input
      id="nombre"
      label="Nombre"
      type="text"
      placeholder="Ej: Juan"
      size="56"
    ></cns-input>

    <cns-input
      id="rut"
      label="RUT"
      type="rut"
      helper="Ingresa tu RUT sin puntos ni guión"
      size="56"
    ></cns-input>

    <cns-input
      id="email"
      label="Correo electrónico"
      type="email"
      placeholder="correo@ejemplo.cl"
      size="56"
    ></cns-input>

    <cns-button
      variant="primary"
      color="azul"
      size="56"
      label="Enviar"
      fullwidth
      @cnsclick="submitForm"
    ></cns-button>
  </section>
</template>

<script setup>
const getValue = (id) => {
  const el = document.querySelector(`#${id}`)
  return el?.shadowRoot?.querySelector('input')?.value ?? ''
}

const submitForm = () => {
  const data = {
    nombre: getValue('nombre'),
    rut: getValue('rut'),
    email: getValue('email'),
  }
  console.log('Formulario enviado:', data)
}
</script>
```

### Excepción: vee-validate + useField

Cuando se usa **vee-validate** con `useField`, el patrón `@input="(e) => field.value = e.detail"`
**sí funciona**, porque vee-validate gestiona el estado internamente sin depender del binding DOM
de Vue hacia el custom element. Ver `prisma-forms.md` para el patrón completo.

### Resumen de qué NO hacer (sin vee-validate)

```vue
<!-- ❌ v-model no funciona con custom elements -->
<cns-input v-model="nombre" />

<!-- ❌ :value reactivo causa warnings de tipo -->
<cns-input :value="nombre" />

<!-- ❌ @input con e.detail no entrega el valor esperado en binding directo -->
<cns-input @input="(e) => nombre = e.detail" />
```

## Eventos

| Evento | Descripción |
|--------|-------------|
| `input` | Se emite internamente pero **no es confiable** para leer valores desde Vue (ver sección anterior) |
| `focus` | Se emite cuando el input recibe foco |
| `blur` | Se emite cuando el input pierde foco |
| `change` | Se emite cuando el valor cambia y pierde foco |

## Tipos especiales

| Type | Comportamiento |
|------|---------------|
| `text` | Input de texto estándar |
| `password` | Oculta caracteres, ícono para mostrar/ocultar |
| `number` | Solo números |
| `email` | Formato de correo |
| `phone` | Formato de teléfono |
| `rut` | Formato RUT chileno con validación incorporada |
| `miles` | Formato numérico con separador de miles |
| `date` | Selector de fecha |
| `time` | Selector de hora |

## Tamaños

| Size | Descripción |
|------|-------------|
| `40` | Compacto |
| `48` | Intermedio |
| `56` | Destacado |

## Ejemplos de uso

```html
<!-- Básico con label y helper -->
<cns-input
  id="nombre"
  label="Nombre"
  helper="Ingresa tu nombre completo"
  placeholder="Ej: Juan Pérez"
  type="text"
></cns-input>

<!-- Con prefix y suffix -->
<cns-input
  id="monto"
  label="Monto"
  type="miles"
  prefix="$"
  suffix="CLP"
></cns-input>

<!-- RUT (formato y validación incorporada) -->
<cns-input
  id="rut"
  label="RUT"
  type="rut"
  helper="Ingresa tu RUT sin puntos ni guión"
></cns-input>

<!-- Password -->
<cns-input
  id="password"
  label="Contraseña"
  type="password"
  placeholder="Ingresa tu contraseña"
></cns-input>

<!-- Con error -->
<cns-input
  id="campo-error"
  label="Campo con error"
  type="text"
  error
  validation="Este campo es obligatorio"
></cns-input>

<!-- Con success -->
<cns-input
  id="campo-success"
  label="Campo válido"
  type="text"
  success
  validation="Datos guardados correctamente"
></cns-input>

<!-- Date -->
<cns-input
  id="fecha"
  label="Fecha de nacimiento"
  type="date"
  helper="Selecciona tu fecha"
></cns-input>

<!-- Phone -->
<cns-input
  id="telefono"
  label="Teléfono"
  type="phone"
  helper="Ingresa tu número"
></cns-input>

<!-- Tamaño compacto -->
<cns-input
  id="compact"
  label="Compacto"
  type="text"
  size="40"
></cns-input>

<!-- Disabled -->
<cns-input
  id="disabled"
  label="Deshabilitado"
  type="text"
  disabled
></cns-input>

<!-- Readonly con valor inicial -->
<cns-input
  id="readonly"
  label="Solo lectura"
  type="text"
  readonly
  value="Valor fijo"
></cns-input>
```
