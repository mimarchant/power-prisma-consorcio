---
inclusion: manual
---
# UI Kit V6 (Prisma) - Switch

**Versión**: 6.1.0
**Paquete**: `@ui-kit/switch-v6`

Switch permite a los usuarios alternar entre dos estados (encendido/apagado). Se puede personalizar con etiqueta, helper text e ícono opcional.

## Instalación

```bash
npm install @ui-kit/switch-v6
```

Registro global en `main.ts`:

```typescript
import { registerSwitch } from '@ui-kit/switch-v6'
registerSwitch()
```

O desde la librería global:

```typescript
import { CnsSwitch } from '@ui-kit/components-v6';
CnsSwitch();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `status` | string | - | Estado actual: `on`, `off` |
| `disabled` | boolean | - | Desactiva la interacción |
| `focus` | boolean | - | Aplica estado de enfoque |
| `labelText` | string | - | Texto visible asociado al switch |
| `showHelperText` | boolean | - | Muestra/oculta el helper text |
| `helperText` | string | - | Texto de ayuda bajo el switch |
| `controlDirection` | string | - | Posición del toggle: `left`, `right` |
| `variant` | string | - | Estilo visual: `base`, `blank`, `box` |
| `showIcon` | boolean | - | Muestra ícono decorativo cuando está activo |
| `icon` | string | - | Ícono SVG cuando `showIcon` está activado |
| `isFullWidth` | boolean | - | Toma el 100% del ancho del contenedor |
| `valueon` | boolean | - | Valor que representa el estado "on" |
| `valueoff` | boolean | - | Valor que representa el estado "off" |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `update:modelValue` | Cambio de estado (compatible con v-model) |
| `input` | Se emite al alternar. Valor emitido: `valueon`/`valueoff` |
| `update:focus` | Se emite cuando gana o pierde foco |

## Variantes

| Variante | Descripción |
|----------|-------------|
| `base` | Switch independiente, interactivo con hover visual |
| `blank` | Sin énfasis visual de caja, más limpio |
| `box` | Contenido en caja con borde neutral (ancho default 343px), ideal para formularios |

## Comportamiento visual

- **Off**: Toggle gris, indica opción desactivada
- **On**: Toggle azul, indica opción activada
- **Hover off**: Gris más oscuro (#B0B0B0) con sombra suave
- **Hover on**: Azul más oscuro (#002B4F) con sombra más pronunciada
- **Disabled**: No permite interacción

## Posicionamiento (controlDirection)

| Dirección | Descripción |
|-----------|-------------|
| `left` | Toggle antes de la etiqueta, ícono después |
| `right` | Toggle después de la etiqueta, ícono antes |

## Ejemplos de uso

```html
<!-- Básico -->
<cns-switch
  id="switch-1"
  labelText="Notificaciones"
  variant="base"
  status="off"
></cns-switch>

<!-- Con helper text -->
<cns-switch
  id="switch-2"
  labelText="Modo oscuro"
  variant="base"
  status="on"
  showHelperText
  helperText="Activa el tema oscuro en la aplicación"
></cns-switch>

<!-- Variante box -->
<cns-switch
  id="switch-3"
  labelText="Recibir correos"
  variant="box"
  status="off"
  showHelperText
  helperText="Te enviaremos novedades semanales"
></cns-switch>

<!-- Variante blank -->
<cns-switch
  id="switch-4"
  labelText="Opción simple"
  variant="blank"
  status="off"
></cns-switch>

<!-- Control a la derecha -->
<cns-switch
  id="switch-5"
  labelText="Toggle a la derecha"
  variant="base"
  status="off"
  controlDirection="right"
></cns-switch>

<!-- Full width -->
<cns-switch
  id="switch-6"
  labelText="Ancho completo"
  variant="box"
  status="off"
  isFullWidth
  showHelperText
  helperText="Se expande al 100% del contenedor"
></cns-switch>

<!-- Con ícono -->
<cns-switch
  id="switch-7"
  labelText="Con ícono"
  variant="base"
  status="on"
  showIcon
  icon="<svg>...</svg>"
></cns-switch>

<!-- Disabled -->
<cns-switch
  id="switch-8"
  labelText="No disponible"
  variant="base"
  status="off"
  disabled
></cns-switch>
```
