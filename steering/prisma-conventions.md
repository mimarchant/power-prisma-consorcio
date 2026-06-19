---
inclusion: manual
---
# UI Kit V6 (Prisma) - Convenciones transversales

Reglas duras para usar componentes `cns-` en Vue 3. Son **opinionadas**: no describen todo lo
posible, sino cómo se hace en este proyecto. Cargar junto al steering del componente puntual.

> **Nota sobre las fuentes**: Los steering individuales de cada componente (`prisma-button.md`,
> `prisma-modal.md`, etc.) se generaron a partir de la documentación oficial del Storybook de
> Prisma. Este archivo de convenciones y `prisma-forms.md` se crearon por separado con patrones
> de integración reales del equipo. Si hay discrepancias entre un steering de componente y el
> Storybook actual, priorizar el Storybook y actualizar el `.md`.

## Eventos y Shadow DOM

- Los componentes `cns-` son web components: los datos del evento viajan en `event.detail`,
  **no** en `event.target.value`.

```vue
<script setup>
const onTabChange = (e) => { activeTab.value = e.detail.name }   // ✅
const onCode = (e) => { codigo.value = e.detail }                 // ✅ segmentedinput
</script>
```

- El botón emite `@cnsclick`, **no** `@click`:

```vue
<cns-button label="Continuar" variant="primary" color="azul" @cnsclick="continuar" />
```

- No estilar el interior del Shadow DOM ni depender de clases internas
  (`.panel__header`, `.modal__body`, etc.). Usar solo props y slots expuestos.

## v-model

Inputs de formulario (`cns-input`, `cns-textarea`, `cns-switch`, `cns-selector`, `cns-checkbox`)
emiten `update:modelValue` / `update:value`. Se pueden usar con `v-model`, pero validar siempre
que el valor llega por `detail` si se escucha el evento crudo.

## Overlays: visibilidad controlada por el padre

`cns-modal` y `cns-panel` **nunca se cierran solos**. El estado vive en el padre y es obligatorio
manejar `@close`.

```vue
<script setup>
import { ref } from 'vue'
const show = ref(false)
const close = () => { /* métricas/guardado previo */ show.value = false }
</script>

<template>
  <cns-modal :showModal="show" @close="close" title="..." interruptLevel="low" state="information">
    <div slot="footer">
      <cns-button label="Cancelar" variant="tertiary" fullwidth @cnsclick="close" />
      <cns-button label="Aceptar"  variant="primary"  fullwidth @cnsclick="close" />
    </div>
  </cns-modal>
</template>
```

- En `cns-panel` y `cns-modal`, los botones del slot `footer` deben llevar `fullwidth` (responsive).
- `interruptLevel="high"` para acciones irreversibles (no cierra con ESC ni clic fuera).

## Props que reciben arrays/objetos en HTML plano

`cns-selector` (`:values`) y `cns-stepper` (`:steps`) reciben JSON. En HTML van como string;
en Vue, pasarlos con binding y, si es atributo string, JSON válido con comillas dobles.

```vue
<cns-selector :values='[{"key":"1","value":"Opción 1"}]' type="text" label="..." />
<cns-stepper :currentstep="step" :steps="steps" orientation="horizontal" />
```

## Chile / negocio

- RUT: usar `cns-input type="rut"` (formato + validación incorporada). No reimplementar.
- Montos: `cns-input type="miles"` con `prefix="$"` / `suffix="CLP"`.
- Validación de formularios: alertas `type="section"` (menor prioridad); `type="page"` solo
  para avisos a nivel de página.

## Loading en Button

`loading` requiere el componente **ProgressSpinner** en el proyecto. Solo aplica a
`variant` primary/secondary, `color` azul/error, y **no** en `shape="circle"`.
Desactivar `loading` al terminar la acción async para no dejar el botón bloqueado.

## Estilos

- Solo tokens `--cns-*` y utilidades `cns-*` (spacing, tipografía, grid, sombras). Nunca hex.
- Texto sobre fondo claro: tonos 70-90. Sobre fondo oscuro: tonos 00-20. Respetar WCAG AA (4.5:1).
