---
inclusion: manual
---
# UI Kit V6 (Prisma) - Modal

**Versión**: 6.2.0
**Paquete**: `@ui-kit/modal-v6`

Modal es un componente que aparece sobre el contenido actual, bloqueando la interacción con el fondo. Se utiliza para mostrar contenido relevante o acciones que requieren la atención exclusiva del usuario.

## Instalación

```bash
npm install @ui-kit/modal-v6
```

Registro global en `main.ts`:

```typescript
import { registerModal } from '@ui-kit/modal-v6'
registerModal()
```

O desde la librería global:

```typescript
import { CnsModal } from '@ui-kit/components-v6';
CnsModal();
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `id` | string | - | Identificador único |
| `showModal` | boolean | false | Controla si el modal está visible |
| `modalType` | string | `standard` | Tipo: `standard`, `tupass` |
| `state` | string | `information` | Estado visual: `information`, `discovery`, `warning`, `critical`, `success`, `error` |
| `interruptLevel` | string | `low` | Nivel de interrupción: `low`, `medium`, `high` |
| `title` | string | - | Título principal en la cabecera |
| `description` | string | - | Texto descriptivo o contenido principal |
| `showIcon` | boolean | true | Muestra/oculta el ícono del modal |
| `showDescription` | boolean | true | Muestra/oculta la descripción |
| `showSlot` | boolean | false | Muestra/oculta el slot de contenido |
| `showFooter` | boolean | true | Muestra/oculta el slot de footer |

## Eventos

| Evento | Descripción |
|--------|-------------|
| `close` | Se emite cuando el usuario intenta cerrar el modal (clic fuera, botón cerrar, ESC) |

## Slots

| Slot | Descripción |
|------|-------------|
| `content` | HTML personalizado entre la descripción y el footer |
| `footer` | Botones de acción/cancelación |

## Niveles de interrupción

| Nivel | Comportamiento |
|-------|---------------|
| `low` | Información sin acción obligatoria. Se cierra con ESC o clic fuera |
| `medium` | Requiere acción antes de continuar. Puede cerrarse con ESC o clic fuera. Fondo bloqueado |
| `high` | Acciones irreversibles. No se cierra con ESC ni clic fuera. Solo interacción explícita |

## Estados visuales (paleta semántica)

| State | Uso |
|-------|-----|
| `information` | Información general |
| `discovery` | Novedad, exploración |
| `warning` | Advertencia, precaución |
| `critical` | Urgencia máxima, irreversible |
| `success` | Operación exitosa |
| `error` | Error, acción destructiva |

## Manejo de visibilidad

- El estado `showModal` **siempre se gestiona en el padre**
- El modal no se cierra solo: emite el evento `close`
- El padre debe implementar la función de cierre y puede ejecutar lógica previa

## Consideraciones

- **Slot content**: Acepta HTML personalizado. Si proviene de fuentes externas, sanear y validar antes de inyectar
- **Slot footer**: Ideal para botones de acción. `showFooter=true` por defecto
- **modalType tupass**: Variante visual para flujos TuPass

## Ejemplos de uso

```vue
<script setup>
import { ref } from 'vue'

const showModal = ref(false)
const openModal = () => (showModal.value = true)
const closeModal = () => {
  // Lógica previa al cierre (métricas, guardado, etc.)
  showModal.value = false
}
</script>

<template>
  <cns-button label="Abrir" variant="primary" @cnsclick="openModal" />

  <cns-modal
    :showModal="showModal"
    @close="closeModal"
    title="Título del modal"
    description="Descripción del contenido"
    state="information"
    interruptLevel="low"
  >
    <div slot="footer">
      <cns-button label="Cancelar" variant="tertiary" fullwidth @cnsclick="closeModal" />
      <cns-button label="Aceptar" variant="primary" fullwidth @cnsclick="closeModal" />
    </div>
  </cns-modal>
</template>
```

```html
<!-- Modal de confirmación crítica -->
<cns-modal
  :showModal="showConfirm"
  @close="closeConfirm"
  title="¿Estás seguro?"
  description="Esta acción no se puede deshacer"
  state="critical"
  interruptLevel="high"
>
  <div slot="footer">
    <cns-button label="Cancelar" variant="tertiary" fullwidth @cnsclick="closeConfirm" />
    <cns-button label="Eliminar" variant="primary" color="error" fullwidth @cnsclick="confirmarEliminacion" />
  </div>
</cns-modal>

<!-- Modal con slot content -->
<cns-modal
  :showModal="showCustom"
  @close="closeCustom"
  title="Detalle de operación"
  description="Revisa los datos antes de confirmar"
  :showSlot="true"
>
  <div slot="content">
    <ul>
      <li>Monto: $150.000</li>
      <li>Destino: Cuenta corriente</li>
    </ul>
  </div>
  <div slot="footer">
    <cns-button label="Confirmar" variant="primary" fullwidth @cnsclick="confirmar" />
  </div>
</cns-modal>

<!-- Modal sin footer -->
<cns-modal
  :showModal="showInfo"
  @close="closeInfo"
  title="Información"
  description="Tu solicitud fue recibida correctamente"
  state="success"
  :showFooter="false"
></cns-modal>

<!-- Modal TuPass -->
<cns-modal
  :showModal="showTupass"
  @close="closeTupass"
  modalType="tupass"
  title="Autorización TuPass"
  description="Confirma la operación en tu dispositivo"
></cns-modal>
```
