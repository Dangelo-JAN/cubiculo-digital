---
trigger: always_on
---

# 🧹 Technical Debt Registry

## Deuda Gobernada
| ID | Archivo | Problema | Plan | Due |
|----|---------|----------|------|-----|
| D-01 | `apps/api/src/schema.ts` | Legacy, deprecated | Eliminar (Fase 7) | v3.5 |
| D-02 | `apps/api/src/context.ts` | Vacío, no usado | Eliminar (Fase 7) | v3.5 |
| D-03 | `apps/api/src/resolvers/health.ts` | Vacío, no usado | Eliminar (Fase 7) | v3.5 |
| D-04 | `apps/web/views/dashboard/DashboardPageView.tsx:37` | Link a `/setup` (no existe) | Corregir a `/dashboard/interview` (Fase 4) | v3.1 |
| D-05 | `apps/api/src/graphql/modules/interview/interview.resolvers.ts:12` | Shuffle con `.sort()` en vez de Fisher-Yates | Refactorizar (Fase 5) | v3.2 |
| D-06 | `.env` | Secrets en texto plano | Migrar a secrets manager (Fase 0) | Inmediato |
| D-07 | `README.md` | Template genérico de create-next-app | Reescribir (Fase 6) | v3.1 |
| D-08 | `package.json` | Sin scripts de test/lint/typecheck | Agregar (Fase 2) | v3.1 |
| D-09 | Logging AI | Mezcla prefijos `OPENAI_*`/`GROQ_*` | Unificar a `[GROQ_*]` (Fase 0) | v3.1 |

## Errores Conocidos (Cosméticos)
| ID | Archivo | Error | Fix |
|----|---------|-------|-----|
| B-01 | `SignupPageView.tsx:58` | Botón de submit dice "Login" | Cambiar a "Crear cuenta" |
| B-02 | `LoginPageView.tsx:44` | Texto "Login in..." (typo) | Cambiar a "Iniciando sesión..." |
| B-03 | `LoginPageView.tsx:17` / `SignupPageView.tsx:20` | Títulos en inglés | Estandarizar a español |

## Inconsistencia Dark Mode
| Color | Ocurrencias | Archivos |
|-------|-------------|----------|
| `#0b1220` | Sidebar, cards | Header.tsx, Sidebar.tsx |
| `#101622` | Body | layout.tsx |
| `#111722` | Cards | DashboardView, StatCard |
| `#0b101a` | Input backgrounds | Input.tsx |

**✅ Target de unificación**: body `#101622`, cards `#111722`, input bg `#0b101a`, borders `#232f48`.

## Dependencias Problemáticas
| ID | Archivo | Problema | Fix |
|----|---------|----------|-----|
| PKG-01 | Root `package.json` | `next`, `react`, `react-dom` duplicados de web/ | Mover solo a `apps/web/` |
| PKG-02 | Root `package.json` | `graphql`, `graphql-yoga` duplicados de api/ | Mover solo a `apps/api/` |
| PKG-03 | `apps/web/package.json` | `@envelop/core` mal ubicado | Mover a `apps/api/` |
| PKG-04 | `apps/api/package.json` | `openai` como dep (no se usa) | Eliminar |
