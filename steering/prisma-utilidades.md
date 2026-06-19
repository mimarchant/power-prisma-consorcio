---
inclusion: manual
---
# UI Kit V6 (Prisma) - Utilidades

Requiere `@ui-kit/styles-v6`:

```bash
npm install @ui-kit/styles-v6
```

```typescript
import '@ui-kit/styles-v6/dist/style.css';
```

---

## Border Radius

Notación CSS: `.cns-border-radius-<scale>` o `var()` en estilos.

Escala basada en múltiplos de 8 (misma regla que spacing).

| Token CSS | Valor |
|-----------|-------|
| `cns-border-radius-0` | 0px |
| `cns-border-radius-4` | 4px |
| `cns-border-radius-8` | 8px |
| `cns-border-radius-16` | 16px |
| `cns-border-radius-full` | 9999px |

---

## Colors

### Estructura de nomenclatura

```
--cns-{familia}-{nombre}-{tono}
```

- **familia**: primary, complementary, neutral, semantic
- **nombre**: brand, marino, cielo, arena, calypso, lima, morado, success, error, etc.
- **tono**: 10 (más claro) a 100 (más oscuro), 00 para blanco puro en neutrales

### Primary Colors

#### Brand Azul
`--cns-primary-brand-10` a `--cns-primary-brand-100`

#### Marino
`--cns-primary-marino-10` a `--cns-primary-marino-100`

#### Cielo
`--cns-primary-cielo-10` a `--cns-primary-cielo-100`

### Complementary Colors

#### Arena
`--cns-complementary-arena-10` a `--cns-complementary-arena-100`

#### Calypso
`--cns-complementary-calypso-10` a `--cns-complementary-calypso-100`

#### Lima
`--cns-complementary-lima-10` a `--cns-complementary-lima-100`

#### Morado
`--cns-complementary-morado-10` a `--cns-complementary-morado-100`

### Neutral Colors
`--cns-neutral-00` a `--cns-neutral-90`

### Semantic Colors

| Color | Token base (tono 50) | Significado |
|-------|---------------------|-------------|
| Discovery | `--cns-semantic-discovery-50` | Novedad, exploración |
| Error | `--cns-semantic-error-50` | Error, acción destructiva |
| Success | `--cns-semantic-success-50` | Operación exitosa |
| Warning | `--cns-semantic-warning-50` | Advertencia, precaución |
| Info | `--cns-semantic-info-50` | Información neutral |
| Critical | `--cns-semantic-critical-50` | Urgencia máxima, irreversible |

Cada semántico tiene escala completa de 10 a 100.

### Clases utilitarias de color

Además de las variables CSS (`var(--cns-*)`), el UI Kit provee **clases directas** para aplicar
colores como texto o fondo sin necesidad de escribir CSS custom:

**Texto**: `.font-{nombre}-{tono}` → aplica `color`
**Fondo**: `.bg-{nombre}-{tono}` → aplica `background-color`

#### Primary

| Clase texto | Clase fondo | Color |
|-------------|-------------|-------|
| `.font-brand-10` | `.bg-brand-10` | #F2F5F7 |
| `.font-brand-20` | `.bg-brand-20` | #E6EAEE |
| `.font-brand-30` | `.bg-brand-30` | #D6DEE4 |
| `.font-brand-40` | `.bg-brand-40` | #B0BFCB |
| `.font-brand-50` | `.bg-brand-50` | #003058 (azul principal) |
| `.font-brand-60` | `.bg-brand-60` | #002B4F |
| `.font-brand-70` | `.bg-brand-70` | #002646 |
| `.font-brand-80` | `.bg-brand-80` | #001D35 |
| `.font-brand-90` | `.bg-brand-90` | #001628 |
| `.font-brand-100` | `.bg-brand-100` | #00111F |

Misma convención para `marino`, `cielo`, `arena`, `calypso`, `lima`, `morado` (ej: `.font-marino-50`, `.bg-cielo-30`).

#### Cuándo usar clases vs variables

