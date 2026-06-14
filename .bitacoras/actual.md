# 🛠️ TAREA ACTUAL
**ID:** #002 | **Estado:** ✅ COMPLETADO | **Fecha:** 2026-06-14

---

## 🎯 OBJETIVO FINAL
> Crear la configuración agéntica completa del proyecto Cubículo Digital basada en PRD2.md y la estructura del proyecto Condominios Venezuela.

---

## 🚦 PUNTO DE CONTROL
- **Lo último que funcionó:** GitHub configurado: workflows, branch protection, labels, repo settings. dev=prod, dev-2=dev.
- **Dónde se rompió/detuvo:** N/A — tarea completada.
- **Siguiente acción inmediata:** Esperar instrucciones para siguiente tarea del backlog (F-01 JWT expiry, F-02 Secrets, etc.)

---

## 📝 CAMBIOS TÉCNICOS CLAVE
### #001 — Configuración agéntica inicial
- [x] **AGENTS.md** — Protocolo de inicio, triaje, ejecución, sincronización
- [x] **opencode.json** — Config de agentes (plan, build, code-reviewer)
- [x] **.opencode/prompts/** — build.txt + review.txt
- [x] **.agent/rules/** — Reglas de global-context, design-system, checklists, skills, workflows
- [x] **.bitacoras/** — 00-plantilla.md, index.md, actual.md
- [x] **.git-hooks/** — pre-commit + pre-push (bloqueo main/dev)

### #002 — GitHub Full Setup ✅ (recién completado)
- [x] **Workflows actualizados** — ci.yml, deploy-staging, deploy-prod, security, pr-quality para nuevo branch model
- [x] **Issue Templates** — agent-implementation, feature-implementation, bug-report
- [x] **Labels** — 25+ labels (track, priority, day, agent, meta) creadas en GitHub
- [x] **Branch Protection** — `dev` (prod: 1 approval, linear history, enforce admins) + `dev-2` (staging: 1 approval, linear history)
- [x] **Repo Settings** — squash merge only, auto-delete branches, auto-merge, issues enabled
- [x] **Sincronización** — dev→dev-2 fast-forward (ambas en commit 6c20ea7)

---

## ⚠️ NOTAS DE MEMORIA
- **Branch model:** `dev` = producción, `dev-2` = staging/desarrollo. NUNCA push directo a dev.
- **Org pendiente:** `cubiculo-digital` no existe en GitHub. Crear manualmente en github.com/settings/organizations si se desea.
- **Projects board pendiente:** Token sin scope `read:project`. Requiere auth refresh: `gh auth refresh -h github.com -s read:project,write:project` o crear manualmente.
