---
trigger: always_on
---

# 📛 Convenciones de Naming

## Branches (Git)
- **Formato**: `<type>/<descripción>` — lowercase, kebab-case, máx 3 palabras.
- **Types**: `feat/`, `fix/`, `refactor/`, `chore/`, `docs/`, `hotfix/`.
- **Ejemplos**: `feat/export-json`, `fix/jwt-expiry`, `refactor/groq-logging`.
- **Prohibido**: `feature/`, CamelCase, espacios, nombres inventados.
- Usar `@git-branch-formatter` para generarlos.

## Commits (Git)
- **Formato**: `<type>(<scope>): <descripción en imperativo>`.
- **Types**: `feat`, `fix`, `refactor`, `chore`, `test`, `docs`, `style`, `perf`.
- **Scope común**: `auth`, `api`, `web`, `db`, `ai`, `dashboard`, `interview`, `export`, `deps`, `ci`, `config`.
- **Ejemplos**: `feat(auth): add JWT expiry to signup`, `fix(api): handle null Groq response`.
- **Regla de oro**: cada commit atómico (una sola responsabilidad).
- Usar `@git-commit-formatter` para generarlos.

## Pull Requests
- **Title**: mismo formato que commit.
- **Base**: SIEMPRE `dev`. NUNCA `main`.
- **Description**: template (qué + por qué + cómo + archivos).
- **Merge**: squash merge a `dev`.

## Archivos React (apps/web/)
- **lowercase** estricto con kebab-case (ej: `page.tsx`, `layout.tsx`, `button.tsx`).

## Componentes
- **PascalCase** (ej: `HeroSection`, `QuestionCard`, `DashboardView`, `StatCard`).

## Hooks
- **use + CamelCase** (ej: `useTheme`, `useAuthActions`, `useInterviewFlow`).

## GraphQL
- **Types**: PascalCase (ej: `User`, `AuthPayload`, `InterviewSession`).
- **Queries/Mutations**: camelCase con prefijo `GET_` / `SUBMIT_` convención (ej: `GET_DASHBOARD_STATS`, `LOGIN_MUTATION`).
- **Fields**: camelCase (ej: `questionId`, `lastAnswerContent`).

## Archivos API (apps/api/)
- **Resolvers**: `*.resolvers.ts` (ej: `auth.resolvers.ts`).
- **Data**: `*.data.ts` (ej: `interview.data.ts`).
- **Services**: `*.service.ts` (ej: `ai.service.ts`).

## Archivos DB (packages/db/)
- **Prisma schema**: `schema.prisma`.
- **Source**: `src/index.ts` (PrismaClient singleton).
