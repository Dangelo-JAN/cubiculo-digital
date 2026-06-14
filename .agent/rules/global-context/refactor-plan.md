---
trigger: always_on
---

# 🏗️ Refactor Plan — Fases Activas

> **⚠️ REGLA**: Consultar este archivo ANTES de implementar cualquier cambio arquitectónico. Las fases tienen dependencias. No saltar fases.

## Resumen de Fases

| Fase | Área | Issues | Prioridad | Estado |
|------|------|--------|-----------|--------|
| 🔴 **Fase 0** | Seguridad crítica (bloqueante) | SEC-01 a SEC-05 | P0-critical | ⏳ Pendiente |
| 🏛️ **Fase 1** | Arquitectura (monorepo + GraphQL + Prisma) | ARC-01 a ARC-05, GRAPH-01 a GRAPH-05, DATA-01 a DATA-05 | P0 | ⏳ Pendiente |
| 🧪 **Fase 2** | Testing + Tooling | TEST-01 a TEST-10, TOOL-01 a TOOL-05 | P0-P1 | ⏳ Pendiente |
| 🔄 **Fase 3** | CI/CD + GitHub Projects | CI-01 a CI-05, PROJ-01 a PROJ-04 | P1 | ⏳ Pendiente |
| 🎨 **Fase 4** | Frontend (componentes, dark mode, bundle) | UI-01 a UI-07, DM-01 a DM-02, PERF-01 a PERF-03 | P1 | ⏳ Pendiente |
| 🔧 **Fase 5** | API (error handling, logging, Redis) | API-01 a API-04, OBS-01 a OBS-05, REDIS-01 a REDIS-02 | P0-P1 | ⏳ Pendiente |
| 📚 **Fase 6** | Documentación | DOC-01 a DOC-07 | P2 | ⏳ Pendiente |
| 🧹 **Fase 7** | Limpieza y consistencia | CLEAN-01 a CLEAN-08, STYLE-01 a STYLE-05, PKG-01 a PKG-04 | P0-P1 | ⏳ Pendiente |
| 📊 **Fase 8** | Monitoreo y métricas | MON-01 a MON-04 | P1-P2 | ⏳ Pendiente |
| 📦 **Fase 9** | Features backlog | F-07 a F-21 del roadmap | P0-P2 | ⏳ Pendiente |

## 🔴 Fase 0: Seguridad Crítica (BLOQUEANTE)
> Nada más importa hasta que estos items estén resueltos. Bloquean cualquier deploy público.

| ID | Issue | Archivos |
|----|-------|----------|
| SEC-01 | JWT sin expiry — `jwt.sign()` sin `expiresIn` | `apps/api/src/graphql/modules/auth/auth.resolvers.ts:18,31` |
| SEC-02 | Secrets en `.env` comiteado — rotar TODO | `.env` → eliminar del repo, migrar a GitHub Secrets |
| SEC-03 | `users` query pública sin autenticación | `apps/api/src/graphql/index.ts:40` |
| SEC-04 | Logging inconsistente: mezcla `[OPENAI_*]`/`[GROQ_*]` | `apps/api/src/core/ai/ai.service.ts:6`, `interview.resolvers.ts:47,53,61` |
| SEC-05 | Sin rate limiting — endpoint GraphQL público sin protección DoS | `apps/api/src/index.ts` |

## 🏛️ Fase 1: Arquitectura

