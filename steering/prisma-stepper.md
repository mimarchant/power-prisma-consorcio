---
inclusion: manual
---
# UI Kit V6 (Prisma) - Stepper

**Versión**: 6.1.0
**Paquete**: `@ui-kit/stepper-v6`

Stepper guía a los usuarios a través de flujos secuenciales, mostrando el progreso y los pasos restantes.

## Instalación

```bash
npm install @ui-kit/stepper-v6
```

Registro global en `main.ts`:

```typescript
import { registerStepper } from '@ui-kit/stepper-v6'
registerStepper()
```

O desde la librería global:

```typescript
import { CnsStepper } from '@ui-kit/components-v6';
CnsStepper();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `orientation` | string | `horizontal` | Orientación: `horizontal`, `vertical` |
| `currentstep` | number | `1` | Número del paso actual (índice base 1) |
| `steps` | array | - | Arreglo de objetos que define los pasos |
| `cnsAriaLabel` | string | `Progreso del proceso` | Texto aria-label |

## Objeto step

Cada objeto en el arreglo `steps` puede tener:

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `title` | string | Título del paso |
| `description` | string | Descripción o información adicional |
| `disabled` | boolean | Deshabilita la interacción para ese paso |
| `complete` | boolean | Indica paso completado (muestra ícono de verificación) |

## Estados de cada paso

| Estado | Descripción |
|--------|-------------|
| Completado | Paso finalizado, muestra ícono de check |
| Actual | Paso activo en el que se encuentra el usuario |
| Pendiente | Paso futuro, aún no alcanzado |
| Deshabilitado | Paso no interactuable |

## Orientaciones

### Horizontal
Pasos en una fila. Ideal para flujos cortos (3-5 pasos) en desktop.

### Vertical
Pasos apilados en columna. Mejor para flujos largos o en mobile.

## Ejemplos de uso

```html
<!-- Horizontal básico -->
<cns-stepper
  id="stepper-1"
  orientation="horizontal"
  :currentstep="3"
  :steps='[
    { "title": "Paso 1", "description": "Datos personales", "complete": true },
    { "title": "Paso 2", "description": "Dirección", "complete": true },
    { "title": "Paso 3", "description": "Confirmación" },
    { "title": "Paso 4", "description": "Pago" },
    { "title": "Paso 5", "description": "Resumen" }
  ]'
></cns-stepper>

<!-- Vertical -->
<cns-stepper
  id="stepper-2"
  orientation="vertical"
  :currentstep="5"
  :steps='[
    { "title": "Paso 1", "description": "Descripción paso 1", "complete": true },
    { "title": "Paso 2", "description": "Descripción paso 2", "complete": true },
    { "title": "Paso 3", "description": "Descripción paso 3", "complete": true },
    { "title": "Paso 4", "description": "Descripción paso 4", "complete": true },
    { "title": "Paso 5", "description": "Descripción paso 5" }
  ]'
></cns-stepper>

<!-- Con paso deshabilitado -->
<cns-stepper
  id="stepper-3"
  orientation="horizontal"
  :currentstep="2"
  :steps='[
    { "title": "Inicio", "description": "Bienvenida", "complete": true },
    { "title": "Formulario", "description": "Completa tus datos" },
    { "title": "Validación", "description": "Verificación" },
    { "title": "Bloqueado", "description": "Requiere aprobación", "disabled": true }
  ]'
></cns-stepper>
```

## Patrón de uso dinámico (Vue 3)

```vue
<script setup>
import { ref } from 'vue'

const currentStep = ref(1)

const steps = [
  { title: 'Datos personales', description: 'Ingresa tu información' },
  { title: 'Dirección', description: 'Dónde vives' },
  { title: 'Confirmación', description: 'Revisa y confirma' },
]

const siguiente = () => {
  if (currentStep.value < steps.length) {
    steps[currentStep.value - 1].complete = true
    currentStep.value++
  }
}

const anterior = () => {
  if (currentStep.value > 1) {
    currentStep.value--
    steps[currentStep.value - 1].complete = false
  }
}
</script>

<template>
  <cns-stepper
    id="stepper-flow"
    orientation="horizontal"
    :currentstep="currentStep"
    :steps="steps"
  ></cns-stepper>

  <cns-button label="Anterior" variant="tertiary" @cnsclick="anterior" />
  <cns-button label="Siguiente" variant="primary" @cnsclick="siguiente" />
</template>
```
