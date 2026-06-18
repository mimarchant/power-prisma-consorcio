---
inclusion: manual
---
# UI Kit V6 (Prisma) - TextArea

**Versión**: 6.1.0
**Paquete**: `@ui-kit/textarea-v6`

TextArea permite a los usuarios introducir texto en múltiples líneas.

## Instalación

```bash
npm install @ui-kit/textarea-v6
```

Registro global en `main.ts`:

```typescript
import { registerTextArea } from '@ui-kit/textarea-v6'
registerTextArea()
```

O desde la librería global:

```typescript
import { CnsTextArea } from '@ui-kit/components-v6';
CnsTextArea();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `label` | string | - | Etiqueta del campo |
| `helperText` | string | - | Texto de ayuda debajo del campo |
| `placeholder` | string | - | Texto cuando el campo está vacío |
| `value` | string | - | Valor actual del campo |
| `isRequired` | boolean | - | Campo obligatorio |
| `validationText` | string | - | Mensaje de error o validación |
| `color` | string | - | Estado visual: `success`, `error` |
| `maxLength` | number | - | Máximo de caracteres permitidos |
| `showTooltip` | boolean | - | Muestra ícono de ayuda |
| `optionalLabel` | string | - | Indica si el campo es opcional |
| `disabled` | boolean | - | Inhabilita la interacción |
| `readonly` | boolean | - | Solo lectura |
| `resize` | boolean | - | Permite redimensionar manualmente |
| `characterCounter` | boolean | - | Muestra contador de caracteres |
| `rows` | number | - | Número de líneas visibles por defecto |
| `size` | string | - | Tamaño visual: `20`, `52` |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `focus` | Se emite cuando el campo recibe foco |
| `blur` | Se emite cuando el campo pierde foco |
| `input` | Se emite cada vez que el valor cambia (v-model) |
| `change` | Se emite cuando el valor cambia y pierde foco |
| `update:value` | Compatible con v-model |
| `update:modelValue` | Compatible con v-model |
| `cnsClickHelp` | Se emite al hacer clic en el ícono de ayuda |

## Tamaños

| Size | Descripción |
|------|-------------|
| `20` | Compacto (menos líneas visibles) |
| `52` | Amplio (más líneas visibles) |

## Ejemplos de uso

```html
<!-- Básico con helper y contador -->
<cns-textarea
  id="comentario"
  label="Comentario"
  helperText="Máximo 500 caracteres"
  placeholder="Escribe tu comentario..."
  :maxLength="500"
  characterCounter
></cns-textarea>

<!-- Requerido -->
<cns-textarea
  id="descripcion"
  label="Descripción"
  placeholder="Describe tu solicitud"
  isRequired
></cns-textarea>

<!-- Tamaño 20 (compacto) -->
<cns-textarea
  id="nota"
  label="Nota breve"
  helperText="Texto corto"
  size="20"
  placeholder="Escribe aquí..."
></cns-textarea>

<!-- Tamaño 52 (amplio) -->
<cns-textarea
  id="detalle"
  label="Detalle extenso"
  helperText="Describe en detalle"
  size="52"
  placeholder="Escribe aquí..."
></cns-textarea>

<!-- Estado success -->
<cns-textarea
  id="exito"
  label="Guardado"
  color="success"
  validationText="Texto guardado correctamente"
  value="Contenido validado"
></cns-textarea>

<!-- Estado error -->
<cns-textarea
  id="error"
  label="Con error"
  color="error"
  validationText="Este campo es obligatorio"
></cns-textarea>

<!-- Disabled -->
<cns-textarea
  id="disabled"
  label="Deshabilitado"
  helperText="No disponible"
  disabled
></cns-textarea>

<!-- Readonly -->
<cns-textarea
  id="readonly"
  label="Solo lectura"
  helperText="No editable"
  readonly
  value="Contenido fijo que no se puede modificar"
></cns-textarea>

<!-- Con resize habilitado -->
<cns-textarea
  id="resizable"
  label="Redimensionable"
  placeholder="Arrastra para agrandar"
  resize
></cns-textarea>
```
