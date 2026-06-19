# Prisma (UI Kit V6) — Consorcio · Kiro Power

Kiro Power con la documentación del design system **Prisma** de Consorcio: web components
`cns-` (Shadow DOM), tokens y utilidades, orientado a Vue 3 + Vite.

Carga los steering de cada componente **on-demand** según la tarea, evitando saturar el
contexto del agente con los 21 archivos a la vez.

## Instalación en Kiro

En el IDE: **Add Custom Power → Import power from GitHub** y pega la URL de este repo.

> El repo debe ser **público** para compartirlo al equipo. Si es privado, cada usuario
> necesita permisos de acceso.

## Contenido

```
power-prisma-consorcio/
├── POWER.md                  # metadata + onboarding + mapeo de carga
└── steering/
    ├── prisma-conventions.md # reglas transversales (eventos, overlays, v-model, Chile)
    ├── prisma-instalacion.md
    ├── prisma-utilidades.md  # tokens, grid, tipografía, spacing, sombras, layout
    ├── prisma-forms.md       # formularios validados (vee-validate + Yup + Shadow DOM)
    ├── prisma-no-component.md # patrones sin componente cns- (tooltip, toast, table, etc.)
    └── prisma-<componente>.md (button, input, modal, panel, tabs, ...)
```

## Mantención

Tratar los steering como código versionado. Al actualizar un componente del UI Kit,
actualizar su `.md` y, si cambia el nombre del power (`name` en POWER.md), avisar al equipo
(puede requerir reinstalar).
