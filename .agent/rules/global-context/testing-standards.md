---
trigger: always_on
---

# 🧪 Testing Standards

## Estrategia General
| Tipo | Framework | Cobertura Target | Prioridad |
|------|-----------|------------------|-----------|
| Unit (API) | Vitest | ≥ 80% lines | P0 |
| Unit (Web) | Vitest + RTL | ≥ 70% lines | P1 |
| Integration (API) | Vitest + Supertest | ≥ 90% critical paths | P1 |
| E2E | Playwright | 3 flujos críticos | P2 |
| Linting | ESLint + Prettier | — | P0 |
| Type Checking | `tsc --noEmit` | — | P0 |

## Reglas para Nuevas Features
1. **Toda feature DEBE incluir tests**: unit (resolver/service) + integration (API)
2. **Coverage mínimo**: 80% líneas nuevas, 70% ramas
3. **Test file location**: `__tests__/` junto al archivo que testea
4. **Naming**: `<archivo>.test.ts` (ej: `auth.resolvers.test.ts`)
5. **Mock externo**: Mockear Groq, Redis, firebase — NO llamar APIs reales

## Tests Críticos (Prioridad Máxima)
| # | Test | Archivo target | Por qué |
|---|------|----------------|---------|
| T-01 | Auth: signup crea usuario con hash | `auth.resolvers.ts` | Seguridad |
| T-02 | Auth: login valida contraseña | `auth.resolvers.ts` | Seguridad |
| T-03 | Auth: JWT expiry se respeta | `auth.resolvers.ts` | Seguridad |
| T-04 | Interview: submitAnswer persiste | `interview.resolvers.ts` | Core feature |
| T-05 | Interview: finishInterview transaction | `interview.resolvers.ts` | Data integrity |
| T-06 | AI: retry pattern 3 intentos | `ai.service.ts` | Robustez |
| T-07 | AI: logging consistente `[GROQ_*]` | `ai.service.ts` | Observabilidad |
| T-08 | Middleware: redirect sin cookie | `middleware.ts` | Seguridad |
| T-09 | E2E: signup → login → dashboard | Playwright | Flujo crítico |
| T-10 | E2E: questions → submit → finish | Playwright | Flujo crítico |

## Comandos
```bash
pnpm run test              # Todos los tests
pnpm run test:coverage     # Con reporte de cobertura
pnpm run test:e2e          # Playwright E2E
pnpm exec tsc --noEmit     # Type check
pnpm run lint              # Linting
pnpm run ci                # typecheck + lint + test + build
```
