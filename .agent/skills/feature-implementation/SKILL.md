---
name: feature-implementation
description: Guía paso a paso para implementar nuevas features en Cubículo Digital. Actívala cuando inicies una tarea de tipo feat/ o feature.
---

# Feature Implementation Skill

## Ciclo de Vida Obligatorio

```
IDEA → ISSUE → BRANCH → 4-CAPAS → TEST → COMMIT → PR → MERGE
```

Ningún paso se salta. Cada uno tiene reglas estrictas.

---

## 1. Issue (antes de escribir código)

Si no existe Issue, crearlo con:
- **Title**: `[FEAT]: descripción corta` o `[FIX]: descripción`
- **Labels**: 1 priority (`p0`/`p1`/`p2`/`p3`) + 1 area (`api`/`web`/`db`/`auth`/`interview`/`ui`/`ai`/`devops`)
- **Milestone**: Asignar al correspondiente (v3.1, v3.2, etc.)
- **Criterios de aceptación**:
  ```markdown
  - [ ] comportamiento esperado A
  - [ ] comportamiento esperado B
  - [ ] Tests pasan
  - [ ] Typecheck ok
  - [ ] Sin secrets expuestos
  ```

## 2. Branch

Usar `@git-branch-formatter`. Formato obligatorio:
```
<type>/<descripcion>
# Ejemplos:
feat/export-json
fix/jwt-expiry
refactor/groq-logging
chore/ci-pipeline
```

**Prohibido**: `feature/`, CamelCase, spaces.

```bash
git checkout dev && git pull origin dev
git checkout -b feat/<descripcion>
git push origin feat/<descripcion> --set-upstream
```

## 3. Implementación — 4 Capas Obligatorias

Toda feature con datos persistentes DEBE implementar:

```
Capa 1: Schema (GraphQL type)    → apps/api/src/graphql/
Capa 2: Resolver (lógica)        → apps/api/src/graphql/modules/<area>/*.resolvers.ts
Capa 3: Query/Mutation (frontend) → apps/web/modules/<area>/*.api.ts
Capa 4: UI Component             → apps/web/views/<area>/**/*.tsx
```

**Prohibido**:
- ❌ Maquetación sin persistencia
- ❌ Endpoints sin consumir desde frontend
- ❌ Lógica de negocio en componentes UI

### Template para nuevo resolver
```typescript
import { GraphQLError } from 'graphql-yoga';
import { prisma } from '@cubiculo/db';
import { GraphQLContext } from '../../context.js';

export const resolvers = {
  Query: {
    myQuery: async (_: any, args: any, { currentUser }: GraphQLContext) => {
      if (!currentUser) throw new GraphQLError("No autorizado", {
        extensions: { code: "UNAUTHORIZED", http: { status: 401 } }
      });
      // implementar lógica
    }
  },
  Mutation: {
    myMutation: async (_: any, args: any, { currentUser }: GraphQLContext) => {
      if (!currentUser) throw new GraphQLError("No autorizado", {
        extensions: { code: "UNAUTHORIZED", http: { status: 401 } }
      });
      // validación server-side
      // lógica de negocio
      // retornar MutationResponse
    }
  }
};
```

### Template para nuevo componente
```tsx
"use client";

interface Props {
  title: string;
  onAction: () => void;
}

export const MyComponent = ({ title, onAction }: Props) => {
  return (
    <div className="bg-white dark:bg-[#111722] transition-colors duration-300">
      <h2 className="text-gray-900 dark:text-white">{title}</h2>
      <button onClick={onAction}
        className="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg">
        Action
      </button>
    </div>
  );
};
```

## 4. Testing

- Unit: resolver retorna datos cuando autenticado, lanza error cuando no
- Integration: mutation completa con response structure
- Coverage mínimo: 80% líneas nuevas, 70% ramas
- Mock externo: NO llamar APIs reales (Groq, Redis, Firebase)

### Template para test de resolver
```typescript
import { describe, it, expect, vi } from 'vitest';

describe('myNewResolver', () => {
  it('should return data when authenticated', async () => {
    const result = await myResolver.Query.myQuery(_, {}, { currentUser: { userId: '123' } });
    expect(result).toBeDefined();
  });

  it('should throw when unauthenticated', async () => {
    await expect(
      myResolver.Query.myQuery(_, {}, { currentUser: undefined })
    ).rejects.toThrow('No autorizado');
  });
});
```

## 5. Pre-commit Checklist

Antes de cada commit, verificar:
```markdown
- [ ] `pnpm exec tsc --noEmit` — 0 errors
- [ ] Tests nuevos escritos y pasando
- [ ] Dark mode implementado (si aplica UI)
- [ ] JWT expiry presente (si aplica auth)
- [ ] Sin secrets en el diff
- [ ] Sin código comentado
- [ ] Sin imports de OpenAI
- [ ] fetchPolicy explícito en nuevas queries GraphQL
- [ ] Branch name sigue convención
- [ ] PR description template seguido
```

## 6. Commit y PR

### Commit (usar `@git-commit-formatter`)
```
<type>(<scope>): <descripción en imperativo>
# Ejemplos:
feat(auth): add JWT expiry to signup and login
fix(api): handle null response from Groq service
refactor(interview): replace sort shuffle with Fisher-Yates
```

Tipos: `feat`, `fix`, `refactor`, `chore`, `test`, `docs`, `style`, `perf`
Scope común: `auth`, `api`, `web`, `db`, `ai`, `dashboard`, `interview`, `export`, `deps`, `ci`, `config`

**Regla de oro**: cada commit atómico (una sola responsabilidad).

### Pull Request
| Regla | Detalle |
|-------|---------|
| Base branch | SIEMPRE `dev`. NUNCA `main`. |
| Title | Mismo formato que commit |
| Description | Template: qué + por qué + cómo + archivos + screenshots |
| Reviewer | Auto-asignar code-reviewer |
| Merge | Squash merge a `dev` |

## 7. Referencia Rápida de Comandos

```bash
# Branch
git checkout dev && git pull origin dev
git checkout -b feat/<descripcion>

# Quality
pnpm exec tsc --noEmit
pnpm run lint
pnpm run test

# Build
pnpm run build:db && pnpm run build:api && pnpm run build:web

# Commit
git add .
git commit -m "feat(area): descripción en imperativo"
git push
```