| Situación | Usar |
|-----------|------|
| Color directo en HTML (sin CSS custom) | Clase: `<p class="font-brand-50">` |
| Color en estilos de un componente (scoped CSS) | Variable: `color: var(--cns-primary-brand-50)` |
| Color dinámico (condicional en JS) | Variable con style binding: `:style="{ color: 'var(--cns-primary-brand-50)' }"` |

#### Ejemplo

```html
<!-- Con clases utilitarias -->
<h2 class="cns-head-2 cns-font-semibold font-brand-50">Título azul</h2>
<section class="bg-brand-10 cns-p24">
  <p class="font-marino-90">Texto sobre fondo claro</p>
</section>

<!-- Con variables CSS (en <style>) -->
<style scoped>
.mi-seccion {
  background-color: var(--cns-primary-brand-10);
  color: var(--cns-primary-marino-90);
}
</style>
```

### Guía de uso por contexto

| Color | Cuándo usar | Ejemplo |
|-------|-------------|---------|
| Brand Azul | Acciones principales, navegación | Botones primarios, enlaces, headers |
| Marino | Textos principales, títulos | Headings, texto de navegación |
| Cielo | Fondos suaves, estados hover | Fondos de secciones, badges |
| Arena | Fondos cálidos | Cards, secciones alternativas |
| Calypso | Diferenciación de categorías | Tags, iconos temáticos |
| Lima | Elementos de energía | Promociones, destacados |
| Morado | Diferenciación premium | Productos premium, badges especiales |

### Neutrales por rango

| Rango | Uso | Ejemplo |
|-------|-----|---------|
| 00-20 | Fondos claros, superficies | Fondo de página, cards |
| 30-50 | Bordes, separadores, disabled | Bordes de inputs, divisores |
| 60-70 | Textos secundarios, placeholders | Texto de ayuda, labels |
| 80-90 | Textos principales | Párrafos, títulos |

### Tokens más usados

```css
--cns-primary-brand-50      /* Azul principal Consorcio */
--cns-primary-marino-90     /* Texto principal oscuro */
--cns-neutral-00            /* Blanco / fondo principal */
--cns-neutral-90            /* Texto principal */
--cns-neutral-70            /* Texto secundario */
--cns-neutral-50            /* Texto deshabilitado */
--cns-neutral-30            /* Bordes sutiles */
--cns-neutral-40            /* Bordes definidos */
--cns-semantic-success-50   /* Éxito */
--cns-semantic-error-50     /* Error */
--cns-semantic-warning-50   /* Advertencia */
--cns-semantic-info-50      /* Información */
```

### Accesibilidad y contraste (WCAG 2.1)

| Nivel | Texto normal | Texto grande | Uso |
|-------|-------------|-------------|-----|
| AA (mínimo) | 4.5:1 | 3:1 | Estándar |
| AAA (mejorado) | 7:1 | 4.5:1 | Contenido crítico |

Combinaciones seguras:
- Tonos 70-90 para texto sobre fondos claros (00-20)
- Tonos 00-20 para texto sobre fondos oscuros (70-100)
- Tono 80 de un semántico sobre tono 10 del mismo color

### Qué evitar

- No usar colores semánticos para decoración
- No mezclar demasiados colores primarios
- No usar valores hexadecimales directos (usar tokens)
- No ignorar contraste en estados hover
- No usar colores complementarios para acciones críticas

---

## Grid System

Componente `<cns-grid>` con contenedores fijos y fluidos.

### Breakpoints

| Breakpoint | Tamaño | Grid |
|-----------|--------|------|
| xs | 0px | grid-1 |
| sm | 576px | grid-2 |
| md | 768px | grid-3 |
| lg | 992px | grid-4 |
| xl | 1200px | grid-5 |
| xxl | 1400px | grid-6 |

### Contenedores Fijos

