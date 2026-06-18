---
inclusion: manual
---
# UI Kit V6 (Prisma) - ProgressSpinner

**Versión**: 6.1.0
**Paquete**: `@ui-kit/progressspinner-v6`

Un indicador circular que muestra visualmente la progresión de una operación del sistema (descargas, cargas, procesamiento). Puede ser determinado o indeterminado.

## Instalación

```bash
npm install @ui-kit/progressspinner-v6
```

Registro global en `main.ts`:

```typescript
import { registerProgressSpinner } from '@ui-kit/progressspinner-v6'
registerProgressSpinner()
```

O desde la librería global:

```typescript
import { CnsProgressSpinner } from '@ui-kit/components-v6';
CnsProgressSpinner();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | `cns-progressspinner` | Identificador único |
| `color` | string | `Azul` | Estilo visual: `Azul`, `Error` |
| `theme` | string | `Positive` | Contexto semántico: `Positive` (fondo claro), `Negative` (fondo oscuro) |
| `size` | string | `md` | Tamaño: `xs`, `sm`, `md`, `lg`, `xl` |
| `spinnerType` | string | `Indeterminate` | Modo: `Indeterminate` (continuo), `Determinate` (porcentaje) |
| `value` | number | - | Porcentaje de avance 0-100 (solo para `Determinate`) |
| `showSpinner` | boolean | false | Controla la visibilidad del spinner |

### Props de accesibilidad

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `cnsAria` | boolean | false | Expone atributos ARIA en el componente |
| `cnsAriaLabel` | string | - | Etiqueta accesible |
| `cnsAriaDescription` | string | - | Descripción accesible |

## Modos de funcionamiento

### Indeterminate

Animación continua sin indicar porcentaje. Para operaciones de duración desconocida.

```html
<cns-progressspinner
  spinnerType="Indeterminate"
  :showSpinner="isLoading"
  color="Azul"
  size="md"
></cns-progressspinner>
```

### Determinate

Muestra porcentaje real de avance (0 a 100). Para operaciones con progreso medible.

```html
<cns-progressspinner
  spinnerType="Determinate"
  :value="progreso"
  :showSpinner="isLoading"
  color="Azul"
  size="md"
></cns-progressspinner>
```

## Tamaños

| Size | Uso |
|------|-----|
| `xs` | Inline, dentro de botones |
| `sm` | Elementos compactos |
| `md` | Uso general (default) |
| `lg` | Secciones destacadas |
| `xl` | Pantallas completas de carga |

## Colores y themes

| Color | Theme | Fondo recomendado |
|-------|-------|-------------------|
| `Azul` | `Positive` | Fondo claro |
| `Azul` | `Negative` | Fondo oscuro (#00263D) |
| `Error` | `Positive` | Fondo claro |
| `Error` | `Negative` | Fondo oscuro (#00263D) |

## Visibilidad

- Cuando `showSpinner=false`: no se renderiza, el contenedor muestra su contenido normal
- Cuando `showSpinner=true`: se oculta el contenido previo y se muestra el spinner centrado
- Controlar con una variable booleana (ej: `isLoading`) ligada al estado de la operación

## Accesibilidad

### Enfoque recomendado: Accesibilidad en el contenedor

El spinner actúa solo como apoyo visual. El contenedor maneja `role="status"`, `aria-live`, etc.

```html
<div role="status" aria-live="polite" aria-label="Cargando datos">
  <cns-progressspinner
    :cnsAria="false"
    spinnerType="Indeterminate"
    :showSpinner="isLoading"
  ></cns-progressspinner>
</div>
```

### Enfoque alternativo: Accesibilidad en el componente

Usar cuando no se puede controlar el contenedor.

```html
<!-- Indeterminate -->
<cns-progressspinner
  :cnsAria="true"
  cnsAriaLabel="Operación en curso"
  cnsAriaDescription="Procesando solicitud"
  spinnerType="Indeterminate"
  :showSpinner="true"
></cns-progressspinner>

<!-- Determinate -->
<cns-progressspinner
  :cnsAria="true"
  cnsAriaLabel="Descargando archivo"
  spinnerType="Determinate"
  :value="75"
  :showSpinner="true"
></cns-progressspinner>
```

## Recomendaciones

- Controlar `showSpinner` con una variable de estado (`isLoading`), no dejarlo fijo en `true`
- Preferir accesibilidad en el contenedor (`cnsAria=false`) para evitar duplicar mensajes en lectores de pantalla
- Es dependencia del componente **Button** en estado `loading`
