---
inclusion: manual
---
# Migración DS5 → Prisma (UI Kit V6)

Guía para migrar componentes del Design System 5 (`@ui-kit/components-v5`, `@ui-kit/components-v4`)
al Design System Prisma (`@ui-kit/components-v6`). Cubre los breaking changes y mapeos de props/eventos.

> **Origen**: DS5 usa paquetes `@ui-kit/components-v5` + `@ui-kit/styles@2.0.2`.
> Prisma usa `@ui-kit/components-v6` + `@ui-kit/styles-v6`.
> Ambos usan web components `<cns-*>` pero con APIs distintas.

---

## Cambios generales (aplican a todos los componentes)

| Concepto | DS5 | Prisma |
|----------|-----|--------|
| Paquete estilos | `@ui-kit/styles@^2.0.2` | `@ui-kit/styles-v6` |
| Paquete global | `@ui-kit/components-v5` | `@ui-kit/components-v6` |
| Paquete individual | `@ui-kit/button` | `@ui-kit/button-v6` (sufijo `-v6`) |
| Registro | `registerButton()` | `registerButton()` (igual) |
| Import global | `CnsButton()` desde `@ui-kit/components-v4` | `CnsButton()` desde `@ui-kit/components-v6` |
| Variante Vue 3 | `<cnsc-*>` (componente Vue) | No existe — todo es `<cns-*>` (web component) |
| Evento click | `@cnsclick` | `@cnsclick` (se mantiene) |
| Datos evento | `event.detail` | `event.detail` (se mantiene) |
| Tokens CSS | `--cns-primary-blue-consorcio`, `--cns-semantyc-*` (typos) | `--cns-primary-brand-50`, `--cns-semantic-*` (corregido) |

### Tokens CSS renombrados

| DS5 | Prisma |
|-----|--------|
| `--cns-primary-blue-consorcio` | `--cns-primary-brand-50` |
| `--cns-primary-blue-dark` | `--cns-primary-marino-50` |
| `--cns-secondary-lightblue-consorcio` | `--cns-primary-cielo-50` |
| `--cns-semantyc-error-alert` | `--cns-semantic-error-50` |
| `--cns-semantyc-success` | `--cns-semantic-success-50` |
| `--cns-semantyc-warning` | `--cns-semantic-warning-50` |
| `--cns-semantyc-information` | `--cns-semantic-info-50` |
| `--cns-gray-scale-gray-dark` | `--cns-neutral-50` |
| `--cns-gray-scale-gray-lightness` | `--cns-neutral-20` |
| `--cns-basic-colors-white` | `--cns-neutral-00` |
| `--cns-basic-colors-black` | `--cns-neutral-90` |

---

## Button

### Mapeo de props

| DS5 prop | Prisma prop | Notas |
|----------|-------------|-------|
| `theme="primary-blue"` | `variant="primary" color="azul"` | Se separan variante y color |
| `theme="primary-green"` | `variant="primary" color="azul"` | En DS5 green = blue desde v5 |
| `theme="secondary-blue"` | `variant="secondary" color="azul"` | Outline → secondary |
| `theme="secondary-red"` | `variant="secondary" color="error"` | |
| `theme="secondary-lightblue"` | `variant="secondary" color="cielo"` | |
| `theme="secondary-dark"` | `variant="secondary" color="azul"` | No hay "dark" en Prisma |
| `theme="solid-morado"` | `variant="primary" color="morado"` | |
| `theme="solid-sand"` | `variant="primary" color="arena"` | |
| `theme="solid-lime"` | `variant="primary" color="lima"` | |
| `theme="solid-white"` | `variant="primary" color="blanco"` | Para fondo azul |
| `theme="circular-white"` | `shape="circle"` | + slot icon-left |
| `size="xsm"` | `size="40"` | Tamaños ahora en px |
| `size="sm"` | `size="48"` | |
| `size="lg"` | `size="56"` | |
| `size="xlg"` | `size="56"` | No hay equivalente mayor |
| `outline` | `variant="secondary"` | Outline es ahora secondary |
| `inactive` | `disabled` | No hay "inactive" en Prisma |
| `iconsrc="<svg>..."` | `<svg slot="icon-left">` o `slot="icon-right"` | SVG va como slot hijo |
| `iconposition="left"` | `slot="icon-left"` | Posición por nombre del slot |
| `iconposition="right"` | `slot="icon-right"` | |
| `fixedwidth` / `buttonstyle="width:100%"` | `fullwidth` | |
| `mobile` | — | No existe, responsive automático |
| `nohover` | — | No existe |
| `notAllowed` | `disabled` | |
| `type="submit"` | — | No existe, siempre "button" |
| `loading` | `loading` | Se mantiene (solo primary/secondary + azul/error) |

