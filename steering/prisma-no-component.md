---
inclusion: manual
---
# UI Kit V6 (Prisma) - Patrones sin componente dedicado

Listado de elementos UI comunes que **NO tienen un componente `cns-`** en el design system.
Resolver con HTML semántico + tokens/utilidades de Prisma. No inventar componentes inexistentes.

## Tooltip

No existe `<cns-tooltip>`. Los componentes que lo necesitan exponen la prop `showTooltip` /
`tooltiptext` internamente (ej: `cns-input`, `cns-selector`).

Para tooltips custom fuera de un componente `cns-`, usar:
- `title` nativo del HTML (limitado, no estilizable)
- Una librería ligera como `floating-ui` con estilos propios usando tokens `--cns-*`

## Toast / Snackbar

No existe `<cns-toast>`. Para feedback transitorio:
- Usar `cns-alert` con `type="section"` posicionado con CSS (`position: fixed`)
- Controlar visibilidad con un `ref` + `setTimeout` para auto-dismiss
- O implementar un componente Vue local usando tokens de color semántico

## Skeleton / Placeholder de carga

No existe `<cns-skeleton>`. Para loading states de contenido:
- Usar divs con fondo `var(--cns-neutral-20)` y `border-radius` del token
- Animación con `@keyframes` (pulse o shimmer) usando colores neutral-10 a neutral-30
- `cns-progressspinner` para spinners aislados; `cns-pageloader` para pantalla completa

## Breadcrumb

No existe `<cns-breadcrumb>`. Implementar con HTML semántico:

```html
<nav aria-label="Breadcrumb">
  <ol class="cns-text-1" style="display:flex; gap:8px; list-style:none; padding:0;">
    <li><a href="/">Inicio</a></li>
    <li aria-hidden="true">/</li>
    <li><a href="/seguros">Seguros</a></li>
    <li aria-hidden="true">/</li>
    <li aria-current="page">Seguro de vida</li>
  </ol>
</nav>
```

Para SEO, inyectar `BreadcrumbList` en JSON-LD (ver guía de datos estructurados del equipo).

## Table / DataGrid

No existe `<cns-table>`. Usar `<table>` nativo con estilos:

```html
<table class="cns-text-1">
  <thead style="background: var(--cns-neutral-10); border-bottom: 1px solid var(--cns-neutral-30);">
    <tr>
      <th class="cns-p8 cns-font-semibold">Columna</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom: 1px solid var(--cns-neutral-20);">
      <td class="cns-p8">Valor</td>
    </tr>
  </tbody>
</table>
```

## Pagination

No existe `<cns-pagination>`. Implementar con botones:

```html
<nav aria-label="Paginación" style="display:flex; gap:8px; align-items:center;">
  <cns-button variant="tertiary" color="azul" size="40" shape="circle" @cnsclick="prev">
    <svg slot="icon-left"><!-- ← --></svg>
  </cns-button>
  <span class="cns-text-1 cns-font-medium">Página 1 de 5</span>
  <cns-button variant="tertiary" color="azul" size="40" shape="circle" @cnsclick="next">
    <svg slot="icon-left"><!-- → --></svg>
  </cns-button>
</nav>
```

## Divider / Separador

No existe `<cns-divider>`. Usar `<hr>` estilizado:

```html
<hr style="border: none; border-top: 1px solid var(--cns-neutral-30); margin: 24px 0;" />
```

## Badge / Chip de notificación

No existe un badge standalone. `cns-tab` tiene prop `badge` interna. Para badges en otros
contextos, usar un `<span>` con tokens:

```html
<span
  class="cns-caption-2 cns-font-semibold cns-p4"
  style="background: var(--cns-semantic-error-50); color: var(--cns-neutral-00); border-radius: 9999px; min-width: 20px; text-align: center;"
>
  3
</span>
```

## Regla general

Si necesitas un patrón UI que no tiene componente `cns-`, construirlo con:
1. HTML semántico (`<nav>`, `<table>`, `<ol>`, etc.)
2. Tokens `--cns-*` para colores, spacing, border-radius
3. Clases utilitarias `cns-*` para tipografía, margin, padding
4. **Nunca** valores hex directos ni clases inventadas con prefijo `cns-` que no existan
