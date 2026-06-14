---
trigger: always_on
---

# 🗺️ Product Roadmap — Cubículo Digital

## Estado Actual (v3.0)
**Completado**: Landing + Auth, Dashboard mock, Interview flow (11 preguntas), AI feedback (Groq), Docker API, Dark/Light mode, Health check, Redis APQ.

**Known Gaps**: Dashboard stats mock (no DB), departments query inexistente, JWT sin expiry, `users` query pública, secrets en `.env`, 0 tests, 0 CI/CD, logging inconsistente, AI error handling frágil.

## Backlog Priorizado

| ID | Feature | Prioridad | Complexity | Dependencias |
|----|---------|-----------|------------|-------------|
| F-01 | 🔴 JWT expiry en signup + login | P0-critical | Baja | — |
| F-02 | 🔴 Secrets management (rotar claves) | P0-critical | Baja | — |
| F-03 | 🔴 Auth en users query | P0-critical | Baja | — |
| F-04 | 🟡 Unit tests API (auth, interview, ai) | P0 | Media | — |
| F-05 | 🟡 ESLint + Prettier + typecheck scripts | P0 | Baja | — |
| F-06 | 🟡 Unificar logging a [GROQ_*] | P0 | Baja | — |
| F-07 | 🟡 Connect dashboard stats a DB real | P0 | Media | Schema GraphQL |
| F-08 | 🟡 Retry pattern en AI service | P0 | Baja | — |
| F-09 | 🔵 Rate limiting (Upstash) | P1 | Media | — |
| F-10 | 🔵 Sentry error tracking | P1 | Baja | — |
| F-11 | 🔵 Export JSON/CSV | P1 | Alta | — |
| F-12 | 🔵 Password reset flow | P1 | Media | — |
| F-13 | 🔵 Email verification | P1 | Baja | — |
| F-14 | 🔵 Feedback viewing page | P1 | Baja | — |
| F-15 | 🔵 CI/CD pipeline (GitHub Actions) | P1 | Media | Tests |
| F-16 | 🟢 i18n (next-intl) EN/ES | P2 | Media | — |
| F-17 | 🟢 GDPR compliance | P2 | Alta | Legal review |
| F-18 | 🟢 Team collaboration (invites) | P2 | Alta | Auth roles |
| F-19 | 🟢 Analytics dashboard | P2 | Media | Feedback data |
| F-20 | 🟢 Custom question pool CRUD | P2 | Alta | — |
| F-21 | 🟢 E2E tests (Playwright) | P2 | Alta | Tests setup |
| F-22 | ⚪ SSO/SAML | P3 | Alta | — |
| F-23 | ⚪ OpenTelemetry + Grafana | P3 | Alta | — |
| F-24 | ⚪ A/B testing para preguntas | P3 | Media | — |

## Roadmap Trimestral

### Q3 2026 — Foundation
**Mes 1 (Julio)**: F-01 JWT expiry, F-02 Rotar secrets, F-03 Auth users query, F-04 Tests API, F-05 ESLint/typecheck, F-06 Logging GROQ, F-07 Dashboard stats reales

**Mes 2 (Agosto)**: F-08 Retry pattern AI, F-09 Rate limiting, F-10 Sentry, F-11 Export JSON, F-12 Password reset, F-15 CI/CD pipeline

**Mes 3 (Septiembre)**: F-13 Email verification, F-14 Feedback page, F-16 i18n EN/ES, F-17 GDPR compliance, F-21 Playwright E2E

### Q4 2026 — Scale
F-18 Team collaboration, F-19 Analytics dashboard, F-20 Custom question pool, F-22 SSO/SAML, F-23 OpenTelemetry, F-24 A/B testing
