---
inclusion: manual
---
# UI Kit V6 (Prisma) - Accordion

**Versión**: 6.1.0
**Paquete**: `@ui-kit/accordion-v6`

Acordeón para mostrar y ocultar contenido. Permite agregar íconos personalizados, controlar su estado y agrupar múltiples acordeones para comportamiento relacionado.

## Instalación

```bash
npm install @ui-kit/accordion-v6
```

Registro global en `main.ts`:

```typescript
import { registerAccordion } from '@ui-kit/accordion-v6'
registerAccordion()
```

O desde la librería global:

```typescript
import { CnsAccordion } from '@ui-kit/components-v6';
CnsAccordion();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `title` | string | - | Texto del encabezado |
| `expanded` | boolean | - | Define si está abierto por defecto |
| `showIcon` | boolean | - | Muestra/oculta el ícono a la derecha |
| `onToggle` | function | - | Callback al expandir/colapsar |

## Slots

| Slot | Descripción |
|------|-------------|
| `icon-left` | Ícono SVG a la izquierda del título |
| default | Contenido del acordeón (visible al expandir) |

## Ejemplos de uso

```html
<!-- Básico -->
<cns-accordion id="acc-1" title="Pregunta frecuente">
  <p>Respuesta al contenido del acordeón.</p>
</cns-accordion>

<!-- Expandido por defecto -->
<cns-accordion id="acc-2" title="Sección abierta" expanded>
  <p>Este contenido es visible al cargar.</p>
</cns-accordion>

<!-- Con ícono a la izquierda -->
<cns-accordion id="acc-3" title="Con ícono">
  <svg slot="icon-left">...</svg>
  <p>Contenido con ícono decorativo.</p>
</cns-accordion>

<!-- Sin ícono de flecha -->
<cns-accordion id="acc-4" title="Sin ícono" :showIcon="false">
  <p>Acordeón sin indicador visual de expand/collapse.</p>
</cns-accordion>

<!-- Disabled -->
<cns-accordion id="acc-5" title="Deshabilitado" disabled>
  <p>No responde a interacciones.</p>
</cns-accordion>

<!-- Grupo de acordeones -->
<cns-accordion id="acc-6" title="Sección 1">
  <p>Contenido sección 1</p>
</cns-accordion>
<cns-accordion id="acc-7" title="Sección 2">
  <p>Contenido sección 2</p>
</cns-accordion>
<cns-accordion id="acc-8" title="Sección 3">
  <p>Contenido sección 3</p>
</cns-accordion>
```

## Patrón FAQ con JSON-LD (Vue 3)

```vue
<template>
  <section>
    <cns-accordion
      v-for="(faq, index) in faqs"
      :key="index"
      :id="`faq-${index}`"
      :title="faq.question"
    >
      <p>{{ faq.answer }}</p>
    </cns-accordion>
  </section>
</template>

<script setup>
const faqs = [
  { question: '¿Cómo contrato?', answer: 'Ingresa a la sucursal virtual...' },
  { question: '¿Cuáles son los requisitos?', answer: 'Debes ser mayor de 18...' },
  { question: '¿Tiene costo?', answer: 'No tiene costo de mantención...' },
]
</script>
```
