---
trigger: always_on
---

# ⚙️ Invariantes del Desarrollo

Reglas que TODO desarrollo debe cumplir sin excepción.

## 1. Soporte Temático Bidireccional
Todo componente DEBE soportar Light y Dark mode via Tailwind `dark:` prefix.

## 2. Responsividad
- Enfoque **desktop-first** con breakpoints: < 768px (mobile), 768-1024px (tablet), > 1024px (desktop).
- Sidebar hidden en mobile, hamburger menu implicado.

## 3. Seguridad End-to-End
- Validación de JWT estrictamente **server-side** en context.ts.
- Nunca confiar en datos del cliente para autorización.
- JWT DEBE tener `expiresIn: '1d'` — prohibido token sin expiry.

## 4. GraphQL Integrity
- Toda mutation protegida DEBE verificar `context.currentUser`.
- Errores GraphQL: nunca exponer detalles de BD en producción.
- Mutation pattern obligatorio: `throw new GraphQLError("mensaje", { extensions: { code: "UNAUTHORIZED", http: { status: 401 } } })`.

## 5. Zero Tolerance
Reglas que NO admiten excepción:
- ❌ Código comentado en producción — eliminarlo siempre.
- ❌ `console.log` en producción — usar logger estructurado.
- ❌ `import * from 'lucide-react'` — importar solo iconos específicos.
- ❌ Link a `/setup` (no existe) — debe apuntar a `/dashboard/interview`.
- ❌ Mezclar OpenAI y Groq en nombres, imports o logs — unificado a `[GROQ_*]`.
- ❌ Mutar Apollo cache manualmente — usar `refetchQueries` o `cache.modify`.
