# API Design

## FIS360 - Design da API REST

---

## 1. Convencoes REST

### 1.1 Verbos HTTP

```
GET    /resources          # Listar
GET    /resources/:id      # Detalhe
POST   /resources          # Criar
PUT    /resources/:id      # Atualizar (completo)
PATCH  /resources/:id      # Atualizar (parcial)
DELETE /resources/:id      # Remover
```

### 1.2 Aninhamento

```
GET    /students/:id/workouts      # Treinos do aluno
POST   /students/:id/workouts      # Criar treino para aluno
```

### 1.3 Acoes

```
POST   /appointments/:id/confirm   # Confirmar agendamento
POST   /appointments/:id/cancel    # Cancelar agendamento
POST   /workout-templates/:id/duplicate  # Duplicar template
```

---

## 2. Formato de Resposta

### 2.1 Sucesso

```typescript
{
  "success": true,
  "data": { ... },
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "totalPages": 8
  }
}
```

### 2.2 Erro

```typescript
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados invalidos",
    "details": [
      { "field": "email", "message": "Email invalido" }
    ]
  }
}
```

### 2.3 Codigos de Erro

| Codigo | HTTP | Descricao |
|--------|------|-----------|
| VALIDATION_ERROR | 400 | Dados invalidos |
| UNAUTHORIZED | 401 | Nao autenticado |
| FORBIDDEN | 403 | Sem permissao |
| NOT_FOUND | 404 | Recurso nao encontrado |
| CONFLICT | 409 | Conflito (ex: email duplicado) |
| RATE_LIMITED | 429 | Muitas requisicoes |
| INTERNAL_ERROR | 500 | Erro interno |

---

## 3. Autenticacao

### 3.1 Headers

```
Authorization: Bearer <access_token>
X-Refresh-Token: <refresh_token>
```

### 3.2 Rotas Publicas

```
POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh
POST /api/auth/forgot-password
POST /api/auth/reset-password
```

### 3.3 Rotas Protegidas

Todas as demais rotas requerem `Authorization: Bearer <token>`

---

## 4. Rate Limiting

| Contexto | Limite |
|----------|--------|
| Global | 1000 req/min por IP |
| Auth | 10 req/min por IP |
| API | 100 req/min por usuario |
| WhatsApp | 30 msg/min por business |

---

## 5. Endpoints

### 5.1 Auth

```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh
GET    /api/auth/me
```

### 5.2 Students

```
GET    /api/students
POST   /api/students
GET    /api/students/:id
PUT    /api/students/:id
DELETE /api/students/:id
GET    /api/students/:id/workouts
GET    /api/students/:id/stats
POST   /api/students/:id/invite
POST   /api/students/import
```

### 5.3 Exercises

```
GET    /api/exercises
POST   /api/exercises
GET    /api/exercises/:id
PUT    /api/exercises/:id
DELETE /api/exercises/:id
```

### 5.4 Workout Templates

```
GET    /api/workout-templates
POST   /api/workout-templates
GET    /api/workout-templates/:id
PUT    /api/workout-templates/:id
DELETE /api/workout-templates/:id
POST   /api/workout-templates/:id/duplicate
```

### 5.5 Workouts

```
GET    /api/workouts
POST   /api/workouts
GET    /api/workouts/:id
PUT    /api/workouts/:id
DELETE /api/workouts/:id
```

### 5.6 Workout Logs

```
POST   /api/workout-logs
GET    /api/workout-logs
GET    /api/workout-logs/:id
```

### 5.7 Appointments

```
GET    /api/appointments
POST   /api/appointments
GET    /api/appointments/:id
PUT    /api/appointments/:id
POST   /api/appointments/:id/confirm
POST   /api/appointments/:id/cancel
GET    /api/appointments/availability
```

### 5.8 WhatsApp

```
POST   /api/whatsapp/instance
GET    /api/whatsapp/instance
GET    /api/whatsapp/qrcode
POST   /api/whatsapp/send
POST   /api/whatsapp/webhook
```

### 5.9 Gamification

```
GET    /api/gamification/stats
GET    /api/gamification/badges
GET    /api/gamification/leaderboard
```

### 5.10 Reports

```
GET    /api/reports/dashboard
GET    /api/reports/churn-risk
GET    /api/reports/attendance
GET    /api/reports/student/:id
```

---

## 6. Paginacao

### 6.1 Request

```
GET /api/students?page=1&limit=20&search=joao
```

### 6.2 Response Meta

```json
{
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "totalPages": 8,
    "hasNext": true,
    "hasPrev": false
  }
}
```

---

## 7. Filtros e Ordenacao

### 7.1 Filtros

```
GET /api/students?status=ACTIVE&goal=MUSCLE_GAIN
GET /api/appointments?date=2026-01-15&status=CONFIRMED
```

### 7.2 Ordenacao

```
GET /api/students?sort=name&order=asc
GET /api/students?sort=createdAt&order=desc
```

---

## 8. Versionamento

A API nao usa versionamento em URL inicialmente. Mudancas breaking serao:

1. Comunicadas com antecedencia
2. Depreciacao de campos com warnings
3. Migracao gradual

---

*Referencia: docs/architecture.md - Secao 5*
