---
inclusion: manual
---
# UI Kit V6 (Prisma) - PageLoader

**Versión**: 6.1.0
**Paquete**: `@ui-kit/pageloader-v6`

Aviso temporal que informa al usuario que una pantalla se está cargando. Una vez finalizada la carga, el indicador se reemplaza por la pantalla.

## Instalación

```bash
npm install @ui-kit/pageloader-v6
```

Registro global en `main.ts`:

```typescript
import { registerPageLoader } from '@ui-kit/pageloader-v6'
registerPageLoader()
```

O desde la librería global:

```typescript
import { CnsPageLoader } from '@ui-kit/components-v6';
CnsPageLoader();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | `cns-pageloader` | Identificador único |
| `title` | string | - | Texto del título |
| `description` | string | - | Texto de la descripción |
| `variant` | string | `loading` | Variante visual: `loading` |
| `showPageLoader` | boolean | false | Controla la visibilidad |
| `showTitle` | boolean | false | Muestra el título |
| `showDescription` | boolean | false | Muestra la descripción |
| `fullViewport` | boolean | true | Cubre todo el viewport |

### Props de accesibilidad

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `cnsAriaLabel` | string | `""` | Etiqueta aria-label |
| `cnsAriaDescription` | string | `""` | Descripción aria-description |

## Comportamiento de visibilidad

- `showPageLoader=true`: Loader visible, bloquea scroll del documento
- `showPageLoader=false`: Loader oculto, restaura scroll

El control del flujo de carga recae en el componente padre. Usar variable booleana ligada al estado de procesos asíncronos.

## Modos de visualización

### Full viewport (default)
Cubre todo el viewport. Ideal para carga de página completa.

### Contained mode (fullViewport=false)
Se muestra solo dentro de su contenedor inmediato. El contenedor debe tener `position: relative` y `overflow: hidden`.

## Accesibilidad

El componente expone `role="status"`, `aria-live="polite"` y `aria-atomic="true"`.

- Sin textos visibles y sin `cnsAriaLabel`: usa "Cargando" como nombre accesible por defecto
- Con `showTitle`: asocia automáticamente `aria-labelledby` al título visible
- Con `showDescription`: asocia automáticamente `aria-describedby` a la descripción visible
- `cnsAriaLabel` y `cnsAriaDescription` tienen prioridad sobre los textos visibles
- Monta un `aria-live` externo para compatibilidad con lectores de pantalla

## Ejemplos de uso

```html
<!-- Básico -->
<cns-pageloader
  id="loader-1"
  :showPageLoader="isLoading"
  variant="loading"
></cns-pageloader>

<!-- Con título y descripción -->
<cns-pageloader
  id="loader-2"
  :showPageLoader="isLoading"
  variant="loading"
  title="Cargando tu información"
  description="Esto puede tardar unos segundos"
  showTitle
  showDescription
></cns-pageloader>

<!-- Contained mode (dentro de un contenedor) -->
<div style="position: relative; overflow: hidden; height: 400px;">
  <cns-pageloader
    id="loader-3"
    :showPageLoader="isLoading"
    variant="loading"
    :fullViewport="false"
  ></cns-pageloader>
  <!-- Contenido del contenedor -->
</div>

<!-- Con accesibilidad personalizada -->
<cns-pageloader
  id="loader-4"
  :showPageLoader="isLoading"
  variant="loading"
  cnsAriaLabel="Procesando tu solicitud"
  cnsAriaDescription="Este proceso puede tardar hasta 30 segundos"
></cns-pageloader>
```

## Patrón de uso recomendado (Vue 3)

```vue
<template>
  <div>
    <cns-button @cnsclick="cargarDatos()" label="Cargar datos" variant="primary" />

    <cns-pageloader
      id="loader"
      :showPageLoader="isLoading"
      variant="loading"
      title="Cargando datos"
      showTitle
    ></cns-pageloader>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isLoading = ref(false)

const cargarDatos = async () => {
  isLoading.value = true
  try {
    await fetch('/api/datos')
  } finally {
    isLoading.value = false
  }
}
</script>
```
