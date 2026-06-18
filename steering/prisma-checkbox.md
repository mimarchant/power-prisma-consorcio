---
inclusion: manual
---
# UI Kit V6 (Prisma) - Checkbox

**Versión**: 6.2.0
**Paquete**: `@ui-kit/checkbox-v6`

Checkbox permite a los usuarios seleccionar una o varias opciones.

## Instalación

```bash
npm install @ui-kit/checkbox-v6
```

Registro global en `main.ts`:

```typescript
import { registerCheckbox } from '@ui-kit/checkbox-v6'
registerCheckbox()
```

O desde la librería global:

```typescript
import { CnsCheckbox } from '@ui-kit/components-v6';
CnsCheckbox();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `active` | boolean | - | Estado activo por defecto |
| `controldirection` | string | - | Posición del check: `left`, `right` |
| `disabled` | boolean | - | Desactiva la interacción |
| `errormsg` | string | - | Texto de error que se muestra bajo el checkbox |
| `helpermsg` | string | - | Texto de ayuda que se muestra bajo el checkbox |
| `icon` | string | - | Ícono SVG cuando `showicon` está activado |
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `indeterminate` | boolean | - | Estado indeterminado (línea horizontal) |
| `isfullwidth` | boolean | - | Toma el 100% del ancho del contenedor |
| `labeltext` | string | - | Texto visible asociado al checkbox |
| `showerror` | boolean | - | Muestra/oculta el mensaje de error |
| `showhelpertext` | boolean | - | Muestra/oculta el texto de ayuda |
| `showicon` | boolean | - | Muestra ícono decorativo cuando está activo |
| `type` | string | - | Estilo visual: `base`, `blank`, `box` |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `initialstate` | Se emite al montar, informando el valor inicial |
| `input` | Se emite cada vez que el usuario cambia el valor |
| `update:indeterminate` | Se emite cuando cambia el estado indeterminado |
| `update:modelvalue` | Se emite al cambiar el valor (compatible con v-model) |

## Variantes (type)

| Tipo | Descripción |
|------|-------------|
| `base` | Checkbox estándar con borde y fondo |
| `blank` | Checkbox sin fondo decorativo |
| `box` | Checkbox con contenedor tipo tarjeta |

## Consideraciones

- `controldirection`: Posiciona el cuadro del checkbox a la izquierda o derecha del texto
- `isfullwidth`: Ajusta el componente al 100% del ancho del contenedor padre
- **Estado de error**: Se activa cuando `showerror=true` y el checkbox no está activo. El borde se muestra en color `#EA6161` y se muestra el `errormsg` si existe
- **Accesibilidad**: Soporta enfoque visible y estados deshabilitados
- **Ícono decorativo**: Activar `showicon` y definir SVG con `icon`
- **Indeterminate**: Estado visual intermedio (línea horizontal), útil para checkboxes padre

## Ejemplos de uso

```html
<!-- Básico -->
<cns-checkbox
  id="check-1"
  labeltext="Acepto los términos"
  type="base"
></cns-checkbox>

<!-- Activo por defecto -->
<cns-checkbox
  id="check-2"
  labeltext="Opción seleccionada"
  type="base"
  active
></cns-checkbox>

<!-- Con error -->
<cns-checkbox
  id="check-3"
  labeltext="Campo requerido"
  type="base"
  showerror
  errormsg="Debes aceptar para continuar"
></cns-checkbox>

<!-- Control a la derecha -->
<cns-checkbox
  id="check-4"
  labeltext="Control a la derecha"
  type="base"
  controldirection="right"
></cns-checkbox>

<!-- Fullwidth -->
<cns-checkbox
  id="check-5"
  labeltext="Ancho completo"
  type="box"
  isfullwidth
></cns-checkbox>

<!-- Indeterminado -->
<cns-checkbox
  id="check-6"
  labeltext="Seleccionar todo"
  type="base"
  indeterminate
></cns-checkbox>

<!-- Con ícono -->
<cns-checkbox
  id="check-7"
  labeltext="Con ícono"
  type="base"
  showicon
  icon="<svg>...</svg>"
></cns-checkbox>

<!-- Disabled -->
<cns-checkbox
  id="check-8"
  labeltext="No disponible"
  type="base"
  disabled
></cns-checkbox>

<!-- Con helper text -->
<cns-checkbox
  id="check-9"
  labeltext="Suscribirse"
  type="base"
  showhelpertext
  helpermsg="Recibirás noticias semanales"
></cns-checkbox>
```