### Ejemplo de migración

```html
<!-- DS5 -->
<cns-button
  id="btn-1"
  label="Continuar"
  theme="primary-blue"
  size="sm"
  :outline="true"
  iconposition="left"
  :iconsrc="iconSvg"
/>

<!-- Prisma -->
<cns-button
  variant="secondary"
  color="azul"
  size="48"
  label="Continuar"
>
  <svg slot="icon-left"><!-- contenido SVG --></svg>
</cns-button>
```

### Props eliminadas (sin equivalente)

`inactive`, `nohover`, `iconanimation`, `notAllowed`, `mobile`, `fixedwidth`, `buttonstyle`, `type`

---

## Input

### Mapeo de props

| DS5 prop | Prisma prop | Notas |
|----------|-------------|-------|
| `type="text"` | `type="text"` | Igual |
| `type="rut"` | `type="rut"` | Igual, formato integrado en v6 |
| `type="rut" formatonchange` | `type="rut"` | Formato on-change es default en v6 |
| `type="miles"` | `type="miles"` | Igual |
| `type="number"` | `type="number"` | Igual |
| `type="email"` | `type="email"` | Igual |
| `type="phone"` | `type="phone"` | Igual |
| `type="password"` + `iconinput` + `iconinputchange` | `type="password"` | Toggle show/hide integrado en v6 |
| `type="pat"` | — | No existe en Prisma |
| `date mobiledate` (booleans) | `type="date"` | Unificado en un solo type |
| `label` | `label` | Igual |
| `placeholder` | `placeholder` | Igual |
| `disabled` | `disabled` | Igual |
| `readonly` | `readonly` | Igual |
| `error` | `error` | Igual |
| `success` | `success` | Igual |
| `optional` | `optional` | Igual |
| `prefix` | `prefix` | Igual |
| `suffix` | `suffix` | Igual |
| `maxlength` | `maxlength` | Igual |
| `minlength` | `minlength` | Igual |
| `value` | `value` | Igual (solo inicialización) |
| `auxilartext` | `helper` | Renombrado |
| `ftrmsgtext` | `validation` | Mensaje de error/validación |
| `mandatorysublabel="*"` | `required` | Boolean en v6 |
| `iconinput` + `iconinputposition` | `iconleft` / `iconright` | Props separadas en v6 |
| `labelfloating` | — | No existe, label siempre arriba |
| `loading` | — | No existe en input de v6 |
| `typemask="miles"` | `type="miles"` | Unificado en type |
| `search` | — | No existe |
| `withControls` | — | No existe |
| `hastextarea` | — | Usar `<cns-textarea>` (componente separado) |
| `darkmode` | — | No existe |
| `clearble` | — | No existe |

### Cambio crítico: lectura de valores

En DS5 se podía leer con `@input` o `@cnsinput` y acceder a `e.target.value`.
En Prisma **no funciona así** — las opciones son:

1. **Sin librería de formularios**: leer del Shadow DOM al submit
   ```js
   const getValue = (id) => {
     const el = document.querySelector(`#${id}`)
     return el?.shadowRoot?.querySelector('input')?.value ?? ''
   }
   ```

2. **Con vee-validate**: sincronizar vía `e.detail` con `useField`
   ```js
   const { value: rut } = useField('rut')
   const onRut = (e) => { rut.value = e.detail }
   ```

### Paquete `@ui-kit/inputs-utils` eliminado

Las funciones `formatRUT`, `validarRut`, `formatearMiles`, `phoneFormatter`, `validateEmail`
ya no se necesitan porque el componente Prisma las tiene integradas. Si necesitas validación
a nivel de esquema (Yup), implementa `rutValido` manualmente (ver `prisma-forms.md`).

### Ejemplo de migración

```html
<!-- DS5 -->
<cns-input
  id="input-rut"
  label="RUT"
  type="rut"
  formatonchange
  auxilartext="Ingresa tu RUT"
  :iconinput="iconSvg"
  iconinputposition="left"
/>

<!-- Prisma -->
<cns-input
  id="input-rut"
  label="RUT"
  type="rut"
  helper="Ingresa tu RUT"
  iconleft="<svg>...</svg>"
