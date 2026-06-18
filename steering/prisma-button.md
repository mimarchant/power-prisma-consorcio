---
inclusion: manual
---
# UI Kit V6 (Prisma) - Button

**Versión**: 6.1.0
**Paquete**: `@ui-kit/button-v6`

Button permite a los usuarios iniciar una acción o responder a un evento con un solo clic.

## Instalación

```bash
npm install @ui-kit/button-v6
```

Registro global en `main.ts`:

```typescript
import { registerButton } from '@ui-kit/button-v6'
registerButton()
```

O desde la librería global:

```typescript
import { CnsButton } from '@ui-kit/components-v6';
CnsButton();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `label` | string | - | Texto que se muestra en el botón |
| `variant` | string | - | Tipo de botón: `primary`, `secondary`, `tertiary` |
| `color` | string | - | Color: `azul`, `cielo`, `error`, `blanco`, `arena`, `calypso`, `lima`, `morado` |
| `size` | string | - | Tamaño (altura en px): `40`, `48`, `56` |
| `shape` | string | - | Forma: `rectangular`, `pill`, `circle` |
| `disabled` | boolean | - | Deshabilita el botón |
| `fullwidth` | boolean | - | Ocupa todo el ancho del contenedor |
| `loading` | boolean | false | Estado de carga (muestra spinner) |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `cnsclick` | Evento de clic del botón |

## Slots

| Slot | Descripción |
|------|-------------|
| `icon-left` | Ícono SVG al inicio del botón |
| `icon-right` | Ícono SVG al final del botón |

## Variantes

| Variante | Uso |
|----------|-----|
| `primary` | Acción principal |
| `secondary` | Acciones de menor prioridad |
| `tertiary` | Acciones opcionales o complementarias |

## Tamaños

| Size | Descripción |
|------|-------------|
| `40` | Compacto |
| `48` | Intermedio (por defecto) |
| `56` | Destacado o para pantallas táctiles |

Para botones `circle`, se muestra un ícono en lugar de texto.

## Formas (shape)

| Shape | Descripción |
|-------|-------------|
| `rectangular` | Bordes rectos con border-radius |
| `pill` | Bordes completamente redondeados |
| `circle` | Botón circular (solo ícono) |

## Colores y contexto de fondo

| Color | Fondo recomendado |
|-------|-------------------|
| `azul` | Fondo blanco |
| `cielo` | Fondo blanco |
| `error` | Fondo blanco |
| `blanco` | Fondo `var(--cns-primary-brand-50)` |
| `arena` | Fondo `var(--cns-primary-brand-50)` |
| `calypso` | Fondo `var(--cns-primary-brand-50)` |
| `lima` | Fondo `var(--cns-primary-brand-50)` |
| `morado` | Fondo `var(--cns-primary-brand-50)` |

## Loading

Estado de carga que muestra un spinner y deshabilita la interacción.

### Restricciones

- Solo aplica para `variant`: `primary` y `secondary`
- Solo aplica para `color`: `azul` y `error`
- No se aplica en `shape: circle`

### Comportamiento

- Al activar `loading=true`, el botón se comporta como disabled
- El ícono izquierdo se reemplaza por ProgressSpinner
- El ícono derecho se oculta
- El label se mantiene visible

### Dependencia

Requiere el componente **ProgressSpinner** disponible en el proyecto.

### Recomendación

Usar `loading` solo para acciones asíncronas y desactivarlo al finalizar para evitar que el botón quede bloqueado.

## Ejemplos de uso

```html
<!-- Primary básico -->
<cns-button variant="primary" color="azul" label="Confirmar"></cns-button>

<!-- Secondary con tamaño -->
<cns-button variant="secondary" color="azul" size="40" label="Cancelar"></cns-button>

<!-- Pill fullwidth -->
<cns-button variant="primary" color="azul" shape="pill" fullwidth label="Continuar"></cns-button>

<!-- Con íconos -->
<cns-button variant="primary" color="azul" label="Siguiente">
  <svg slot="icon-right">...</svg>
</cns-button>

<!-- Circle (solo ícono) -->
<cns-button variant="primary" color="azul" shape="circle" size="48">
  <svg slot="icon-left">...</svg>
</cns-button>

<!-- Loading -->
<cns-button variant="primary" color="azul" label="Enviando" loading></cns-button>

<!-- Disabled -->
<cns-button variant="primary" color="azul" label="No disponible" disabled></cns-button>

<!-- Sobre fondo azul -->
<cns-button variant="primary" color="blanco" label="Acción"></cns-button>
```
