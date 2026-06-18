---
inclusion: manual
---
# UI Kit V6 (Prisma) - SegmentedInput

**Versión**: 6.2.0
**Paquete**: `@ui-kit/segmentedinput-v6`

Permite ingresar datos alfanuméricos en campos segmentados. Cada campo acepta una parte del código y el foco se desplaza automáticamente al siguiente segmento al completar el actual. Ideal para flujos de registro, control de acceso o validación de vehículos.

## Instalación

```bash
npm install @ui-kit/segmentedinput-v6
```

Registro global en `main.ts`:

```typescript
import { registerSegmentedInput } from '@ui-kit/segmentedinput-v6'
registerSegmentedInput()
```

O desde la librería global:

```typescript
import { CnsSegmentedInput } from '@ui-kit/components-v6';
CnsSegmentedInput();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | `cns-segmentedinput` | Identificador único |
| `size` | number | `48` | Tamaño: `40`, `48`, `56` |
| `state` | string | `default` | Estado: `default`, `success`, `error` |
| `digits` | number | `4` | Número de inputs: `4`, `6` |
| `inputType` | string | `text` | Tipo de input: `text`, `number` |
| `showLabelText` | boolean | true | Muestra/oculta el label |
| `labelText` | string | `""` | Etiqueta del componente |
| `showHelperText` | boolean | true | Muestra/oculta el helper text |
| `helperText` | string | `""` | Texto de ayuda |
| `showValidation` | boolean | false | Muestra/oculta texto de validación |
| `validation` | string | `""` | Texto de validación |
| `showIndicator` | boolean | true | Muestra/oculta indicador opcional/requerido |
| `labelType` | string | `optional` | Tipo de label: `required`, `optional` |
| `showTooltip` | boolean | true | Muestra/oculta tooltip |
| `showInputVisible` | boolean | true | Muestra caracteres visibles (false = modo password) |
| `showIconVisible` | boolean | true | Muestra/oculta botón de alternar visibilidad |
| `disabled` | boolean | false | Deshabilita el componente |

### Props de accesibilidad

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `cnsAriaLabel` | string | - | Etiqueta accesible para el grupo |
| `cnsAriaDescription` | string | - | Descripción accesible adicional |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `change` | Se emite cuando el valor cambia |
| `complete` | Se emite cuando se completan todos los inputs |

## Comportamiento

- **Flujo secuencial**: Solo se puede interactuar hasta la casilla activa. Las posteriores quedan bloqueadas
- **Autoavance**: Al ingresar un carácter válido, avanza automáticamente a la siguiente casilla
- **ArrowLeft/ArrowRight**: Navega entre casillas (nunca más allá de la activa)
- **Backspace**: Borra contenido de casilla actual. Si está vacía, retrocede y borra la anterior
- **Paste**: Sanitiza texto (sin espacios; solo dígitos si es numérico) y lo distribuye desde la casilla enfocada
- **Visibilidad (eye)**: Alterna mostrar/ocultar contenido

## Tamaños

| Size | Descripción |
|------|-------------|
| `40` | Compacto |
| `48` | Estándar (recomendado) |
| `56` | Mayor presencia visual, mejor accesibilidad táctil |

## Tipos de input

| Type | Descripción |
|------|-------------|
| `text` | Alfanumérico (letras y números) |
| `number` | Solo numérico (sanitiza al pegar) |

## Ejemplos de uso

```html
<!-- Básico 4 dígitos -->
<cns-segmentedinput
  id="code-1"
  :digits="4"
  inputType="number"
  labelText="Código de verificación"
  helperText="Ingresa el código enviado a tu correo"
></cns-segmentedinput>

<!-- 6 dígitos alfanumérico -->
<cns-segmentedinput
  id="code-2"
  :digits="6"
  inputType="text"
  labelText="Código de activación"
  helperText="Código enviado por SMS"
></cns-segmentedinput>

<!-- Con estado error -->
<cns-segmentedinput
  id="code-3"
  :digits="4"
  inputType="number"
  state="error"
  :showValidation="true"
  validation="Código incorrecto, intenta nuevamente"
  labelText="Código"
  helperText="Ingresa tu código"
></cns-segmentedinput>

<!-- Con estado success -->
<cns-segmentedinput
  id="code-4"
  :digits="4"
  inputType="number"
  state="success"
  :showValidation="true"
  validation="Código verificado correctamente"
  labelText="Código"
  helperText="Ingresa tu código"
></cns-segmentedinput>

<!-- Modo password (oculto por defecto) -->
<cns-segmentedinput
  id="code-5"
  :digits="4"
  inputType="number"
  :showInputVisible="false"
  labelText="PIN"
  helperText="Ingresa tu PIN de seguridad"
></cns-segmentedinput>

<!-- Sin botón de visibilidad -->
<cns-segmentedinput
  id="code-6"
  :digits="4"
  inputType="number"
  :showIconVisible="false"
  labelText="Código secreto"
  helperText="No se puede alternar visibilidad"
></cns-segmentedinput>

<!-- Disabled -->
<cns-segmentedinput
  id="code-7"
  :digits="4"
  inputType="number"
  disabled
  labelText="Deshabilitado"
  helperText="No disponible"
></cns-segmentedinput>

<!-- Tamaño 56 -->
<cns-segmentedinput
  id="code-8"
  :digits="4"
  :size="56"
  inputType="number"
  labelText="Código grande"
  helperText="Más fácil de interactuar en móvil"
></cns-segmentedinput>

<!-- Requerido -->
<cns-segmentedinput
  id="code-9"
  :digits="4"
  inputType="number"
  labelType="required"
  labelText="Código"
  helperText="Este campo es obligatorio"
></cns-segmentedinput>
```

## Patrón de uso con eventos (Vue 3)

```vue
<template>
  <cns-segmentedinput
    id="otp"
    :digits="6"
    inputType="number"
    labelText="Código OTP"
    helperText="Ingresa el código de 6 dígitos"
    @change="onCodeChange"
    @complete="onCodeComplete"
  ></cns-segmentedinput>
</template>

<script setup>
const onCodeChange = (event) => {
  console.log('Valor parcial:', event.detail)
}

const onCodeComplete = (event) => {
  console.log('Código completo:', event.detail)
  // Validar código con API
}
</script>
```
