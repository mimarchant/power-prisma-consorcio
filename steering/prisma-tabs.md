---
inclusion: manual
---
# UI Kit V6 (Prisma) - Tabs

**Versión**: 6.1.0
**Paquete**: `@ui-kit/tabs-v6`

Tabs permiten organizar contenido relacionado en diferentes vistas bajo una misma área. Cada pestaña muestra una sección distinta al ser seleccionada.

## Instalación

```bash
npm install @ui-kit/tabs-v6
```

Registro global en `main.ts`:

```typescript
import { registerTabs, registerTab } from '@ui-kit/tabs-v6'
registerTabs()
registerTab()
```

O desde la librería global:

```typescript
import { CnsTabs, CnsTab } from '@ui-kit/components-v6';
CnsTabs();
CnsTab();
```

## Props de `<cns-tabs>`

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `variant` | string | - | Orientación: `horizontal`, `vertical` |
| `color` | string | - | Color: `azul` (privado), `cielo` (público) |
| `size` | string | - | Altura: `40` (compacto), `56` (grande) |
| `fullWidth` | boolean | - | Ocupa el 100% del ancho del contenedor |
| `selected` | string | - | Nombre del tab seleccionado actualmente |

## Props de `<cns-tab>`

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `name` | string | - | Nombre único del tab (identificador) |
| `id` | string | - | Identificador único |
| `disabled` | boolean | - | Desactiva la interacción |
| `badge` | string | - | Badge numérico |

## Eventos

| Evento | Componente | Descripción |
|--------|-----------|-------------|
| `cnsTabClick` | `<cns-tab>` | Se emite al hacer clic en un tab |

## Slots de `<cns-tab>`

| Slot | Descripción |
|------|-------------|
| `icon` | Ícono SVG dentro del tab |
| default | Texto del tab |

## Orientaciones

| Variant | Descripción |
|---------|-------------|
| `horizontal` | Tabs en fila horizontal |
| `vertical` | Tabs apilados verticalmente |

## Colores

| Color | Contexto |
|-------|----------|
| `azul` | Productos digitales privados (Sucursal Virtual) |
| `cielo` | Productos digitales públicos (páginas promocionales) |

## Tamaños

| Size | Descripción |
|------|-------------|
| `56` | Grande (default) |
| `40` | Compacto |

## Ancho

| Modo | Descripción |
|------|-------------|
| Intrínseco (sin fullWidth) | Se ajusta al contenido de las pestañas |
| `fullWidth` | Se extiende a lo largo del contenedor padre |

## Ejemplos de uso

```html
<!-- Básico horizontal -->
<cns-tabs variant="horizontal" color="azul" size="56">
  <cns-tab name="home" id="tab-1" @cnsTabClick="handleTabChange">
    Inicio
  </cns-tab>
  <cns-tab name="profile" id="tab-2">
    Perfil
  </cns-tab>
  <cns-tab name="settings" id="tab-3">
    Configuración
  </cns-tab>
</cns-tabs>

<!-- Con íconos y badges -->
<cns-tabs variant="horizontal" color="azul" size="56" fullWidth>
  <cns-tab name="home" id="tab-1" badge="0" @cnsTabClick="handleTabChange">
    <div slot="icon">
      <svg>...</svg>
    </div>
    Inicio
  </cns-tab>
  <cns-tab name="profile" id="tab-2" badge="3">
    Perfil
  </cns-tab>
  <cns-tab name="settings" id="tab-3" disabled>
    Ajustes
  </cns-tab>
</cns-tabs>

<!-- Vertical -->
<cns-tabs variant="vertical" color="azul" size="56">
  <cns-tab name="home" id="tab-v1">Inicio</cns-tab>
  <cns-tab name="profile" id="tab-v2">Perfil</cns-tab>
  <cns-tab name="settings" id="tab-v3">Configuración</cns-tab>
</cns-tabs>

<!-- Color cielo (público) -->
<cns-tabs variant="horizontal" color="cielo" size="56">
  <cns-tab name="tab1" id="tab-c1">Inicio</cns-tab>
  <cns-tab name="tab2" id="tab-c2">Perfil</cns-tab>
</cns-tabs>

<!-- Compacto (40px) -->
<cns-tabs variant="horizontal" color="azul" size="40">
  <cns-tab name="tab1" id="tab-s1">Inicio</cns-tab>
  <cns-tab name="tab2" id="tab-s2">Perfil</cns-tab>
</cns-tabs>

<!-- Tab seleccionado programáticamente -->
<cns-tabs variant="horizontal" color="azul" size="56" selected="profile">
  <cns-tab name="home" id="tab-p1">Inicio</cns-tab>
  <cns-tab name="profile" id="tab-p2">Perfil</cns-tab>
</cns-tabs>
```

## Patrón de uso con contenido (Vue 3)

```vue
<script setup>
import { ref } from 'vue'

const activeTab = ref('home')

const handleTabChange = (event) => {
  activeTab.value = event.detail.name
}
</script>

<template>
  <cns-tabs variant="horizontal" color="azul" size="56" :selected="activeTab">
    <cns-tab name="home" id="tab-1" @cnsTabClick="handleTabChange">Inicio</cns-tab>
    <cns-tab name="profile" id="tab-2" @cnsTabClick="handleTabChange">Perfil</cns-tab>
    <cns-tab name="settings" id="tab-3" @cnsTabClick="handleTabChange">Ajustes</cns-tab>
  </cns-tabs>

  <div v-if="activeTab === 'home'">Contenido de inicio</div>
  <div v-if="activeTab === 'profile'">Contenido de perfil</div>
  <div v-if="activeTab === 'settings'">Contenido de ajustes</div>
</template>
```
