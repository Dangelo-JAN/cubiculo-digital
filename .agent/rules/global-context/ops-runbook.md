---
trigger: always_on
---

# 🏃 Ops Runbook

## Debugging Guide

### Dashboard muestra datos hardcodeados
```
→ Verificar GET_DASHBOARD_STATS query en dashboard.api.ts
→ Schema GraphQL no tiene departments → backlog P0
```

### Groq no genera feedback
```
→ Revisar GROQ_API_KEY en .env
→ Revisar logs [GROQ_ERROR] o [GROQ_CRITICAL_ERROR]
→ Verificar rate limits de Groq Cloud (free tier: ~30 req/min)
```

### Auth no funciona
```
→ Revisar token en localStorage
→ Revisar cookie (secure:true bloquea HTTP local si no es HTTPS)
→ Revisar JWT_SECRET en .env
→ Verificar que JWT tiene expiresIn
```

### Redis connection issues
```
→ Redis down no es crítico: APQ skip cache, query DB direct
→ Verificar REDIS_URL en entorno
→ Ping manual: redis-cli ping
```

## Health Checks
| Endpoint | Formato | Propsito |
|----------|---------|----------|
| `GET /health` | HTML | Status DB + Redis |
| `POST /graphql` | GraphQL | Schema + queries |

## Rollback Procedure
```bash
# API: Re-deploy versión anterior del Docker image
docker pull cubiculo-api:<previous-tag>
docker run -d -p 4000:4000 cubiculo-api:<previous-tag>

# Web: Vercel rollback via dashboard (Inmediato, sin costo)
```

## Alertas Propuestas
| Tipo | Condición | Canal |
|------|-----------|-------|
| **Pager** | Groq API fails >5 veces en 10 min | Slack/PagerDuty |
| **Warning** | DB connections >80% pool | Slack |
| **Info** | Nueva cuenta creada, entrevista completada | Slack |
| **Cost** | Groq usage >5K generaciones/mes | Email |

## GDPR Compliance Checklist (P1)
| Requisito | Estado | Acción |
|-----------|--------|--------|
| Derecho al olvido (Art. 17) | ❌ | Implementar delete user + cascade |
| Portabilidad (Art. 20) | ❌ | Export JSON de respuestas y feedback |
| Consentimiento (Art. 7) | ❌ | Checkbox en signup + privacy link |
| Data Processing Agreement | ❌ | DPA con Supabase + Upstash |
| Breach notification | ❌ | Plan 72h |

## Data Retention
- **Respuestas activas**: mientras la cuenta exista
- **Cuentas inactivas**: 12 meses sin login → soft delete → hard delete 24 meses
- **Feedback**: mismo ciclo que respuestas