/>
```

---

## Modal

### Cambio de arquitectura

El modal de Prisma tiene un diseño completamente diferente:

| Aspecto | DS5 | Prisma |
|---------|-----|--------|
| Montaje | `v-if` (monta/desmonta el DOM) | `:showModal` (prop, siempre montado) |
| Botones | Props del modal (`buttonactionlabel`, etc.) | Slot `footer` con `<cns-button>` |
| Ícono | Prop `iconmodal` (SVG manual) | Automático según `state` |
| Tipos | `type="error"` / `info` / `warning` / `success` | `state="error"` / `information` / `warning` / `success` / `critical` / `discovery` |
| Cierre | `@close` + `v-if=false` | `@close` + `:showModal=false` |
| Acciones | `@action`, `@sencodaryAction` | `@cnsclick` en cada button del slot |
| Interrupción | No existe | `interruptLevel="low"` / `medium` / `high"` |
| Estilo título | `titlestyle="..."` | No estilizable inline |
| Contenido | Slot default | `description` (prop) + slot `content` |
| Evento global | `document.addEventListener("evt-ui-kit", ...)` | No existe |
| Modal SPUI | `<cns-modal-spui isopen>` (componente separado) | No existe — usar `cns-modal` + slot |

### Mapeo de props

| DS5 prop | Prisma prop | Notas |
|----------|-------------|-------|
| `title` | `title` | Igual |
| `type="error"` | `state="error"` | Renombrado |
| `type="info"` | `state="information"` | Nombre cambia |
| `type="warning"` | `state="warning"` | Igual |
| `type="success"` | `state="success"` | Igual |
| `closelabel` | — | No existe, ícono integrado |
| `closeicon` | — | No existe, ícono integrado |
| `closecolor` | — | No existe |
| `iconmodal` | `showIcon` (boolean) | Ícono automático según state |
| `buttonactionlabel` | — | Usar `<cns-button label="...">` en slot footer |
| `buttoncancellabel` | — | Usar `<cns-button label="...">` en slot footer |
| `buttonactiondisabled` | — | Usar `<cns-button disabled>` en slot footer |
| `buttonactiontheme` | — | Usar `variant`/`color` en el button del slot |
| `buttonOutLine` | — | Usar `variant="secondary"` en el button |
| `buttonsOnColumns` | — | CSS propio en el slot footer |
| `titlestyle` | — | No existe |
| — | `interruptLevel` | Nuevo: controla cierre por ESC/clic fuera |
| — | `showModal` | Nuevo: controla visibilidad (antes era `v-if`) |
| — | `description` | Nuevo: texto descriptivo sin slot |
| — | `showSlot` | Nuevo: habilita slot content |
| — | `showFooter` | Nuevo: muestra/oculta footer |

### Ejemplo de migración

```html
<!-- DS5 -->
<cns-modal
  v-if="showModal"
  id="modal-1"
  title="¿Estás seguro?"
  type="warning"
  :closeicon="iconClose"
  closelabel="cerrar"
  :iconmodal="iconWarn"
  buttonactionlabel="Sí, continuar"
  buttoncancellabel="No, cancelar"
  @close="showModal = false"
  @action="confirmar"
  @sencodaryAction="showModal = false"
>
  Esta acción no se puede deshacer.
</cns-modal>

<!-- Prisma -->
<cns-modal
  :showModal="showModal"
  @close="closeModal"
  title="¿Estás seguro?"
  description="Esta acción no se puede deshacer"
  state="warning"
  interruptLevel="high"
>
  <div slot="footer">
    <cns-button label="No, cancelar" variant="tertiary" fullwidth @cnsclick="closeModal" />
    <cns-button label="Sí, continuar" variant="primary" color="azul" fullwidth @cnsclick="confirmar" />
  </div>
</cns-modal>
```

### Patrón de visibilidad

```js
// DS5: montar/desmontar con v-if
// showModal = true  → <cns-modal v-if="showModal">
// showModal = false → componente se desmonta

// Prisma: prop controla visibilidad (componente siempre en DOM)
const showModal = ref(false)
const closeModal = () => { showModal.value = false }
// <cns-modal :showModal="showModal" @close="closeModal">
```

---

## Checklist de migración

```
□ Actualizar paquetes: @ui-kit/*-v6 + @ui-kit/styles-v6
□ Buscar y reemplazar tokens CSS (--cns-primary-blue-consorcio → --cns-primary-brand-50, etc.)
□ Button: separar theme en variant + color, mover íconos a slots
□ Input: unificar types (date/rut/miles), cambiar auxilartext → helper, ftrmsgtext → validation
□ Input: adaptar lectura de valores (shadowRoot o vee-validate)
□ Modal: cambiar v-if por :showModal, mover botones al slot footer
□ Modal: type → state, agregar interruptLevel
□ Eliminar imports de @ui-kit/inputs-utils (formatRUT, etc.)
□ Eliminar listeners globales de "evt-ui-kit"
□ Verificar que PurgeCSS safelist incluya clases cns- de v6
```