| Contenedor | Breakpoint | Max-Width | Columnas | Margen | Gutter |
|-----------|-----------|-----------|----------|--------|--------|
| grid-1 | < 576px | 375px | 4 | 16px | 8px |
| grid-2 | ≥ 576px | 540px | 4 | 18px | 16px |
| grid-3 | ≥ 768px | 720px | 6 | auto | 24px |
| grid-4 | ≥ 992px | 960px | 12 | auto | 24px |
| grid-5 | ≥ 1200px | 1140px | 12 | auto | 24px |
| grid-6 | ≥ 1400px | 1320px | 12 | auto | 24px |

### Contenedores Fluidos

| Contenedor | Columnas | Margen | Gutter |
|-----------|----------|--------|--------|
| container-fluid-4 | 4 | 24px | 16px |
| container-fluid-6 | 6 | 0 | 24px |
| container-fluid-12 | 12 | 0 | 24px |

### Uso

```html
<cns-grid container-type="grid-4">
  <div style="grid-column: span 3;">Sidebar</div>
  <div style="grid-column: span 9;">Contenido</div>
</cns-grid>
```

Prop `container-type`: `grid-1` a `grid-6`, `container-fluid-4`, `container-fluid-6`, `container-fluid-12`.

Usar `grid-column: span N` para definir cuántas columnas ocupa cada hijo.

---

## Shadow

Sombras basadas en color brand 50-azul.

| Clase | Box-shadow |
|-------|-----------|
| `cns-shadow soft` | 0px 4px 8px rgba(0, 48, 88, 0.15) |
| `cns-shadow hard` | 0px 8px 16px rgba(0, 48, 88, 0.20) |
| `cns-shadow soft bottom` | 0px 4px 8px rgba(0, 48, 88, 0.15) |
| `cns-shadow soft left` | -4px 0px 8px rgba(0, 48, 88, 0.15) |
| `cns-shadow hard bottom` | 0px 8px 16px rgba(0, 48, 88, 0.20) |
| `cns-shadow hard left` | -8px 0px 16px rgba(0, 48, 88, 0.20) |

**soft**: Elementos pequeños interactivos.
**hard**: Elementos destacados (modales, toasts).

```html
<div class="cns-shadow soft">Sombra suave</div>
<div class="cns-shadow hard">Sombra fuerte</div>
```

---

## Spacing

Escala modular para margen y padding. Todos los valores en px.

| Nombre | Tamaño |
|--------|--------|
| spacing 0 | 0px |
| spacing 4 | 4px |
| spacing 8 | 8px |
| spacing 12 | 12px |
| spacing 16 | 16px |
| spacing 20 | 20px |
| spacing 24 | 24px |
| spacing 32 | 32px |
| spacing 40 | 40px |
| spacing 48 | 48px |
| spacing 64 | 64px |
| spacing 80 | 80px |

### Clases de margen

Notación: `.cns-m{dirección}{valor}`

Direcciones: `m` (todos), `mt` (top), `mb` (bottom), `ml` (left), `mr` (right)

Valores: 0, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80

Ejemplos: `.cns-m8`, `.cns-mt16`, `.cns-mb24`, `.cns-ml40`, `.cns-mr80`

### Clases de padding

Notación: `.cns-p{dirección}{valor}`

Direcciones: `p` (todos), `pt` (top), `pb` (bottom), `pl` (left), `pr` (right)

Valores: 0, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80

Ejemplos: `.cns-p8`, `.cns-pt16`, `.cns-pb24`, `.cns-pl40`, `.cns-pr80`

```html
<div class="cns-m16 cns-p8">Margen 16px, padding 8px</div>
<div class="cns-mt24 cns-pb16">Margen top 24px, padding bottom 16px</div>
```

---

## Typography

### Fuentes

```css
font-family: 'OpenSans-Regular', 'Geograph-Regular', Arial, sans-serif;
```

- **Open Sans**: Fuente principal (textos, párrafos, UI)
- **Geograph**: Fuente complementaria (displays, headlines)

### Escala tipográfica

