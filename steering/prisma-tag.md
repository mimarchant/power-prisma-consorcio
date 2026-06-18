---
inclusion: manual
---
# UI Kit V6 (Prisma) - Tag

**Versión**: 6.1.0
**Paquete**: `@ui-kit/tag-v6`

Tags se utilizan para etiquetar elementos, crear categorizaciones, filtrar datos, seleccionar/deseleccionar opciones y mostrar etiquetas relacionadas.

## Instalación

```bash
npm install @ui-kit/tag-v6
```

Registro global en `main.ts`:

```typescript
import { registerTag } from '@ui-kit/tag-v6'
registerTag()
```

O desde la librería global:

```typescript
import { CnsTags } from '@ui-kit/components-v6';
CnsTags();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único del componente |
| `label` | string | - | Texto principal que se muestra en el tag |
| `dcto` | string | - | Texto opcional para mostrar un descuento |
| `variant` | string | - | Estilo visual: `readonly`, `primary`, `secondary` |
| `color` | string | - | Color principal: `success`, `warning`, `critical`, `error`, `info`, `discovery`, `arena`, `calypso`, `morado`, `lima` |
| `size` | string | - | Tamaño del tag: `24`, `32` (solo variante readonly) |
| `disabled` | boolean | - | Desactiva el tag |
| `dot` | boolean | - | Muestra un punto en lugar del contenido completo (solo readonly) |

## Slots

| Slot | Descripción |
|------|-------------|
| `icon-left` | Ícono SVG inline a la izquierda |
| `icon-right` | Ícono SVG inline a la derecha |

## Variantes

### Readonly
- Uso: Etiquetas informativas, estados, indicadores
- Soporta íconos: **uno solo** (izquierda O derecha, no ambos)
- Soporta `size` (24 o 32)
- Soporta `dot`
- Soporta `disabled`

### Primary
- Uso: Acción menos importante para avanzar en un flujo
- Soporta íconos: **solo izquierda**
- NO soporta `size`, `dot`

### Secondary
- Uso: Acción complementaria
- Soporta `dcto` (texto de descuento)
- NO permite íconos
- NO soporta `size`, `dot`

## Reglas de íconos por variante

| Variante | icon-left | icon-right | Ambos |
|----------|-----------|-----------|-------|
| readonly | ✅ | ✅ | ❌ (solo uno) |
| primary | ✅ | ❌ | ❌ |
| secondary | ❌ | ❌ | ❌ |

## Atributo `size` (solo readonly)

- `size="32"`: Espaciado mayor, más presencia visual
- `size="24"`: Más compacto, interfaces densas

Solo cambia el padding, no el tamaño del texto. No aplica en primary ni secondary.

## Atributo `dot` (solo readonly)

- Muestra un punto de color a la izquierda del texto
- Reemplaza cualquier ícono (ignora icon-left/icon-right)
- No aplica en primary ni secondary

## Ejemplos de uso

```html
<!-- Readonly básico -->
<cns-tag variant="readonly" color="success" label="Activo"></cns-tag>

<!-- Readonly con tamaño -->
<cns-tag variant="readonly" color="info" label="Info" size="32"></cns-tag>

<!-- Readonly con dot -->
<cns-tag variant="readonly" color="warning" label="Pendiente" dot></cns-tag>

<!-- Primary con ícono izquierdo -->
<cns-tag variant="primary" color="arena" label="Arena">
  <svg slot="icon-left">...</svg>
</cns-tag>

<!-- Secondary con descuento -->
<cns-tag variant="secondary" color="success" label="Label" dcto="20% dcto."></cns-tag>

<!-- Disabled -->
<cns-tag variant="readonly" color="success" label="Label" disabled></cns-tag>
```
