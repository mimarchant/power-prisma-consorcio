---
inclusion: manual
---
# UI Kit V6 (Prisma) - LinkCard

**Versión**: 6.1.0
**Paquete**: `@ui-kit/linkcard-v6`

Elementos interactivos que combinan el diseño de una tarjeta con la funcionalidad de un enlace. Redirige al usuario al hacer clic en cualquier parte de la tarjeta.

## Instalación

```bash
npm install @ui-kit/linkcard-v6
```

Registro global en `main.ts`:

```typescript
import { registerLinkCard } from '@ui-kit/linkcard-v6'
registerLinkCard()
```

O desde la librería global:

```typescript
import { CnsLinkCard } from '@ui-kit/components-v6';
CnsLinkCard();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | `cns-linkcard` | Identificador único |
| `alignment` | string | `horizontalCenter` | Layout: `horizontalCenter`, `verticalLeft`, `verticalCenter` |
| `title` | string | - | Título principal |
| `description` | string | - | Descripción secundaria |
| `showDescription` | boolean | true | Muestra/oculta la descripción |
| `showIconSemantic` | boolean | false | Muestra ícono a la izquierda |
| `showIconAction` | boolean | true | Muestra ícono a la derecha |
| `iconBg` | boolean | false | Fondo coloreado para el ícono semántico |
| `animated` | boolean | false | Animación del ícono de acción en hover |
| `disabled` | boolean | false | Deshabilita la tarjeta |

### Props de enlace

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `cnsHref` | string | - | URL de destino |
| `cnsTarget` | string | `_self` | Dónde se abre: `_self`, `_blank`, `_parent`, `_top` |
| `cnsRel` | string | - | Relación entre documentos |

### Props de accesibilidad

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `cnsAriaLabel` | string | - | Etiqueta accesible personalizada |
| `cnsAriaDescription` | string | - | Descripción accesible adicional |

## Slots

| Slot | Descripción |
|------|-------------|
| `iconSemantic` | Ícono SVG a la izquierda del título |
| `iconAction` | Ícono SVG a la derecha del título |

## Variantes de layout (alignment)

### horizontalCenter (default)
- Contenido en una fila, centrado verticalmente
- Ícono semántico a la izquierda, texto al centro, ícono de acción a la derecha

### verticalLeft
- Contenido apilado en columna, alineado a la izquierda
- Ícono semántico arriba, texto debajo, ícono de acción a la derecha

### verticalCenter
- Contenido apilado en columna, centrado horizontalmente
- Ícono semántico arriba, texto centrado debajo
- **No renderiza ícono de acción**

## Comportamiento

- **Disabled**: No navega, quita href/target/rel, no se activa con teclado, click anulado. Expone `aria-disabled="true"`
- **Animated**: Animación sutil en hover del ícono de acción. No aplica si disabled, si showIconAction=false, o en verticalCenter
- **iconBg**: Solo tiene efecto si el ícono semántico es visible
- **Ancho por defecto**: 317px. Se puede personalizar con CSS inline (`style="width: 500px;"`)

## Seguridad en enlaces

- Preferir HTTPS
- Con `target="_blank"`, agregar siempre `rel="noopener noreferrer"`
- Validar/sanitizar valores dinámicos en `cnsHref`

## Ejemplos de uso

```html
<!-- Horizontal center (default) -->
<cns-linkcard
  id="card-1"
  title="Mi cuenta"
  description="Administra tu perfil y preferencias"
  cnsHref="/mi-cuenta"
>
  <svg slot="iconSemantic">...</svg>
  <svg slot="iconAction">...</svg>
</cns-linkcard>

<!-- Vertical left -->
<cns-linkcard
  id="card-2"
  alignment="verticalLeft"
  title="Seguros"
  description="Conoce nuestros planes de protección"
  cnsHref="https://sitio.consorcio.cl/seguros"
  cnsTarget="_blank"
  cnsRel="noopener noreferrer"
  showIconSemantic
>
  <svg slot="iconSemantic">...</svg>
</cns-linkcard>

<!-- Vertical center (sin ícono de acción) -->
<cns-linkcard
  id="card-3"
  alignment="verticalCenter"
  title="Inversiones"
  description="Haz crecer tu patrimonio"
  cnsHref="/inversiones"
  showIconSemantic
  iconBg
>
  <svg slot="iconSemantic">...</svg>
</cns-linkcard>

<!-- Sin descripción -->
<cns-linkcard
  id="card-4"
  title="Ver más"
  :showDescription="false"
  cnsHref="/detalle"
></cns-linkcard>

<!-- Con animación -->
<cns-linkcard
  id="card-5"
  title="Ofertas"
  description="Descubre las últimas promociones"
  cnsHref="/ofertas"
  animated
></cns-linkcard>

<!-- Con fondo en ícono -->
<cns-linkcard
  id="card-6"
  title="Ayuda"
  description="Centro de soporte"
  cnsHref="/ayuda"
  showIconSemantic
  iconBg
>
  <svg slot="iconSemantic">...</svg>
</cns-linkcard>

<!-- Disabled -->
<cns-linkcard
  id="card-7"
  title="No disponible"
  description="Este servicio está temporalmente suspendido"
  disabled
></cns-linkcard>

<!-- Ancho personalizado -->
<cns-linkcard
  id="card-8"
  title="Card ancha"
  description="Con ancho personalizado"
  cnsHref="/ejemplo"
  style="width: 500px;"
></cns-linkcard>
```
