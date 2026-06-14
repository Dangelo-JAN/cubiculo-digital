---
trigger: always_on
---

# 🗺️ Mapa de Rutas

## Rutas Públicas
| Ruta | Descripción | Componente |
|------|-------------|------------|
| `/` | Landing page | `LandingView` |
| `/login` | Inicio de sesión | `LoginView` |
| `/signup` | Registro de usuario | `SignupView` |

## Rutas Protegidas (requieren JWT cookie)
| Ruta | Descripción | Componente |
|------|-------------|------------|
| `/dashboard` | Panel de control principal | `DashboardView` |
| `/dashboard/interview` | Flujo de entrevista (11 preguntas) | `InterviewView` |

## API GraphQL
| Endpoint | Descripción |
|----------|-------------|
| `POST /graphql` | GraphQL Yoga (schema único) |
| `GET /health` | Health check (DB + Redis status) |