| Clase | Desktop (>991px) | Tablet (576-991px) | Mobile (≤575px) | Uso |
|-------|----------|--------|--------|-----|
| `.cns-display-3` | 48/62 | 28/36 | 28/36 | Display grande |
| `.cns-display-2` | 40/52 | 24/31 | 24/31 | Display mediano |
| `.cns-display-1` | 32/42 | 24/31 | 24/31 | Display pequeño |
| `.cns-lead-3` | 24/34 | 20/28 | 20/28 | Texto destacado 1 |
| `.cns-lead-2` | 20/28 | 18/27 | 18/27 | Texto destacado 2 |
| `.cns-lead-1` | 18/27 | 16/24 | 16/24 | Texto destacado 3 |
| `.cns-head-3` | 48/62 | 28/36 | 28/36 | Título principal |
| `.cns-head-2` | 40/52 | 24/31 | 24/31 | Título secundario |
| `.cns-head-1` | 32/42 | 24/31 | 24/31 | Título terciario |
| `.cns-subhead-3` | 28/39 | 20/28 | 20/28 | Subtítulo 3 |
| `.cns-subhead-2` | 24/34 | 20/28 | 20/28 | Subtítulo 2 |
| `.cns-subhead-1` | 20/28 | 18/27 | 18/27 | Subtítulo 1 |
| `.cns-text-3` | 18/27 | 16/24 | 16/24 | Texto grande |
| `.cns-text-2` | 16/24 | 16/24 | 16/24 | Texto medio |
| `.cns-text-1` | 14/21 | 14/21 | 14/21 | Texto base |
| `.cns-caption-2` | 12/18 | 12/18 | 12/18 | Leyenda mediana |
| `.cns-caption-1` | 10/15 | 10/15 | 10/15 | Leyenda pequeña |

Formato: tamaño(px)/line-height(px). Los tamaños son responsivos automáticamente.

### Peso tipográfico

#### Open Sans

| Clase | Peso | Uso |
|-------|------|-----|
| `.cns-font-regular` | 400 | Texto base, párrafos |
| `.cns-font-italic` | Italic | Énfasis alternativo |
| `.cns-font-medium` | 500 | Subtítulos, énfasis leve |
| `.cns-font-semibold` | 600 | Títulos, botones |
| `.cns-font-bold` | 700 | Títulos destacados |
| `.cns-font-bold-italic` | 700 + Italic | Énfasis alto |

#### Geograph

| Clase | Peso | Uso |
|-------|------|-----|
| `.cns-font-geo-light` | 300 | Contraste delicado |
| `.cns-font-geo-regular` | 400 | Display general |
| `.cns-font-geo-medium` | 500 | Display con más cuerpo |
| `.cns-font-geo-bold` | 700 | Headlines, display |

### Ejemplo

```html
<p class="cns-text-1">Texto base</p>
<h2 class="cns-head-2 cns-font-semibold">Título de sección</h2>
<span class="cns-caption-1 cns-font-medium">Leyenda</span>
```

Se puede combinar cualquier clase de fuente (`cns-font-*`) con cualquier tamaño (`cns-text-*`, `cns-head-*`, etc.).


---

## Layout y Visibilidad (sin clases utilitarias dedicadas)

El UI Kit V6 **no provee** clases utilitarias confiables para layout y visibilidad.
Aunque existen en el CSS (`cns-flex-*`, `cns-w-*`, etc.), no funcionan correctamente
y no se recomienda su uso.

Resolver estos patrones con CSS propio usando tokens de spacing:

```css
/* Layout flex con spacing del design system */
.mi-layout {
  display: flex;
  gap: 16px; /* spacing-16 */
  align-items: center;
}

/* Ocultar en mobile */
@media (max-width: 575px) {
  .solo-desktop { display: none; }
}

/* Ocultar en desktop */
@media (min-width: 576px) {
  .solo-mobile { display: none; }
}
```

Usar `matchMedia` en JS si la lógica de visibilidad afecta a datos o lógica de negocio,
no solo presentación (ver guía de `matchMedia` del equipo).

