---
trigger: always_on
---

# 🛠️ Reglas Técnicas

## 1. Validación de Formularios
- Validación server-side en resolvers GraphQL.
- Frontend: validación básica (email format, password min 6 chars, name not empty).

## 2. GraphQL Resolvers
- Toda mutation DEBE verificar `currentUser` del context.
- Errores: lanzar `Error("mensaje en español")` — el frontend captura y muestra.
- Transactions: usar `prisma.$transaction` para operaciones atómicas.

## 3. Fullstack Integrity Check (4 Capas)
**Regla obligatoria — No negociable:**
Toda funcionalidad con datos persistentes DEBE implementar 4 capas:
```
Capa 1: Schema (GraphQL type)    → Schema (donde exista: index.ts o schema.graphql)
Capa 2: Resolver (lógica)        → modules/<area>/*.resolvers.ts
Capa 3: Query/Mutation (frontend) → modules/<area>/*.api.ts
Capa 4: UI Component             → views/<area>/**/*.tsx
```

**Prohibido**:
- ❌ Maquetación sin persistencia
- ❌ Endpoints sin consumir desde frontend
- ❌ Lógica de negocio en componentes UI

## 4. AI Service (Groq)
- Usar modelo `llama-3.3-70b-versatile` — no cambiar sin aprobación.
- Retry pattern: 3 intentos con exponential backoff (1s, 2s, 4s). Timeout: 30s por llamado.
- Logs con prefijo `[GROQ_*]` — NUNCA `[OPENAI_*]`.
- Fallback: mensaje amigable al usuario + guardar en cola de reproceso si falla.
- **Prohibido** llamar Groq directamente desde resolvers — siempre via `ai.service.ts`.

## 5. Caché
- Redis APQ: TTL 24h, key `apq:${sha256(query)}`.
- localStorage: entrevista persiste pregunta por pregunta (`interview_q_${id}`, `interview_step`).
- Toda nueva query DEBE especificar `fetchPolicy` explícitamente:

| Tipo de Query | fetchPolicy | Razón |
|---------------|-------------|-------|
| Datos de dashboard | `cache-and-network` → `cache-first` | Cambian con frecuencia media |
| Datos de usuario (me) | `cache-first` → `cache-and-network` | Cambian poco |
| Datos aleatorios (randomInterview) | `network-only` | Necesita fresh data siempre |
| Mutaciones | No aplica (always network) | — |

## 6. Dark Mode
- Inline script en `<head>` para anti-flash.
- ThemeProvider + useTheme hook.
- Tailwind `dark:` prefix para estilos.
- `transition-colors duration-300` en elementos que cambien bg/fg.

## 7. Testing Rules
- Toda nueva feature DEBE incluir tests: unit (resolver/service) + integration (API).
- Coverage mínimo: 80% líneas nuevas, 70% ramas.
- Test file location: `__tests__/` junto al archivo que testea.
- Naming: `<archivo>.test.ts` (ej: `auth.resolvers.test.ts`).
- Mock externo: Mockear Groq, Redis — NO llamar APIs reales.

## 8. Prohibiciones Absolutas (Zero Tolerance)
| # | Prohibición | Alternativa |
|---|-------------|-------------|
| Z-01 | Usar `any` en TypeScript | Tipar correctamente o usar `unknown` + type guard |
| Z-02 | Mezclar OpenAI con Groq (nombres, SDKs, logs) | Usar solo Groq SDK. Prefijo `[GROQ_*]` siempre |
| Z-03 | Dejar código comentado en archivos de producción | Eliminar. Usar git history como referencia |
| Z-04 | Usar `console.log` en producción | Usar logger estructurado (pino/winston) |
| Z-05 | Mutar estado de Apollo cache manualmente | Usar `refetchQueries` o `cache.modify` |
| Z-06 | Importar todo Lucide (`import * from 'lucide-react'`) | Importar solo iconos específicos |
| Z-07 | Dejar `/setup` como link roto | Siempre verificar rutas antes de commit |
| Z-08 | Llamar a `prisma` sin verificar auth primero | Verificar `currentUser` antes de cualquier query |
| Z-09 | Hacer commits directos a `main` o `dev` | Rama de feature + PR a `dev`
