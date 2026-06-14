---
trigger: always_on
---

# 🗄️ API Schema — GraphQL + Prisma

## GraphQL Schema (apps/api/src/graphql/index.ts)

```graphql
type User {
  id: String!
  email: String!
  name: String
}

type AuthPayload {
  token: String!
  user: User!
}

type InterviewQuestion {
  id: ID!
  title: String!
  description: String!
  department: String!
  topic: String!
}

type InterviewSession {
  id: ID!
  questions: [InterviewQuestion!]!
}

type MutationResponse {
  id: ID!
  success: Boolean!
}

type Query {
  health: String!
  me: User
  users: [User!]!           # ⚠️ REQUIERE AUTH - seguridad
  randomInterview: InterviewSession!
}

type Mutation {
  signup(name: String!, email: String!, password: String!): AuthPayload!
  login(email: String!, password: String!): AuthPayload!
  submitAnswer(content: String!, questionId: String!): MutationResponse!
  finishInterview(lastAnswerContent: String!, questionId: String!): MutationResponse!
}
```

## Prisma Schema (packages/db/prisma/schema.prisma)

```prisma
model User {
  id        String   @id @default(uuid())
  email     String   @unique
  password  String
  name      String?
  interviewResponses InterviewResponse[]
  feedback           Feedback?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Question {
  id          String   @id @default(uuid())
  title       String
  description String
  department  String
  topic       String
}

model InterviewResponse {
  id          String   @id @default(uuid())
  userId      String
  questionId  String
  content     String   @db.Text
  isCompleted Boolean  @default(false)
  user        User     @relation(fields: [userId], references: [id])
}

model Feedback {
  id        String   @id @default(uuid())
  content   String   @db.Text
  userId    String   @unique
  user      User     @relation(fields: [userId], references: [id])
  createdAt DateTime @default(now())
}
```

## Notas de Seguridad
- **JWT** DEBE tener `expiresIn: '1d'` en signup y login
- **users query** requiere `currentUser` en context — NO pública
- **submitAnswer** y **finishInterview** requieren auth
- **CORS**: solo localhost:3000 y *.vercel.app

## ⚠️ Mejoras Planificadas al Schema
| Aspecto | Estado Actual | Plan | Prioridad |
|---------|--------------|------|-----------|
| MutationResponse | `{ id, success }` | Agregar `error: String` opcional | P1 |
| Dashboard stats | No existe | Crear type `Department` + query `GetDashboardStats` | P0 |
| Export JSON/CSV | No existe | Crear mutation `exportBiblia(format: String!): ExportPayload` | P1 |
| Password reset | No existe | Crear mutations `requestPasswordReset` + `resetPassword` | P1 |
| Role enum | No en schema | Agregar `role` (ADMIN/USER) a User | P2 |
