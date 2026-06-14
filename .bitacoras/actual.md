# 🛠️ TAREA ACTUAL
**ID:** #001 | **Estado:** ✅ COMPLETADO | **Fecha:** 2026-06-12

---

## 🎯 OBJETIVO FINAL
> Crear la configuración agéntica completa del proyecto Cubículo Digital basada en PRD2.md y la estructura del proyecto Condominios Venezuela.

---

## 🚦 PUNTO DE CONTROL
- **Lo último que funcionó:** Archivos creados: AGENTS.md, opencode.json, .opencode/, .agent/ (rules, skills, workflows), .bitacoras/, .git-hooks/, .github/workflows/.
- **Dónde se rompió/detuvo:** N/A — tarea completada.
- **Siguiente acción inmediata:** N/A — esperar nuevas instrucciones.

---

## 📝 CAMBIOS TÉCNICOS CLAVE
- [x] **AGENTS.md** — Protocolo de inicio, triaje, ejecución, sincronización
- [x] **opencode.json** — Config de agentes (plan, build, code-reviewer)
- [x] **.opencode/prompts/** — build.txt + review.txt
- [x] **.agent/rules/checklist-verify.md** — Checklist pre-flight y post-flight
- [x] **.agent/rules/global-context/** — 10 archivos (global-context, index, route-map, dev-invariants, naming, technical, accessibility, self-maintenance, api-schema, infra-deploy)
- [x] **.agent/rules/design-system/** — 5 archivos (index, colors, specs, ui-elements, lists-tables, migration-mapping)
- [x] **.agent/skills/** — git-branch-formatter + git-commit-formatter (SKILL.md)
- [x] **.agent/workflows/git-workflow.md** — Flujo Git completo
- [x] **.bitacoras/** — 00-plantilla.md, index.md, actual.md
- [x] **.git-hooks/** — pre-commit + pre-push (bloqueo main/dev)
- [x] **.github/workflows/** — check-merge-source.yml + ci.yml

---

## ⚠️ NOTAS DE MEMORIA
- *Regla:* Basado en PRD2.md como fuente de verdad del producto.
- *Regla:* Misma estructura de Condominios Venezuela pero adaptado al stack (Next.js 15, GraphQL Yoga, Prisma, Groq).
- *Regla:* Se agregaron archivos específicos: api-schema.md, infra-deploy.md.
- *Branch:* (sin rama — tarea exenta de configuración agéntica inicial)
