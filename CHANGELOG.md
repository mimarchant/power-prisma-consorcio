# Changelog

Cuando se publica una versión nueva (tag/release en GitHub), el equipo debe
**reimportar el power** en Kiro para recibir los cambios.

## [Unreleased]
### Added
-

### Changed
-

### Fixed
-

## [1.0.2] - 2026-06-19
### Added
-

### Changed
-

### Fixed
-

## [1.0.2] - 2026-06-19
### Changed
- `prisma-utilidades.md`: agregada sección de clases utilitarias de color (`.font-{nombre}-{tono}`,
  `.bg-{nombre}-{tono}`) como alternativa a las variables CSS `var(--cns-*)`. Incluye tabla de
  clases Primary (brand 10-100) y guía de cuándo usar clases vs variables.
- `prisma-utilidades.md`: corregida sección "Layout y Visibilidad" — las clases `cns-flex-*`,
  `cns-w-*` existen en el CSS pero no funcionan correctamente; se mantiene la recomendación
  de usar CSS propio.

## [1.0.1]
### Added
- `prisma-forms.md` (inclusion: manual): guía completa para construir formularios validados
  con vee-validate + Yup sobre componentes `cns-` (Shadow DOM) en Vue 3. Cubre:
  - Puente `event.detail` → `useField` para sincronizar valores con vee-validate.
  - Captura de eventos del Shadow DOM con `capture: true`.
  - Timing con `nextTick` al hidratar o precargar valores programáticos.
  - Validación de RUT chileno con algoritmo módulo 11 y dígito verificador.
  - Selectores en cascada (región → ciudad → comuna) con watchers y reset de hijos.
  - Esquemas dinámicos con `yup.lazy` + `useFieldArray` para listas variables.
  - Checklist para cotizadores multi-paso con `cns-stepper`.
- Sección "Layout y Visibilidad" en `prisma-utilidades.md`: documenta que no existen clases
  utilitarias de display/flex/visibility y cómo resolverlo con CSS propio.

### Changed
- `POWER.md`: ampliadas keywords para activación más agresiva del power; agregado
  `prisma-forms.md` al mapeo de carga on-demand.
- `prisma-conventions.md`: agregada nota sobre el origen de los steering (Storybook oficial
  vs patrones de integración del equipo).
- `prisma-forms.md`: agregada nota aclarando que los patrones provienen de implementaciones
  reales, no del Storybook oficial.
- `prisma-input.md`: agregada sección "Excepción: vee-validate + useField" que aclara que
  `e.detail` sí funciona cuando se usa vee-validate (resuelve contradicción con prisma-forms).
- `prisma-accordion.md`: patrón FAQ ahora incluye inyección de JSON-LD `FAQPage` para SEO.

### Fixed
-

## [1.0.0] - 2026-06-18
### Added
- POWER.md con onboarding y mapeo de carga on-demand de cada steering.
- 20 steering de componentes del UI Kit V6 (button, input, modal, panel, tabs,
  accordion, stepper, selector, segmentedinput, checkbox, radiobutton, switch,
  alert, tag, linkcard, textarea, progressspinner, pageloader) más instalación y utilidades.
- prisma-conventions.md con reglas transversales (eventos `cns-` vía `event.detail`,
  `@cnsclick`, patrón `:show`/`@close` en overlays, v-model, JSON en `:values`/`:steps`,
  RUT/miles chilenos, restricciones de `loading`).
- README con instrucciones de instalación vía Import from GitHub.
