---
inclusion: manual
---
# UI Kit V6 (Prisma) - Selector

**Versión**: 6.2.0
**Paquete**: `@ui-kit/selector-v6`

Selector (dropdown/picker) permite a los usuarios elegir entre una lista de opciones en un espacio limitado.

## Instalación

```bash
npm install @ui-kit/selector-v6
```

Registro global en `main.ts`:

```typescript
import { registerSelector } from '@ui-kit/selector-v6'
registerSelector()
```

O desde la librería global:

```typescript
import { CnsSelector } from '@ui-kit/components-v6';
CnsSelector();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `label` | string | - | Etiqueta que describe el campo |
| `placeholder` | string | - | Texto cuando no hay selección |
| `labelerror` | string | - | Mensaje de validación o error |
| `disabled` | boolean | - | Deshabilita el componente |
| `readonly` | boolean | - | Solo lectura |
| `fullwidth` | boolean | - | Ocupa el ancho completo del contenedor |
| `searchable` | boolean | - | Permite búsqueda por texto |
| `isrequired` | boolean | - | Campo obligatorio (muestra "requerido") |
| `optional` | boolean | - | Campo opcional (muestra "opcional") |
| `optionaltext` | string | - | Texto personalizado para opcional/requerido |
| `optionellipsis` | boolean | - | Corta texto de opciones que excede el espacio |
| `showtooltip` | boolean | - | Muestra ícono de tooltip |
| `tooltiptext` | string | - | Texto del tooltip |
| `size` | string | - | Altura en px: `40`, `48`, `56` |
| `state` | string | - | Estado visual: `error`, `success` |
| `type` | string | - | Tipo de ítem en la lista: `text`, `logo`, `icon`, `checkbox` |
| `value` | string | - | Valor actualmente seleccionado |
| `values` | string | - | Lista de objetos con clave y valor para las opciones |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `input` | Se emite al seleccionar una opción o cambiar la selección |
| `update:modelValue` | Compatible con v-model |

## Tipos de ítems (type)

| Type | Descripción |
|------|-------------|
| `text` | Opciones de texto simples |
| `logo` | Opciones con logo/imagen |
| `icon` | Opciones con ícono SVG |
| `checkbox` | Opciones con checkbox (selección múltiple) |

## Tamaños

| Size | Descripción |
|------|-------------|
| `40` | Compacto |
| `48` | Intermedio |
| `56` | Destacado |

## Variante sin búsqueda (searchable=false)

Deshabilita el comportamiento de búsqueda. Funciona solo como listado de selección. Recomendado cuando:
- El conjunto de opciones es acotado
- No se requiere filtrado
- Se desea comportamiento más controlado

## Ejemplos de uso

```html
<!-- Básico con opciones de texto -->
<cns-selector
  id="selector-1"
  label="Selecciona una opción"
  placeholder="Elige..."
  type="text"
  :values='[{"key":"1","value":"Opción 1"},{"key":"2","value":"Opción 2"},{"key":"3","value":"Opción 3"}]'
></cns-selector>

<!-- Requerido -->
<cns-selector
  id="selector-2"
  label="Campo requerido"
  placeholder="Selecciona"
  type="text"
  isrequired
  :values='[{"key":"a","value":"Valor A"},{"key":"b","value":"Valor B"}]'
></cns-selector>

<!-- Con logos -->
<cns-selector
  id="selector-3"
  label="Banco"
  placeholder="Selecciona un banco"
  type="logo"
  :values='[{"key":"1","value":"Banco 1","logo":"url-logo.png"}]'
></cns-selector>

<!-- Con íconos -->
<cns-selector
  id="selector-4"
  label="Categoría"
  placeholder="Selecciona"
  type="icon"
  :values='[{"key":"1","value":"Categoría 1","icon":"<svg>...</svg>"}]'
></cns-selector>

<!-- Con checkbox (selección múltiple) -->
<cns-selector
  id="selector-5"
  label="Intereses"
  placeholder="Selecciona varios"
  type="checkbox"
  :values='[{"key":"1","value":"Deporte"},{"key":"2","value":"Música"},{"key":"3","value":"Lectura"}]'
></cns-selector>

<!-- Estado error -->
<cns-selector
  id="selector-6"
  label="Con error"
  placeholder="Selecciona"
  type="text"
  state="error"
  labelerror="Debes seleccionar una opción"
  :values='[{"key":"1","value":"Opción 1"}]'
></cns-selector>

<!-- Estado success -->
<cns-selector
  id="selector-7"
  label="Validado"
  placeholder="Selecciona"
  type="text"
  state="success"
  :values='[{"key":"1","value":"Opción 1"}]'
></cns-selector>

<!-- Sin búsqueda -->
<cns-selector
  id="selector-8"
  label="Sin buscador"
  placeholder="Selecciona"
  type="text"
  :searchable="false"
  :values='[{"key":"1","value":"Opción 1"},{"key":"2","value":"Opción 2"}]'
></cns-selector>

<!-- Disabled -->
<cns-selector
  id="selector-9"
  label="Deshabilitado"
  placeholder="No disponible"
  type="text"
  disabled
  :values='[{"key":"1","value":"Opción 1"}]'
></cns-selector>

<!-- Readonly -->
<cns-selector
  id="selector-10"
  label="Solo lectura"
  type="text"
  readonly
  value="2"
  :values='[{"key":"1","value":"Opción 1"},{"key":"2","value":"Opción 2"}]'
></cns-selector>

<!-- Tamaño 40 -->
<cns-selector
  id="selector-11"
  label="Compacto"
  placeholder="Selecciona"
  type="text"
  size="40"
  :values='[{"key":"1","value":"Opción 1"}]'
></cns-selector>
```
