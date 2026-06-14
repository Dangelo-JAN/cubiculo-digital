---
name: git-branch-formatter
description: Formateas los nombres de las ramas de git de acuerdo con la convención de nombres de ramas. Úselo cuando el usuario solicite crear una nueva rama.
---

# Git Branch Naming Convention

Cuando creas una nueva rama, DEBES seguir esta estructura:
`<type>/<short-description>`

# Tipos permitidos
- **feat**: Nuevas funcionalidades o módulos (e.g., `feat/dashboard-stats`).
- **fix**: Correcciones de errores (e.g., `fix/jwt-expiry`).
- **refactor**: Mejoras en el código sin nuevas funcionalidades (e.g., `refactor/ai-service`).
- **docs**: Actualizaciones de la documentación (e.g., `docs/prd-update`).
- **chore**: Mantenimiento, dependencias, o configuración (e.g., `chore/update-deps`).
- **hotfix**: Correcciones urgentes de producción.

# Instrucciones
1. **Lowercase only**: Todos los nombres de las ramas deben estar en minúsculas.
2. **Kebab-case**: Usa guiones (`-`) para separar las palabras en la descripción.
3. **Conciseness**: Mantén la descripción por debajo de 3 palabras.
4. **Context**: Si el usuario proporciona un ID de Ticket/Issue (e.g., #42), prefix the description: `<type>/#42-description`.

## Ejemplos
- `feat/export-json`
- `fix/jwt-expiration`
- `refactor/groq-logging`
- `chore/ci-pipeline`
