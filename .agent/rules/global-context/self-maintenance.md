---
trigger: always_on
---

# 🔄 Self-Maintenance: Actualización Post-Flight

Este archivo define cuándo y cómo el agente DEBE actualizar su propia configuración después de completar una tarea.

## ⏱ Cuándo se ejecuta

**SOLO** después de que la bitácora de la tarea se marque como:

- `✅ FINALIZADO`
- `✅ COMPLETADO`

NO se ejecuta antes, durante, ni en medio de la tarea. Es un **post-flight check** que ocurre al cierre del ciclo de vida de la tarea.

## 📊 Matriz de actualización

| Si la tarea COMPLETADA implicó... | Entonces DEBES actualizar... |
|-----------------------------------|------------------------------|
| Nuevo feature cross-cutting (impacta API+Web) con reglas invariantes | Crear archivo en `global-context/` + registrar en `index.md` |
| Cambio en el stack tecnológico (nueva librería, nuevo servicio) | `global-context.md` (sección 2: Tech Stack) |
| Nueva ruta principal o cambio de rutas existentes | `route-map.md` |
| Nueva regla de desarrollo (tema, responsive, seguridad) | `development-invariants.md` |
| Nueva convención de naming | `naming-conventions.md` |
| Nueva regla técnica (validación, modularidad, integridad) | `technical-rules.md` |
| Nueva regla de accesibilidad/contraste | `accessibility.md` |
| Nuevo token/componente/patrón visual | Archivo correspondiente en `design-system/` |
| Cambio en schema GraphQL o Prisma | `api-schema.md` |
| Cambio en Docker, Vercel, o env vars | `infra-deploy.md` |
| Cambio en el flujo de Git o PR | `AGENTS.md` y/o `.agent/workflows/git-workflow.md` |
| Cambio en el protocolo de inicio del agente | `AGENTS.md` |
| Cambio en la visión del producto, personas, o costos | `product-vision.md` |
| Cambio en el backlog o roadmap | `product-roadmap.md` |
| Cambio en el plan de refactor (nueva fase, issue completado) | `refactor-plan.md` |
| Nueva deuda técnica identificada | `tech-debt.md` |
| Cambio en estrategia de testing o framework | `testing-standards.md` |
| Cambio en GitHub Projects config (labels, milestones, templates) | `project-management.md` |
| Cambio en procedimientos de ops, debugging, rollback | `ops-runbook.md` |
| Nuevo skill o skill modificado | `.agent/skills/*/SKILL.md` correspondiente |
| Deprecación de una regla existente | Archivo correspondiente + marcar como `⚠️ DEPRECATED` |

## 🚦 Indicadores de auto-mantenimiento

Responde **SÍ** a alguna de estas preguntas al finalizar la tarea:

- [ ] ¿La tarea introdujo un nuevo patrón que no existía antes? (ej: WebSockets, cola de mensajes, nueva BD)
- [ ] ¿La tarea modificó la forma en que frontend y backend se comunican?
- [ ] ¿La tarea agregó una dependencia externa nueva (servicio, SDK, API)?
- [ ] ¿La tarea creó un nuevo tipo de componente que se usará en múltiples lugares?
- [ ] ¿La tarea cambió reglas de estilo, colores, o componentes visuales?
- [ ] ¿La tarea modificó el flujo de trabajo (Git, PR, revisión)?
- [ ] ¿La tarea agregó o eliminó una convención de desarrollo?

Si alguna respuesta es **SÍ** → actualizar el/los archivos según la matriz.

## 🛑 Regla de oro

Documenta **SOLO** lo que la tarea realmente construyó, no lo que planeaste. La verdad la tiene el código completado, no el plan inicial. Si el cambio arquitectónico fue menor o no evidente, NO fuerces una actualización.
