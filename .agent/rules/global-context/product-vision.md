---
trigger: always_on
---

# 🎯 Product Vision — Cubículo Digital

## Overview
Plataforma SaaS B2B que transforma conocimiento tácito corporativo en activos digitales estructurados ("Biblia Corporativa") mediante entrevistas guiadas por IA (Groq/Llama-3.3-70b).

**Target**: Startups, scale-ups y PYMEs que necesitan documentar conocimiento organizacional para fine-tuning de modelos de IA propios o consulta estratégica.

## User Personas
| Persona | Job-to-be-Done |
|---------|---------------|
| **Founder/CEO** | Documentar inteligencia de negocio antes de escalar o buscar financiación |
| **Head of Operations** | Tener conocimiento operacional explícito para entrenar IA interna |
| **CTO/Tech Lead** | Datos limpios para RAG o fine-tuning domain-specific |
| **HR/People Lead** | Documentar cultura organizacional de forma sistemática |

## Value Proposition
| Pilar | Descripción |
|-------|-------------|
| Extracción de Conocimiento | Entrevistas adaptativas que extraen información de alto valor sin fricción |
| Estructuración Automática | Conocimiento mapeado automáticamente por departamentos y tópicos |
| Síntesis con IA | Groq/Llama-3.3 genera análisis, pain points y plan a 90 días |
| Exportación LLM-Ready | Datos estructurados en JSON para fine-tuning (P1 backlog) |

## Diferenciación vs Alternativas
| Característica | Cubículo Digital | Consultants | Notion/Confluence | Generic LLM |
|----------------|-----------------|-------------|--------------------|-------------|
| Costo | $/mes | $$$$ | $ | $ |
| Tiempo a valor | Horas | Semanas | Días | Horas |
| Estructura automática | ✅ | ❌ | ❌ | ❌ |
| Síntesis IA estratégica | ✅ | ✅ | ❌ | ❌ |
| Export LLM-ready | P1 | ❌ | ❌ | ❌ |
| Dark mode | ✅ | N/A | ✅ | ✅ |

## Flujos de Usuario End-to-End
| Flujo | Ruta | Descripción |
|-------|------|-------------|
| Nuevo Usuario | `/` → `/signup` → JWT → `/dashboard` | Registro + login automático |
| Usuario Existente | `/` → `/login` → JWT → `/dashboard` | Login con credenciales |
| Entrevista | `/dashboard` → "Nueva Entrevista" → `/dashboard/interview` → Q1-Q11 → Feedback → Dashboard |
| Route Protection | `middleware.ts` verifica cookie JWT → redirect `/login?callbackUrl=X` si no existe |

## Glosario
| Término | Definición |
|---------|------------|
| Biblia Corporativa | Documento generado por IA (3 partes: análisis, pain points, plan 90 días) |
| Pool de Preguntas | 11 preguntas de negocio seleccionadas aleatoriamente |
| Interview Response | Respuesta individual a una pregunta del pool |
| APQ | Automatic Persisted Queries — caché GraphQL por hash SHA256 |

## Costos Operativos Estimados
| Servicio | Costo/mes | Notas |
|----------|-----------|-------|
| Groq Cloud | ~$0 (tier gratuito) | ~1000 generaciones/mes, 4K tokens c/u |
| Supabase | $0-25 (free-pro) | 500MB DB, 5GB transfer |
| Upstash Redis | $0-5 (free) | ~10K requests/día, APQ + cache |
| Vercel | $0 (pro) | Web hosting, 100GB BW |
| Sentry | $0 | Error tracking, 5K eventos/mes |
| **Total** | **$0-30/mes** | MVP stage — monitorear Groq al escalar |
