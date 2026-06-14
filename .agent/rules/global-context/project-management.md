---
trigger: always_on
---

# 📋 GitHub Project Management

## Estructura del Proyecto
```
GitHub Project: Cubículo Digital v3 — "Biblia Corporativa"
├── Milestones (5)
├── Epics (9)
├── Labels (15+)
└── Views: Board (Kanban) + Timeline + Table
```

## Milestones
| Milestone | Focus | Fecha |
|-----------|-------|-------|
| 🚨 v3.0.1 — Security Hotfix | Fase 0 (SEC-01 a SEC-03) | 1 día |
| 🏗️ v3.1 — Security & Foundation | Fases 0-1-2 | Jul 2026 |
| 📊 v3.2 — Data & Dashboard | Fases 3-4-5 | Aug 2026 |
| 🚀 v3.3 — Export & Features | Fase 6-7-9 | Sep 2026 |
| 🏢 v3.4 — Enterprise Prep | Fase 8 + F-18 a F-21 | Q4 2026 |

## Epics
| Epic | Fases | Descripción |
|------|-------|-------------|
| EPIC-1 | Security Hardening | Fase 0 |
| EPIC-2 | Testing Infrastructure | Fase 2 |
| EPIC-3 | CI/CD Pipeline | Fase 3 |
| EPIC-4 | Frontend Architecture | Fase 4 |
| EPIC-5 | API Robustez | Fase 5 |
| EPIC-6 | Documentation | Fase 6 |
| EPIC-7 | Code Cleanup | Fase 7 |
| EPIC-8 | Monitoring | Fase 8 |
| EPIC-9 | Product Features | Fase 9 |

## Labels
| Categoría | Labels |
|-----------|--------|
| **Priority** | `p0-critical`, `p0`, `p1`, `p2`, `p3` |
| **Type** | `bug`, `enhancement`, `feature`, `tech-debt`, `security`, `docs`, `test`, `ci/cd` |
| **Area** | `api`, `web`, `db`, `devops`, `ui`, `auth`, `interview`, `ai` |
| **Status** | `blocked`, `in-progress`, `review`, `done` |

## Issue Templates

### Bug Report
```markdown
**Descripción:**
**Pasos para reproducir:**
**Comportamiento esperado:**
**Comportamiento actual:**
**Entorno:** (URL, browser, OS)
**Logs/Capturas:**
```

### Feature Request
```markdown
**Descripción:**
**User Story:** Como [rol], quiero [acción] para [beneficio].
**Criterios de aceptación:**
- [ ] ...
**Impacto en DB/API/UI:**
```

## Definition of Done (DoD)
Checklist obligatorio en cada PR:
- [ ] Tests nuevos escritos y pasando
- [ ] `pnpm exec tsc --noEmit` — 0 errors
- [ ] Dark mode implementado (si aplica UI)
- [ ] Sin secrets expuestos en el diff
- [ ] Changelog actualizado (si aplica)
