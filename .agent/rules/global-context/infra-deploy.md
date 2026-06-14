---
trigger: always_on
---

# 🚀 Infraestructura y Deploy

## Runtime
| Componente | Versión | Notas |
|------------|---------|-------|
| Node.js | 20.x LTS | engines en package.json |
| pnpm | 10.28.1 | packageManager requerido |
| PostgreSQL | Supabase (v15+) | Pooled + Direct URLs |
| Redis | Upstash (v7+) | Serverless, APQ + query cache |

## Docker (API only)
- Multi-stage build: node:20 builder + node:20 runner
- Stage 1: pnpm install —frozen-lockfile → generate Prisma → build API
- Stage 2: openssl + prisma migrate deploy → node apps/api/dist/index.js
- Expone puerto 4000

## Variables de Entorno Críticas
| Variable | Requerido | ⚠️ Nota |
|----------|-----------|---------|
| DATABASE_URL | ✅ | Supabase pooled — NO comitear |
| DIRECT_URL | ✅ | Supabase direct — NO comitear |
| JWT_SECRET | ✅ | NO default en prod |
| GROQ_API_KEY | ✅ | Groq Cloud — NO comitear |
| REDIS_URL | Prod | Upstash — solo prod |
| NODE_ENV | No | development/production |
| HEALTHCHECK_DB | No | true/false |

## ⚠️ Seguridad de Secrets
- **PROHIBIDO** comitear `.env` con valores reales
- Usar `.env.example` con placeholders
- En prod: GitHub Secrets / Vercel Environment Variables / Doppler

## Deploy Targets
- **API**: Docker container (servidor propio o Railway/Render)
- **Web**: Vercel (presunto por configuración CORS)

## CI/CD Pipeline (GitHub Actions)
| Workflow | Trigger | Jobs |
|----------|---------|------|
| PR Quality Gate | `pull_request` → `dev` | typecheck → lint → test → build |
| Deploy API Staging | `push` → `dev` | Build Docker → deploy staging |
| Deploy API Production | `push` → `main` | Build Docker → deploy production |
| Deploy Web | `push` → `main` | Build Next.js → deploy Vercel |
| Security Scan | weekly cron | `npm audit`, `trivy`, `gitleaks` |

## Health Check
- `GET /health` → HTML con DB + Redis status
- Respeta `HEALTHCHECK_DB=false` para ambientes serverless
- A futuro: health endpoint JSON para monitoreo programático
