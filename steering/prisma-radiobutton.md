---
inclusion: manual
---
# UI Kit V6 (Prisma) - RadioButton

**Versión**: 6.1.0
**Paquete**: `@ui-kit/radiobutton-v6`

RadioButton permite a los usuarios seleccionar una opción de un grupo de opciones mutuamente exclusivas.

## Instalación

```bash
npm install @ui-kit/radiobutton-v6
```

Registro global en `main.ts`:

```typescript
import { registerRadiobutton } from '@ui-kit/radiobutton-v6'
registerRadiobutton()
```

O desde la librería global:

```typescript
import { CnsRadiobutton } from '@ui-kit/components-v6';
CnsRadiobutton();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `controldirection` | string | - | Posición del control: `left`, `right` |
| `disabled` | boolean | - | Desactiva la interacción |
| `errormsg` | string | - | Texto de error bajo el radio button |
| `helpermsg` | string | - | Texto de ayuda bajo el radio button |
| `group` | string | - | Nombre del grupo para vincular múltiples radio buttons |
| `id` | string | - | Identificador único (accesibilidad y testing) |
| `icon` | string | - | Ícono SVG cuando `showicon` está activado |
| `isfullwidth` | boolean | - | Toma el 100% del ancho del contenedor |
| `label` | string | - | Texto visible asociado al radio button |
| `showerror` | boolean | - | Muestra/oculta el mensaje de error |
| `showhelpertext` | boolean | - | Muestra/oculta el texto de ayuda |
| `showicon` | boolean | - | Muestra ícono decorativo cuando está activo |
| `type` | string | - | Estilo visual: `base`, `blank`, `box` |
| `value` | string | - | Valor asociado dentro del grupo |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `input` | Se emite cada vez que el usuario selecciona el radio button |
| `selected` | Se emite al seleccionar (compatible con v-model) |

## Variantes (type)

| Tipo | Descripción |
|------|-------------|
| `base` | Radio button estándar con borde |
| `blank` | Radio button sin fondo decorativo |
| `box` | Radio button con contenedor tipo tarjeta |

## Consideraciones

- `controldirection`: Posiciona el círculo del radio a la izquierda o derecha del texto
- `isfullwidth`: Ajusta el componente al 100% del ancho del contenedor padre
- `group`: Vincular múltiples radio buttons con el mismo `group` los hace mutuamente exclusivos
- **Estado de error**: Se activa cuando `showerror=true` y el radio no está seleccionado. Borde en `#EA6161` y muestra `errormsg`
- **Accesibilidad**: Soporta enfoque visible y estados deshabilitados
- **Ícono decorativo**: Activar `showicon` y definir SVG con `icon`

## Ejemplos de uso

```html
<!-- Básico -->
<cns-radiobutton
  id="radio-1"
  label="Opción A"
  group="grupo1"
  value="a"
  type="base"
></cns-radiobutton>

<!-- Grupo de opciones -->
<cns-radiobutton
  id="radio-hombre"
  label="Hombre"
  group="genero"
  value="hombre"
  type="base"
></cns-radiobutton>
<cns-radiobutton
  id="radio-mujer"
  label="Mujer"
  group="genero"
  value="mujer"
  type="base"
></cns-radiobutton>

<!-- Con error -->
<cns-radiobutton
  id="radio-2"
  label="Selecciona una opción"
  group="grupo2"
  value="x"
  type="base"
  showerror
  errormsg="Este campo es obligatorio"
></cns-radiobutton>

<!-- Control a la derecha -->
<cns-radiobutton
  id="radio-3"
  label="Control a la derecha"
  group="grupo3"
  value="b"
  type="base"
  controldirection="right"
></cns-radiobutton>

<!-- Fullwidth con variante box -->
<cns-radiobutton
  id="radio-4"
  label="Opción completa"
  group="grupo4"
  value="c"
  type="box"
  isfullwidth
></cns-radiobutton>

<!-- Con ícono -->
<cns-radiobutton
  id="radio-5"
  label="Con ícono"
  group="grupo5"
  value="d"
  type="base"
  showicon
  icon="<svg>...</svg>"
></cns-radiobutton>

<!-- Disabled -->
<cns-radiobutton
  id="radio-6"
  label="No disponible"
  group="grupo6"
  value="e"
  type="base"
  disabled
></cns-radiobutton>

<!-- Con helper text -->
<cns-radiobutton
  id="radio-7"
  label="Opción con ayuda"
  group="grupo7"
  value="f"
  type="base"
  showhelpertext
  helpermsg="Selecciona si aplica"
></cns-radiobutton>
```
