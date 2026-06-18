---
inclusion: manual
---
# UI Kit V6 (Prisma) - Panel

**Versión**: 6.1.1
**Paquete**: `@ui-kit/panel-v6`

Panel es un contenedor visual que se desliza desde un borde de la pantalla y permite mostrar contenido adicional de forma no intrusiva. Ideal para flujos complementarios como formularios, detalles de ítems o acciones contextuales sin cambiar de página.

## Instalación

```bash
npm install @ui-kit/panel-v6
```

Registro global en `main.ts`:

```typescript
import { registerPanel } from '@ui-kit/panel-v6'
registerPanel()
```

O desde la librería global:

```typescript
import { CnsPanel } from '@ui-kit/components-v6';
CnsPanel();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `title` | string | - | Título principal del panel |
| `subtitle` | string | - | Subtítulo descriptivo |
| `show` | boolean | - | Controla la visibilidad del panel |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `close` | Se emite cuando el usuario hace clic en el botón de cerrar |

## Slots

| Slot | Descripción |
|------|-------------|
| `icon-left` | Ícono SVG a la izquierda del título |
| `content` | Contenido de texto o HTML dentro del cuerpo del panel |
| `footer` | Botones de acción (`<cns-button>` con `fullwidth` para responsividad) |

## Consideraciones

- La visibilidad se controla externamente con la prop `show`
- Es **obligatorio** manejar `@close="closePanel"` para ocultar el panel
- No necesita `v-show`; la prop `show` controla completamente la visibilidad
- El contenido del slot `content` tiene scroll vertical automático si supera la altura disponible
- No es necesario implementar clases como `.panel__header` o `.panel__body` (layout interno)
- Los botones en el slot `footer` deben tener `fullwidth` activado para correcto uso responsivo

## Ejemplos de uso

```vue
<script setup>
import { ref } from 'vue'

const showPanel = ref(false)
const openPanel = () => (showPanel.value = true)
const closePanel = () => (showPanel.value = false)
</script>

<template>
  <cns-button label="Abrir Panel" variant="primary" @cnsclick="openPanel" />

  <cns-panel
    title="Detalle del producto"
    subtitle="Información complementaria"
    :show="showPanel"
    @close="closePanel"
  >
    <svg slot="icon-left">...</svg>

    <div slot="content">
      <p>Contenido personalizado del panel.</p>
      <p>Puede incluir formularios, listas, etc.</p>
    </div>

    <div slot="footer">
      <cns-button label="Cancelar" variant="tertiary" fullwidth @cnsclick="closePanel" />
      <cns-button label="Confirmar" variant="primary" fullwidth @cnsclick="closePanel" />
    </div>
  </cns-panel>
</template>
```

```html
<!-- Panel básico sin footer -->
<cns-panel
  title="Información"
  :show="showInfo"
  @close="closeInfo"
>
  <div slot="content">
    <p>Texto informativo dentro del panel.</p>
  </div>
</cns-panel>

<!-- Panel con ícono y subtítulo -->
<cns-panel
  title="Mi cuenta"
  subtitle="Gestiona tu perfil"
  :show="showAccount"
  @close="closeAccount"
>
  <svg slot="icon-left">...</svg>
  <div slot="content">
    <p>Datos de la cuenta...</p>
  </div>
  <div slot="footer">
    <cns-button label="Guardar" variant="primary" fullwidth @cnsclick="guardar" />
  </div>
</cns-panel>
```
