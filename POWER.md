---
name: "prisma-consorcio"
displayName: "Prisma (UI Kit V6) — Consorcio"
description: "Design system de Consorcio: web components cns- (Shadow DOM), tokens y utilidades para Vue 3"
keywords: ["prisma", "ui-kit", "consorcio", "cns", "design system", "web components", "vue", "componentes", "shadow dom", "ui kit v6", "formulario", "form", "vee-validate", "modal", "button", "input", "selector", "stepper", "tabs", "accordion", "token", "layout"]
author: "Equipo Sitios / Miguel Marchant"
---

# Prisma (UI Kit V6) — Consorcio

Design system propio de Consorcio basado en **web components con prefijo `cns-`** (Shadow DOM),
consumido desde `@ui-kit/components-v6` o desde paquetes individuales (`@ui-kit/<componente>-v6`).

**Stack objetivo:** Vue 3 (`<script setup>`, Composition API, sin TypeScript en frontend) + Vite.

Esta guía es **autoritativa** para cualquier UI que use componentes `cns-`. Antes de inventar markup
o estilos, cargar el steering del componente correspondiente y respetar sus props/eventos/slots reales.

## Onboarding

1. Verificar `.npmrc` apuntando a AWS CodeArtifact con token vigente **antes** de instalar → `prisma-instalacion.md`
2. Instalar el/los paquete(s): completo `@ui-kit/components-v6` o individuales.
3. Registrar el componente (`registerXxx()` en `main.ts`, o `CnsXxx()` desde la librería global).
4. Importar estilos globales una sola vez en el entry point: `import '@ui-kit/styles-v6/dist/style.css'`.
5. Aplicar convenciones transversales → `prisma-conventions.md`.

## Cuándo cargar cada steering file

- Instalación, `.npmrc`, AWS CodeArtifact, token → `prisma-instalacion.md`
- Convenciones transversales (eventos, Shadow DOM, patrones obligatorios) → `prisma-conventions.md`
- Tokens, colores, spacing, grid, tipografía, sombras, border-radius → `prisma-utilidades.md`
- Botones, estados `loading`, variantes, shapes → `prisma-button.md`
- Inputs (`text`/`rut`/`date`/`miles`/`password`/`phone`/`email`/`number`/`time`) → `prisma-input.md`
- Textarea multilínea, contador de caracteres → `prisma-textarea.md`
- Selector / dropdown / picker (text, logo, icon, checkbox) → `prisma-selector.md`
- Código segmentado / OTP / PIN → `prisma-segmentedinput.md`
- Checkbox (incl. indeterminate) → `prisma-checkbox.md`
- Radio button (grupos mutuamente exclusivos) → `prisma-radiobutton.md`
- Switch / toggle on-off → `prisma-switch.md`
- Alertas section / page notice → `prisma-alert.md`
- Modales (interruptLevel, states) → `prisma-modal.md`
- Panel deslizante lateral → `prisma-panel.md`
- Tabs (horizontal/vertical, azul/cielo) → `prisma-tabs.md`
- Formularios validados (vee-validate + Yup + Shadow DOM) → `prisma-forms.md`
- Acordeón / patrón FAQ + JSON-LD → `prisma-accordion.md`
- Stepper / flujos secuenciales multi-paso → `prisma-stepper.md`
- Tags / etiquetas / chips (readonly, primary, secondary) → `prisma-tag.md`
- LinkCard / tarjeta-enlace → `prisma-linkcard.md`
- ProgressSpinner (determinate/indeterminate) → `prisma-progressspinner.md`
- PageLoader / carga de pantalla completa → `prisma-pageloader.md`
- Patrones sin componente (tooltip, toast, skeleton, breadcrumb, table, pagination) → `prisma-no-component.md`
- Migración DS5 → Prisma (mapeo de props, tokens, breaking changes) → `prisma-migracion-ds5.md`

## Reglas mínimas (siempre)

- Usar tokens `--cns-*` y clases utilitarias (`cns-*`); **nunca** valores hex directos.
- Los eventos de los componentes `cns-` viajan en `event.detail` (no en el target).
- Componentes de overlay (`cns-modal`, `cns-panel`) controlan visibilidad desde el padre con
  prop (`:show` / `:showModal`) + evento `@close`. El componente no se cierra solo.
- No estilar internals del Shadow DOM; usar las props/slots expuestos.
