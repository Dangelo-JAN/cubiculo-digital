---
trigger: always_on
---

# 🌍 Global Context & Master Rules (Cubículo Digital - Biblia Corporativa)

## 1. Visión del Proyecto
Plataforma SaaS B2B que transforma conocimiento tácito corporativo en activos digitales estructurados ("Biblia Corporativa") mediante entrevistas guiadas por IA (Groq/Llama-3.3-70b). Target: startups, scale-ups y PYMEs que necesitan documentar conocimiento organizacional para fine-tuning de modelos de IA propios o consulta estratégica.

Para visión detallada, user personas, value prop y backlog → consultar [`product-vision.md`](./product-vision.md) y [`product-roadmap.md`](./product-roadmap.md).

## 2. Tech Stack & Infraestructura
- **Frontend:** Next.js 15 (App Router), React 19, Tailwind v4, Apollo Client v3, Lucide React.
- **Backend:** Node.js 20, GraphQL Yoga v5, Prisma ORM, bcryptjs, JWT, Groq SDK.
- **Base de Datos:** PostgreSQL (Supabase).
- **Caché:** Redis (Upstash) para APQ + query cache.
- **Monorepo:** pnpm workspaces con 3 paquetes (`apps/web`, `apps/api`, `packages/db`).

## 3. Arquitectura y Principios
- **Monorepo pnpm:** DB package compartido via `@cubiculo/db`.
- **GraphQL First:** Schema céntrico, resolvers modulares por módulo (auth, interview).
- **Auth:** JWT en dual storage (localStorage para Apollo, cookies para Next.js middleware).
- **Caché:** Apollo InMemoryCache + Redis APQ + localStorage resilience.
- **Estados de UI:** Server Components (layout, page shells) + Client Components (interactividad, GraphQL).

## 4. The Source of Truth
- **Datos:** PostgreSQL via Prisma ORM.
- **API:** GraphQL Yoga schema autogenerado.
- **Auth:** JWT token verificado en context.ts.
- **AI:** Groq SDK con modelo llama-3.3-70b-versatile.

## 5. Reglas Especializadas
| Contexto | Archivo |
|----------|---------|
| Reglas detalladas (rutas, invariantes, naming, técnicas) | `.agent/rules/global-context/index.md` |
| Diseño visual (colores, componentes, tokens) | `.agent/rules/design-system/index.md` |
| API GraphQL y Schema | `.agent/rules/global-context/api-schema.md` |
| Infraestructura y Deploy | `.agent/rules/global-context/infra-deploy.md` |
| Product Vision y Personas | `.agent/rules/global-context/product-vision.md` |
| Roadmap y Backlog | `.agent/rules/global-context/product-roadmap.md` |
| Refactor Plan Activo | `.agent/rules/global-context/refactor-plan.md` |
| Technical Debt Registry | `.agent/rules/global-context/tech-debt.md` |
| Testing Standards | `.agent/rules/global-context/testing-standards.md` |
| Project Management | `.agent/rules/global-context/project-management.md` |
| Ops Runbook | `.agent/rules/global-context/ops-runbook.md` | |

## 6. Flujo de Git (NO NEGOCIABLE)
Seguir estrictamente `.agent/workflows/git-workflow.md`. Prohibido commit directo a `main` o `dev`.

## 7. Regla Obligatoria de Pull Request
**NUNCA** PR directo a `main`. Flujo obligatorio: `Rama de trabajo` → `dev` → `main`.

## 8. Protocolo de Triaje
1. **Exentas (sin Git/Bitácora):** Cambios en `.gitignore`, `.agent/`, `.opencode/`, pruebas locales.
2. **Trackeables (Git + PR + Bitácora):** Todo cambio en `apps/web/`, `apps/api/`, `packages/`, assets o config de producción.

## 9. Seguridad Obligatoria
- JWT DEBE tener `expiresIn: '1d'` en signup y login (P0)
- Toda query protegida DEBE verificar `context.currentUser`
- `users` query requiere autenticación (P0)
- Secrets NUNCA en `.env` comiteado — usar secrets manager (P0)
