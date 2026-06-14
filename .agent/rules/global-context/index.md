---
trigger: always_on
---

# 🗺️ Index: Reglas Globales Especializadas

Este archivo indexa todas las reglas detalladas del proyecto. Consultar el archivo correspondiente según el contexto de la tarea.

## 📂 Estructura de Reglas

1. **[Mapa de Rutas](./route-map.md)**: Rutas de la aplicación (públicas y protegidas).
2. **[Invariantes de Desarrollo](./development-invariants.md)**: Soporte temático, responsividad, seguridad.
3. **[Convenciones de Naming](./naming-conventions.md)**: Archivos, componentes, GraphQL types.
4. **[Reglas Técnicas](./technical-rules.md)**: Validación, modularidad, integridad fullstack.
5. **[Accesibilidad y Contraste](./accessibility.md)**: WCAG, reglas de contraste modo oscuro/claro.
6. **[API Schema](./api-schema.md)**: GraphQL types, resolvers, Prisma schema.
7. **[Infra y Deploy](./infra-deploy.md)**: Docker, Vercel, Redis, variables de entorno.
8. **[Self-Maintenance](./self-maintenance.md)**: Reglas de actualización post-flight de la configuración del agente.
9. **[Product Vision](./product-vision.md)**: Visión del producto, user personas, value prop, costos, glosario.
10. **[Product Roadmap](./product-roadmap.md)**: Backlog priorizado (F-01 a F-24), roadmap trimestral, milestones.
11. **[Refactor Plan](./refactor-plan.md)**: Fases activas de refactor, issues, attack plan semanal.
12. **[Technical Debt](./tech-debt.md)**: Deuda gobernada, archivos legacy, dark mode inconsistency, packages.
13. **[Testing Standards](./testing-standards.md)**: Estrategia de testing, frameworks, cobertura, comandos.
14. **[Project Management](./project-management.md)**: GitHub Projects labels, milestones, epics, issue templates, DoD.
15. **[Ops Runbook](./ops-runbook.md)**: Debugging, rollback, health checks, alertas, GDPR.

## 🥇 Reglas de Oro (Cross-cutting)

1. **Fullstack Integrity**: Toda funcionalidad requiere Schema + Resolver (API) + Query/Mutation + UI (Web). No maquetación sin persistencia.
2. **Soporte Temático Bidireccional**: Todo componente debe soportar Light/Dark mode via Tailwind `dark:`.
3. **Seguridad por Defecto**: JWT con expiry, auth en toda query protegida, CORS restrictivo.
4. **GraphQL Naming**: Types PascalCase, queries/mutations camelCase, fields camelCase.
5. **Feature Standards Primero**: Para toda feature nueva, leer `testing-standards.md` y ejecutar `@feature-implementation` skill.
6. **Refactor Aware**: Consultar `refactor-plan.md` antes de cambios arquitectónicos — respetar dependencias entre fases.

## 🛑 Prohibiciones Estrictas

1. **No romper estructura monorepo**: `apps/web/`, `apps/api/`, `packages/db/` son dominios separados.
2. **No trabajar sin bitácora**: Toda tarea trackeable requiere bitácora ANTES de escribir código.
3. **No JWT sin expiry**: Prohibido firmar tokens sin `expiresIn`.
4. **No exponer queries sin auth**: Prohibido resolver `users` sin verificar `currentUser`.
5. **No secrets en código**: Prohibido commitear `.env` con claves reales.
6. **No Zero Tolerance violations**: Ver sección Z en `technical-rules.md` — prohibiciones absolutas.
