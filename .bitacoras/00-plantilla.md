# 📋 PLANTILLA DE BITÁCORA (OBLIGATORIO SEGUIR)

> Todas las bitácoras DEBEN seguir esta estructura exacta.

```markdown
# 🛠️ TAREA: [Nombre Breve]
**ID:** #XXX | **Estado:** 🟡 EN CURSO | **Fecha:** YYYY-MM-DD

---

## 🎯 OBJETIVO FINAL
> Una frase que defina el "éxito" de esta tarea (Ej: "Que el dashboard muestre stats reales desde la DB").

---

## 🚦 PUNTO DE CONTROL (Contexto de Reanudación)
*Usa esto para "despertar" a la IA si el chat se cierra:*

- **Lo último que funcionó:** [Ej: El schema GraphQL ya tiene departments].
- **Dónde se rompió/detuvo:** [Ej: Error de conexión a Prisma en el resolver].
- **Siguiente acción inmediata:** [Ej: Revisar la query en dashboard.api.ts].

---

## 📝 CAMBIOS TÉCNICOS CLAVE
- [x] [Configuración de Schema - COMPLETADO]
- [ ] [Resolver de Dashboard - PENDIENTE]
- [ ] [UI de Stats desde DB - PENDIENTE]

---

## ⚠️ NOTAS DE MEMORIA
- *Regla:* [Regla importante a recordar para esta tarea]
- *Regla:* [Otra regla relevante]
- *Branch:* [nombre de la rama]
- *Commit:* [hash del commit si aplica]
```

---

## 📝 REGLAS DE LA PLANTILLA

| Campo | Formato | Ejemplo |
|-------|---------|---------|
| **ID** | `#001`, `#002`, etc. (secuencial) | `#001` |
| **Estado** | 🟡 EN CURSO / ✅ FINALIZADO / 🔴 BLOQUEADO | 🟡 EN CURSO |
| **Fecha** | YYYY-MM-DD | 2026-06-12 |
| **Objetivo Final** | Una sola frase que defina el éxito | "Que el dashboard muestre stats reales" |
| **Punto de Control** | Contexto para recuperación si el chat se cierra | 3 puntos: último trabajo, dónde se detuvo, siguiente acción |
| **Cambios Técnicos** | Checklist con [x] completado y [ ] pendiente | - [x] Tarea completada |
| **Notas de Memoria** | Reglas importantes, branch, commit | - Branch: feat/dashboard-stats |

---

*Esta plantilla es de cumplimiento obligatorio para todas las nuevas bitácoras.*
