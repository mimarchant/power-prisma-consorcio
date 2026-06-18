---
inclusion: manual
---
# UI Kit V6 (Prisma) - Instalación y Configuración

## Instalación completa

```bash
npm install @ui-kit/components-v6
```

Requiere archivo `.npmrc` configurado para acceder al repositorio privado en AWS CodeArtifact.

## Instalación de componentes individuales

```bash
npm install @ui-kit/button-v6
npm install @ui-kit/modal-v6
```

### Componentes disponibles

| Paquete | Componente |
|---------|-----------|
| `@ui-kit/accordeon-v6` | Acordeón |
| `@ui-kit/alert-v6` | Alerta |
| `@ui-kit/button-v6` | Botón |
| `@ui-kit/checkbox-v6` | Checkbox |
| `@ui-kit/input-v6` | Input |
| `@ui-kit/modal-v6` | Modal |
| `@ui-kit/panel-v6` | Panel |
| `@ui-kit/radiobutton-v6` | Radio button |
| `@ui-kit/selector-v6` | Selector |
| `@ui-kit/stepper-v6` | Stepper |
| `@ui-kit/switch-v6` | Switch |
| `@ui-kit/tabs-v6` | Tabs |
| `@ui-kit/tag-v6` | Tag |
| `@ui-kit/textarea-v6` | Textarea |

## Estilos globales

```bash
npm install @ui-kit/styles-v6
```

Importar en el entry point (`main.ts` o `main.js`):

```typescript
import '@ui-kit/styles-v6/dist/style.css';
```

## Configuración .npmrc

```ini
registry=https://registry.npmjs.org/
@ui-kit:registry=https://consorcio-digital-235204775724.d.codeartifact.us-east-1.amazonaws.com/npm/consorcio-repository/
//consorcio-digital-235204775724.d.codeartifact.us-east-1.amazonaws.com/npm/consorcio-repository/:always-auth=true
//consorcio-digital-235204775724.d.codeartifact.us-east-1.amazonaws.com/npm/consorcio-repository/:_authToken=CODEARTIFACT_AUTH_TOKEN
```

## Obtener token de AWS CodeArtifact

```bash
aws codeartifact get-authorization-token \
  --domain consorcio-digital \
  --domain-owner 235204775724 \
  --query authorizationToken \
  --output text
```

Reemplazar `CODEARTIFACT_AUTH_TOKEN` en `.npmrc` con el valor obtenido. El token expira y debe renovarse periódicamente.

## Verificación

1. Ejecutar `npm install`
2. Confirmar que existen paquetes en `node_modules/@ui-kit`
3. Importar un componente en la app para validar
