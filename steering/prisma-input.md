---
inclusion: manual
---
# UI Kit V6 (Prisma) - Input

**Versión**: 6.1.0
**Paquete**: `@ui-kit/input-v6`

Input permite ingresar datos de manera sencilla y personalizable.

## Instalación

```bash
npm install @ui-kit/input-v6
```

Registro global en `main.ts`:

```typescript
import { registerInput } from '@ui-kit/input-v6'
registerInput()
```

O desde la librería global:

```typescript
import { CnsInput } from '@ui-kit/components-v6';
CnsInput();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `label` | string | - | Etiqueta que describe el campo |
| `helper` | string | - | Texto de ayuda bajo el input |
| `validation` | string | - | Mensaje de validación o error |
| `placeholder` | string | - | Texto cuando no hay valor ingresado |
| `required` | boolean | - | Campo obligatorio (muestra "requerido") |
| `disabled` | boolean | - | Deshabilita el componente |
| `readonly` | boolean | - | Solo lectura, sin edición |
| `size` | string | - | Altura en px: `40`, `48`, `56` |
| `state` | string | - | Estado visual del input |
| `prefix` | string | - | Texto/símbolo antes del valor |
| `suffix` | string | - | Texto/símbolo después del valor |
| `iconleft` | string | - | Ícono SVG a la izquierda |
| `iconright` | string | - | Ícono SVG a la derecha |
| `type` | string | - | Tipo de input: `text`, `password`, `number`, `email`, `phone`, `rut`, `miles`, `date`, `time` |
| `value` | any | - | Valor actualmente ingresado |
| `showTooltip` | boolean | - | Muestra ícono de tooltip |
| `optional` | boolean | - | Campo opcional (muestra "opcional") |
| `optionalText` | string | - | Texto personalizado para opcional/requerido |
| `maxlength` | number | - | Máximo de caracteres permitidos |
| `minlength` | number | - | Mínimo de caracteres requeridos |
| `max` | any | - | Valor máximo (numéricos o fecha) |
| `min` | any | - | Valor mínimo (numéricos o fecha) |
| `error` | boolean | - | Aplica estilos de error |
| `success` | boolean | - | Aplica estilos de éxito |
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `name` | string | - | Nombre del campo en formularios |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `input` | Se emite cada vez que el valor cambia |
| `focus` | Se emite cuando el input recibe foco |
| `blur` | Se emite cuando el input pierde foco |
| `change` | Se emite cuando el valor cambia y pierde foco |
| `update:value` | Compatible con v-model |
| `update:modelValue` | Compatible con v-model |

## Tipos especiales

| Type | Comportamiento |
|------|---------------|
| `text` | Input de texto estándar |
| `password` | Oculta caracteres, ícono para mostrar/ocultar |
| `number` | Solo números |
| `email` | Formato de correo |
| `phone` | Formato de teléfono |
| `rut` | Formato RUT chileno con validación |
| `miles` | Formato numérico con separador de miles |
| `date` | Selector de fecha |
| `time` | Selector de hora |

## Tamaños

| Size | Descripción |
|------|-------------|
| `40` | Compacto |
| `48` | Intermedio |
| `56` | Destacado |

## Ejemplos de uso

```html
<!-- Básico con label y helper -->
<cns-input
  id="nombre"
  label="Nombre"
  helper="Ingresa tu nombre completo"
  placeholder="Ej: Juan Pérez"
  type="text"
></cns-input>

<!-- Requerido -->
<cns-input
  id="email"
  label="Correo electrónico"
  type="email"
  required
  placeholder="correo@ejemplo.cl"
></cns-input>

<!-- Con prefix y suffix -->
<cns-input
  id="monto"
  label="Monto"
  type="miles"
  prefix="$"
  suffix="CLP"
></cns-input>

<!-- RUT -->
<cns-input
  id="rut"
  label="RUT"
  type="rut"
  helper="Ingresa tu RUT sin puntos ni guión"
></cns-input>

<!-- Password -->
<cns-input
  id="password"
  label="Contraseña"
  type="password"
  placeholder="Ingresa tu contraseña"
></cns-input>

<!-- Con error -->
<cns-input
  id="campo-error"
  label="Campo con error"
  type="text"
  error
  validation="Este campo es obligatorio"
></cns-input>

<!-- Con success -->
<cns-input
  id="campo-success"
  label="Campo válido"
  type="text"
  success
  validation="Datos guardados correctamente"
></cns-input>

<!-- Date -->
<cns-input
  id="fecha"
  label="Fecha de nacimiento"
  type="date"
  helper="Selecciona tu fecha"
></cns-input>

<!-- Time -->
<cns-input
  id="hora"
  label="Hora"
  type="time"
></cns-input>

<!-- Phone -->
<cns-input
  id="telefono"
  label="Teléfono"
  type="phone"
  helper="Ingresa tu número"
></cns-input>

<!-- Tamaño 40 -->
<cns-input
  id="compact"
  label="Compacto"
  type="text"
  size="40"
></cns-input>

<!-- Disabled -->
<cns-input
  id="disabled"
  label="Deshabilitado"
  type="text"
  disabled
></cns-input>

<!-- Readonly -->
<cns-input
  id="readonly"
  label="Solo lectura"
  type="text"
  readonly
  value="Valor fijo"
></cns-input>
```