| ID | Refactor | Archivos |
|----|----------|----------|
| ARC-01 | Eliminar `apps/public/` (mover SVGs a `web/public/`) | `apps/public/*` → `apps/web/public/` |
| ARC-02 | Crear `packages/config/` (tsconfig, eslint, prettier compartidos) | Nuevo package |
| ARC-03 | Desduplicar root package.json (mover React/Next solo a web/) | `package.json`, `apps/web/package.json` |
| ARC-04 | Migrar `next.config.ts` a ESM (`module.exports` → `export default`) | `apps/web/next.config.ts` |
| ARC-05 | Eliminar archivos legacy: `schema.ts`, `context.ts`, `resolvers/health.ts` | 3 archivos en `apps/api/src/` |
| GRAPH-01 | Separar schema GraphQL a `schema.graphql` (hoy inline en index.ts) | Nuevo: `apps/api/src/graphql/schema.graphql` |
| GRAPH-02 | Crear `Departments` GraphQL type + dashboard resolver | `apps/api/src/graphql/modules/dashboard/` |
| GRAPH-03 | Conectar dashboard a DB real (hoy mock data) | Dashboard resolver |
| GRAPH-04 | Tipado compartido API-Web (`packages/types/`) | Nuevo package |
| GRAPH-05 | Estandarizar error handling (códigos `UNAUTHORIZED`, `NOT_FOUND`, etc.) | `apps/api/src/graphql/errors.ts` |
| DATA-01 | Agregar `role` enum a User (`ADMIN`, `USER`) | Prisma migration |
| DATA-02 | Agregar `deletedAt` para soft delete | Prisma migration |
| DATA-03 | Agregar índices compuestos | Prisma migration |
| DATA-04 | Migrar Question de hardcode a DB (seed) | Seed + resolver update |
| DATA-05 | Agregar `companyId` opcional (multi-tenant futuro) | Prisma migration |

## 🧪 Fase 2: Testing
TEST-01: Vitest API, TEST-02: Vitest Web, TEST-03: Playwright E2E, TEST-04-06: Tests resolvers, TEST-07-08: Tests hooks/middleware, TEST-09-10: E2E auth/interview, TOOL-01: TypeScript strict, TOOL-02: ESLint+Prettier, TOOL-03: Husky+lint-staged, TOOL-04: Script `ci`, TOOL-05: Script `test:coverage`

## 🔄 Fase 3: CI/CD + GitHub Projects
CI-01: PR Quality Gate, CI-02/03: Deploy API staging/prod, CI-04: Deploy Web, CI-05: Security Scan, PROJ-01: Labels, PROJ-02: Milestones, PROJ-03: Issue templates, PROJ-04: Definition of Done

## 🎨 Fase 4: Frontend
UI-01: Server/Client convention, UI-02: Loading states, UI-03: Error boundaries, UI-04: not-found pages, UI-05: Fix `/setup` link, UI-06: i18n, UI-07: Fix Signup button label, DM-01: `transition-colors`, DM-02: Unificar dark colors, PERF-01/02/03: Bundle optimization

## 🔧 Fase 5: API Robustez
API-01: Retry pattern AI (3 retries, exponential backoff), API-02: Structured error codes, API-03: Dead letter queue AI failures, API-04: Health endpoint JSON, OBS-01: Pino structured logging, OBS-02: Request ID tracking, OBS-03: Sentry, OBS-04: Unificar prefijos `[GROQ_*]`, OBS-05: Business metrics counters, REDIS-01: Lazy connect, REDIS-02: Health ping

## 🧹 Fase 7: Limpieza
CLEAN-01 a CLEAN-03: Eliminar archivos legacy API, CLEAN-04: Mover `apps/public/`, CLEAN-05/06: Eliminar código comentado, CLEAN-07/08: Eliminar deps no usadas, STYLE-01/02/03: Fix signup button/title/typo, STYLE-04: Unificar dark colors, STYLE-05: next.config ESM, PKG-01 a PKG-04: Desduplicar deps

## 📊 Fase 8: Monitoreo
MON-01: Dashboard métricas (Grafana/Metabase), MON-02: Alertas Slack/PagerDuty, MON-03: Uptime monitoring, MON-04: User analytics

## Plan de Ataque Semanal
```
Semana 1 (Días 1-2):   🔴 FASE 0 — SEC-01, SEC-02, SEC-03, SEC-05
Semana 1 (Días 3-5):   🏛️ FASE 1 + FASE 7 — ARC-01 a ARC-05 + CLEAN-01 a CLEAN-08
Semana 2:               🧪 FASE 2 — TEST-01 a TEST-10, TOOL-01 a TOOL-05
Semana 3:               🔄 FASE 3 — CI-01 a CI-05, PROJ-01 a PROJ-04
Semana 4:               🎨 FASE 4 — UI-01 a UI-07, DM-01/02, PERF-01 a PERF-03
Semana 5:               🔧 FASE 5 — API-01 a API-04, OBS-01 a OBS-05, REDIS-01/02
Semana 6:               📚 FASE 6 — DOC-01 a DOC-07
Semana 7+:              📊 FASE 8 + FASE 9 — MON-01 a MON-04 + Features backlog
```
