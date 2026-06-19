# Hooks recomendados para proyectos Prisma

Hooks de Kiro que refuerzan las convenciones del design system en tiempo de desarrollo.
Son opcionales — cada desarrollador los instala en su proyecto si los quiere.

## Instalación

Copiar el archivo `.json` del hook deseado a `.kiro/hooks/` en la raíz del proyecto:

```bash
# Desde la raíz de tu proyecto Vue
mkdir -p .kiro/hooks
cp <ruta-al-power>/hooks/validate-prisma-conventions.json .kiro/hooks/
```

O copiar el contenido manualmente y pegarlo como nuevo hook desde la UI de Kiro
(Command Palette → "Open Kiro Hook UI").

## Hooks disponibles

### validate-prisma-conventions.json

**Trigger**: `fileEdited` en archivos `*.vue`
**Acción**: `askAgent` (solo sugiere, no modifica código)

Detecta y sugiere correcciones para:
- Valores hex directos → tokens `--cns-*`
- `addEventListener('resize')` → `matchMedia`
- `v-model` en componentes `cns-` → shadowRoot o vee-validate
- `@click` en `cns-button` → `@cnsclick`
- Estilos apuntando a internals del Shadow DOM → props/slots

**Impacto en performance del agente**: bajo. Solo se activa al guardar un `.vue` y
el prompt es corto. Si se siente lento, desactivarlo temporalmente renombrando el archivo.
