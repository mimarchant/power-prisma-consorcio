---
inclusion: manual
---
# UI Kit V6 (Prisma) - Alert

**Versión**: 6.1.0
**Paquete**: `@ui-kit/alert-v6`

Mensajes de alerta para comunicar estados e información al usuario. Existen dos tipos:
- **Section notice** (alert notice): Menor prioridad, comunica estado de una sección. Común en validación de formularios.
- **Page notice**: Alta prioridad a nivel de página. Llamativo y prominente.

## Instalación

```bash
npm install @ui-kit/alert-v6
```

Registro global en `main.ts`:

```typescript
import { registerAlert } from '@ui-kit/alert-v6'
registerAlert()
```

O desde la librería global:

```typescript
import { CnsAlert } from '@ui-kit/components-v6';
CnsAlert();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `variant` | string | - | Color semántico: `information`, `discovery`, `warning`, `critical`, `success`, `error` |
| `title` | string | - | Título del mensaje de alerta |
| `text` | string | - | Descripción del mensaje |
| `actionLinkTo` | string | - | Href del link complementario |
| `actionText` | string | - | Texto del link o botón complementario |
| `type` | string | - | Tipo de alerta: `section`, `page` |
| `actionType` | string | - | Para variante `page`: `link`, `button` |
| `showCloseButton` | boolean | - | Muestra/oculta botón de cerrar |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `close` | Se emite al cerrar el alert |

## Tipos

| Type | Descripción |
|------|-------------|
| `section` | Alerta de sección, menor prioridad. Ideal para validación de formularios |
| `page` | Alerta de página, alta prioridad. Prominente y llamativa |

## Variantes (colores semánticos)

| Variant | Uso |
|---------|-----|
| `information` | Información general |
| `discovery` | Novedad, exploración |
| `success` | Operación exitosa |
| `warning` | Advertencia, precaución |
| `critical` | Urgencia máxima |
| `error` | Error, fallo |

Los íconos de cada alerta **no se pueden personalizar** (están ligados al variant).

## Action type (solo para type="page")

| ActionType | Descripción |
|-----------|-------------|
| `link` | Muestra un enlace complementario |
| `button` | Muestra un botón complementario |

## Ejemplos de uso

```html
<!-- Section notice básico -->
<cns-alert
  id="alert-1"
  type="section"
  variant="information"
  title="Información"
  text="Tu solicitud fue recibida correctamente."
></cns-alert>

<!-- Section notice con link -->
<cns-alert
  id="alert-2"
  type="section"
  variant="success"
  title="Operación exitosa"
  text="Los datos fueron guardados."
  actionText="Ver detalle"
  actionLinkTo="/detalle"
></cns-alert>

<!-- Page notice con link -->
<cns-alert
  id="alert-3"
  type="page"
  variant="warning"
  title="Mantenimiento programado"
  text="El sistema estará en mantenimiento el próximo sábado."
  actionType="link"
  actionText="Más información"
  actionLinkTo="/mantenimiento"
  showCloseButton
></cns-alert>

<!-- Page notice con botón -->
<cns-alert
  id="alert-4"
  type="page"
  variant="critical"
  title="Sesión por expirar"
  text="Tu sesión expirará en 2 minutos."
  actionType="button"
  actionText="Extender sesión"
  showCloseButton
></cns-alert>

<!-- Error en formulario -->
<cns-alert
  id="alert-5"
  type="section"
  variant="error"
  title="Error en el formulario"
  text="Revisa los campos marcados en rojo."
></cns-alert>

<!-- Discovery -->
<cns-alert
  id="alert-6"
  type="section"
  variant="discovery"
  title="Nueva funcionalidad"
  text="Ahora puedes pagar con QR desde la app."
  actionText="Conocer más"
  actionLinkTo="/novedades"
></cns-alert>

<!-- Con botón de cerrar y evento -->
<cns-alert
  id="alert-7"
  type="page"
  variant="information"
  title="Aviso"
  text="Recuerda actualizar tus datos de contacto."
  showCloseButton
  @close="handleClose"
></cns-alert>
```
