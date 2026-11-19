# Arquitetura Tecnica

## FIS360 - Plataforma Inteligente de Gestao Fitness

**Versao:** 1.0
**Data:** 06/01/2026
**Status:** Aprovado

---

## 1. Visao Geral

### 1.1 Arquitetura de Alto Nivel

```
┌─────────────────────────────────────────────────────────────────────────┐
│                              CLIENTES                                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐             │
│   │  Dashboard   │    │   App Aluno  │    │   WhatsApp   │             │
│   │   (Next.js)  │    │    (PWA)     │    │   (Mobile)   │             │
│   └──────┬───────┘    └──────┬───────┘    └──────┬───────┘             │
│          │                   │                   │                      │
└──────────┼───────────────────┼───────────────────┼──────────────────────┘
           │                   │                   │
           ▼                   ▼                   ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                              NGINX                                       │
│                     (Reverse Proxy + SSL + Rate Limiting)                │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
           ┌───────────────────┼───────────────────┐
           ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│    API Server   │ │   Web Server    │ │  Evolution API  │
│   (Express.js)  │ │   (Next.js)     │ │   (WhatsApp)    │
│    Port 3001    │ │    Port 3000    │ │    Port 8080    │
└────────┬────────┘ └─────────────────┘ └────────┬────────┘
         │                                       │
         ▼                                       │
┌─────────────────┐                              │
│     Worker      │◄─────────────────────────────┘
│    (BullMQ)     │
└────────┬────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                           DATA LAYER                                     │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐             │
│   │  PostgreSQL  │    │    Redis     │    │   AWS S3     │             │
│   │   (Data)     │    │   (Cache)    │    │  (Storage)   │             │
│   └──────────────┘    └──────────────┘    └──────────────┘             │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### 1.2 Principios Arquiteturais

1. **Monorepo**: Codigo compartilhado entre API e Web
2. **API-First**: Backend desacoplado do frontend
3. **Multi-tenancy**: Isolamento de dados por Business
4. **Stateless**: API sem estado para escalabilidade
5. **Event-Driven**: Filas para operacoes async

---

## 2. Stack Tecnologico

### 2.1 Backend

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Node.js | 20 LTS | Runtime |
| Express.js | 4.x | Framework HTTP |
| TypeScript | 5.x | Tipagem estatica |
| Prisma | 5.x | ORM |
| PostgreSQL | 15 | Banco de dados |
| Redis | 7 | Cache e filas |
| BullMQ | 5.x | Job queue |
| Zod | 3.x | Validacao |
| JWT | - | Autenticacao |

### 2.2 Frontend - Dashboard

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Next.js | 14 | Framework React |
| React | 18 | UI Library |
| TypeScript | 5.x | Tipagem estatica |
| TailwindCSS | 3.x | Styling |
| shadcn/ui | - | Componentes |
| React Query | 5.x | Data fetching |
| React Hook Form | 7.x | Formularios |
| Zustand | 4.x | Estado global |

### 2.3 Frontend - App do Aluno

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Next.js | 14 | PWA |
| React | 18 | UI Library |
| TailwindCSS | 3.x | Styling |
| Workbox | 7.x | Service Worker |
| IndexedDB | - | Offline storage |

### 2.4 Infraestrutura

| Tecnologia | Proposito |
|------------|-----------|
| Docker | Containerizacao |
| Docker Compose | Orquestracao local |
| Nginx | Reverse proxy |
| Let's Encrypt | SSL |
| GitHub Actions | CI/CD |

### 2.5 Servicos Externos

| Servico | Proposito |
|---------|-----------|
| Evolution API | WhatsApp |
| AWS S3 / Cloudflare R2 | Storage |
| Bunny CDN | Video streaming |
| Stripe / PagSeguro | Pagamentos |
| Resend | Email transacional |

---

## 3. Estrutura do Monorepo

```
fis360/
├── apps/
│   ├── api/                      # Backend Express
│   │   ├── src/
│   │   │   ├── config/           # Configuracoes
│   │   │   │   ├── env.ts
│   │   │   │   ├── database.ts
│   │   │   │   └── redis.ts
│   │   │   ├── modules/          # Modulos de dominio
│   │   │   │   ├── auth/
│   │   │   │   │   ├── auth.controller.ts
│   │   │   │   │   ├── auth.service.ts
│   │   │   │   │   ├── auth.routes.ts
│   │   │   │   │   ├── auth.schema.ts
│   │   │   │   │   └── auth.types.ts
│   │   │   │   ├── users/
│   │   │   │   ├── businesses/
│   │   │   │   ├── students/
│   │   │   │   ├── professionals/
│   │   │   │   ├── exercises/
│   │   │   │   ├── workouts/
│   │   │   │   ├── appointments/
│   │   │   │   ├── assessments/
│   │   │   │   ├── gamification/
│   │   │   │   ├── notifications/
│   │   │   │   ├── whatsapp/
│   │   │   │   └── reports/
│   │   │   ├── middlewares/
│   │   │   │   ├── auth.middleware.ts
│   │   │   │   ├── tenant.middleware.ts
│   │   │   │   ├── error.middleware.ts
│   │   │   │   └── rate-limit.middleware.ts
│   │   │   ├── jobs/             # Background jobs
│   │   │   │   ├── notifications.job.ts
│   │   │   │   ├── whatsapp.job.ts
│   │   │   │   └── churn.job.ts
│   │   │   ├── utils/
│   │   │   │   ├── logger.ts
│   │   │   │   ├── response.ts
│   │   │   │   └── helpers.ts
│   │   │   ├── app.ts
│   │   │   ├── server.ts
│   │   │   └── worker.ts
│   │   ├── prisma/
│   │   │   ├── schema.prisma
│   │   │   ├── seed.ts
│   │   │   └── migrations/
│   │   ├── tests/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   ├── web/                      # Dashboard Next.js
│   │   ├── src/
│   │   │   ├── app/
│   │   │   │   ├── (auth)/
│   │   │   │   │   ├── login/
│   │   │   │   │   ├── register/
│   │   │   │   │   └── layout.tsx
│   │   │   │   ├── (dashboard)/
│   │   │   │   │   ├── layout.tsx
│   │   │   │   │   ├── page.tsx           # Dashboard
│   │   │   │   │   ├── alunos/
│   │   │   │   │   │   ├── page.tsx       # Lista
│   │   │   │   │   │   ├── novo/page.tsx  # Criar
│   │   │   │   │   │   └── [id]/
│   │   │   │   │   │       ├── page.tsx   # Perfil
│   │   │   │   │   │       └── editar/page.tsx
│   │   │   │   │   ├── treinos/
│   │   │   │   │   ├── exercicios/
│   │   │   │   │   ├── agenda/
│   │   │   │   │   ├── relatorios/
│   │   │   │   │   └── configuracoes/
│   │   │   │   └── api/                   # Route handlers
│   │   │   ├── components/
│   │   │   │   ├── ui/                    # shadcn components
│   │   │   │   ├── forms/
│   │   │   │   ├── tables/
│   │   │   │   ├── charts/
│   │   │   │   └── layout/
│   │   │   ├── hooks/
│   │   │   ├── lib/
│   │   │   │   ├── api.ts                 # API client
│   │   │   │   ├── auth.ts
│   │   │   │   └── utils.ts
│   │   │   ├── stores/
│   │   │   └── types/
│   │   ├── public/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── tailwind.config.js
│   │
│   └── student-app/              # App do Aluno (PWA)
│       ├── src/
│       │   ├── app/
│       │   │   ├── (app)/
│       │   │   │   ├── layout.tsx
│       │   │   │   ├── page.tsx           # Home
│       │   │   │   ├── treino/
│       │   │   │   ├── evolucao/
│       │   │   │   ├── agenda/
│       │   │   │   └── perfil/
│       │   │   └── login/
│       │   ├── components/
│       │   ├── hooks/
│       │   ├── lib/
│       │   └── stores/
│       ├── public/
│       │   └── manifest.json
│       ├── Dockerfile
│       └── package.json
│
├── packages/
│   └── shared/                   # Codigo compartilhado
│       ├── src/
│       │   ├── types/            # Tipos TypeScript
│       │   │   ├── api.ts
│       │   │   ├── models.ts
│       │   │   └── index.ts
│       │   ├── constants/
│       │   ├── utils/
│       │   └── validators/
│       ├── package.json
│       └── tsconfig.json
│
├── docker/
│   ├── nginx/
│   │   ├── nginx.conf
│   │   └── conf.d/
│   └── postgres/
│       └── init.sql
│
├── docs/                         # Documentacao
│   ├── project-brief.md
│   ├── prd.md
│   ├── front-end-spec.md
│   ├── architecture.md
│   ├── prd/                      # PRD shardado
│   ├── architecture/             # Arquitetura shardada
│   └── stories/                  # User stories
│
├── docker-compose.yml            # Desenvolvimento
├── docker-compose.prod.yml       # Producao
├── package.json                  # Root package
├── pnpm-workspace.yaml
├── turbo.json                    # Turborepo config
└── .env.example
```

---

## 4. Banco de Dados

### 4.1 Schema Prisma (Resumo)

```prisma
// Modelos principais - Ver schema completo em prisma/schema.prisma

// Multi-tenancy
model Business {
  id        String   @id @default(cuid())
  name      String
  slug      String   @unique
  type      BusinessType
  // ... demais campos

  users     User[]
  students  Student[]
  // ... demais relacoes
}

// Usuario do sistema
model User {
  id           String   @id @default(cuid())
  businessId   String
  email        String
  passwordHash String
  role         UserRole

  business     Business @relation(...)
  student      Student?
  professional Professional?

  @@unique([businessId, email])
}

// Aluno
model Student {
  id         String   @id @default(cuid())
  userId     String   @unique
  businessId String
  name       String
  email      String
  phone      String
  goals      GoalType[]

  // Gamificacao
  totalPoints   Int @default(0)
  currentStreak Int @default(0)
  level         Int @default(1)

  // Relacoes
  workouts     Workout[]
  assessments  Assessment[]
  // ...
}

// Exercicio
model Exercise {
  id          String   @id @default(cuid())
  businessId  String?  // null = global
  name        String
  category    ExerciseCategory
  videoUrl    String?
  // ...
}

// Template de Treino
model WorkoutTemplate {
  id          String   @id @default(cuid())
  businessId  String
  name        String
  type        WorkoutType
  exercises   WorkoutTemplateExercise[]
}

// Treino Prescrito
model Workout {
  id         String   @id @default(cuid())
  studentId  String
  templateId String?
  name       String
  exercises  WorkoutExercise[]
  logs       WorkoutLog[]
}
```

### 4.2 Estrategia de Indices

```sql
-- Indices para multi-tenancy
CREATE INDEX idx_students_business ON students(business_id);
CREATE INDEX idx_workouts_student ON workouts(student_id);
CREATE INDEX idx_appointments_business_date ON appointments(business_id, date);

-- Indices para busca
CREATE INDEX idx_students_name ON students USING gin(name gin_trgm_ops);
CREATE INDEX idx_exercises_name ON exercises USING gin(name gin_trgm_ops);

-- Indices para performance
CREATE INDEX idx_workout_logs_date ON workout_logs(date);
CREATE INDEX idx_checkins_date ON checkins(checkin_at);
```

### 4.3 Migrations

```bash
# Criar migration
pnpm --filter api prisma migrate dev --name add_gamification

# Aplicar em producao
pnpm --filter api prisma migrate deploy

# Reset (dev only)
pnpm --filter api prisma migrate reset
```

---

## 5. API Design

### 5.1 Convencoes REST

```
VERBOS:
GET    /resources          # Listar
GET    /resources/:id      # Detalhe
POST   /resources          # Criar
PUT    /resources/:id      # Atualizar (completo)
PATCH  /resources/:id      # Atualizar (parcial)
DELETE /resources/:id      # Remover

ANINHAMENTO:
GET    /students/:id/workouts      # Treinos do aluno
POST   /students/:id/workouts      # Criar treino para aluno

ACOES:
POST   /appointments/:id/confirm   # Confirmar agendamento
POST   /appointments/:id/cancel    # Cancelar agendamento
```

### 5.2 Formato de Resposta

```typescript
// Sucesso
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

// Erro
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

### 5.3 Autenticacao

```typescript
// Headers
Authorization: Bearer <access_token>
X-Refresh-Token: <refresh_token>

// Rotas publicas
POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh
POST /api/auth/forgot-password
POST /api/auth/reset-password

// Rotas protegidas
GET /api/auth/me
// ... todas as outras rotas
```

### 5.4 Rate Limiting

```
LIMITES:
- Global: 1000 req/min por IP
- Auth: 10 req/min por IP
- API: 100 req/min por usuario
- WhatsApp: 30 msg/min por business
```

### 5.5 Endpoints Principais

```
AUTH:
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh
GET    /api/auth/me

STUDENTS:
GET    /api/students
POST   /api/students
GET    /api/students/:id
PUT    /api/students/:id
DELETE /api/students/:id
GET    /api/students/:id/workouts
GET    /api/students/:id/stats
POST   /api/students/:id/invite

EXERCISES:
GET    /api/exercises
POST   /api/exercises
GET    /api/exercises/:id
PUT    /api/exercises/:id
DELETE /api/exercises/:id

WORKOUT-TEMPLATES:
GET    /api/workout-templates
POST   /api/workout-templates
GET    /api/workout-templates/:id
PUT    /api/workout-templates/:id
DELETE /api/workout-templates/:id
POST   /api/workout-templates/:id/duplicate

WORKOUTS:
GET    /api/workouts
POST   /api/workouts
GET    /api/workouts/:id
PUT    /api/workouts/:id
DELETE /api/workouts/:id

WORKOUT-LOGS:
POST   /api/workout-logs
GET    /api/workout-logs

APPOINTMENTS:
GET    /api/appointments
POST   /api/appointments
GET    /api/appointments/:id
PUT    /api/appointments/:id
POST   /api/appointments/:id/confirm
POST   /api/appointments/:id/cancel
GET    /api/appointments/availability

WHATSAPP:
POST   /api/whatsapp/instance
GET    /api/whatsapp/instance
GET    /api/whatsapp/qrcode
POST   /api/whatsapp/send
POST   /api/whatsapp/webhook

GAMIFICATION:
GET    /api/gamification/stats
GET    /api/gamification/badges
GET    /api/gamification/leaderboard

REPORTS:
GET    /api/reports/dashboard
GET    /api/reports/churn-risk
GET    /api/reports/attendance
```

---

## 6. Autenticacao e Autorizacao

### 6.1 Fluxo de Autenticacao

```
1. LOGIN:
   Cliente -> POST /api/auth/login {email, password}
   Servidor -> Valida credenciais
   Servidor -> Gera access_token (JWT, 24h) + refresh_token (30d)
   Servidor -> Salva refresh_token no Redis
   Servidor -> Retorna tokens

2. REQUESTS:
   Cliente -> Request com Authorization: Bearer <access_token>
   Middleware -> Valida JWT
   Middleware -> Extrai userId e businessId
   Middleware -> Injeta no request

3. REFRESH:
   Cliente -> POST /api/auth/refresh {refresh_token}
   Servidor -> Valida refresh_token no Redis
   Servidor -> Gera novos tokens
   Servidor -> Invalida token antigo
   Servidor -> Retorna novos tokens

4. LOGOUT:
   Cliente -> POST /api/auth/logout
   Servidor -> Remove refresh_token do Redis
```

### 6.2 JWT Payload

```typescript
interface JWTPayload {
  userId: string;
  businessId: string;
  role: UserRole;
  iat: number;
  exp: number;
}
```

### 6.3 Middleware de Autorizacao

```typescript
// auth.middleware.ts
export const requireAuth = async (req, res, next) => {
  const token = extractToken(req);
  if (!token) return res.status(401).json({ error: 'Unauthorized' });

  const payload = verifyJWT(token);
  req.user = payload;
  next();
};

// role.middleware.ts
export const requireRole = (...roles: UserRole[]) => {
  return (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    next();
  };
};

// tenant.middleware.ts
export const injectTenant = (req, res, next) => {
  // Todas as queries filtram por businessId automaticamente
  req.businessId = req.user.businessId;
  next();
};
```

### 6.4 Matriz de Permissoes

| Recurso | OWNER | MANAGER | PROFESSIONAL | RECEPTIONIST |
|---------|-------|---------|--------------|--------------|
| Students CRUD | Full | Full | Own | Read |
| Exercises | Full | Full | Read | - |
| Workouts | Full | Full | Own | - |
| Appointments | Full | Full | Own | Full |
| Reports | Full | Full | Own | - |
| Settings | Full | Partial | - | - |
| Users | Full | Read | - | - |
| Billing | Full | - | - | - |

---

## 7. Multi-tenancy

### 7.1 Estrategia

- **Abordagem**: Shared database, shared schema
- **Isolamento**: Por businessId em todas as tabelas
- **Enforcement**: Middleware + Prisma extensions

### 7.2 Implementacao Prisma

```typescript
// prisma.ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient().$extends({
  query: {
    $allModels: {
      async findMany({ args, query, model }) {
        // Injeta businessId automaticamente
        if (hasBusinessId(model)) {
          args.where = { ...args.where, businessId: getCurrentBusinessId() };
        }
        return query(args);
      },
      async create({ args, query, model }) {
        if (hasBusinessId(model)) {
          args.data.businessId = getCurrentBusinessId();
        }
        return query(args);
      },
      // ... outros metodos
    },
  },
});
```

### 7.3 Contexto de Tenant

```typescript
// Usando AsyncLocalStorage para contexto
import { AsyncLocalStorage } from 'async_hooks';

interface TenantContext {
  businessId: string;
  userId: string;
}

export const tenantStorage = new AsyncLocalStorage<TenantContext>();

// Middleware
export const tenantMiddleware = (req, res, next) => {
  const context = { businessId: req.user.businessId, userId: req.user.userId };
  tenantStorage.run(context, () => next());
};
```

---

## 8. Cache e Performance

### 8.1 Estrategia de Cache

```
REDIS CACHE:
- Sessions: 30 dias
- Refresh tokens: 30 dias
- API responses: 5 minutos (invalidacao por evento)
- Leaderboard: 1 minuto
- Dashboard stats: 5 minutos

BROWSER CACHE:
- Assets estaticos: 1 ano (hashed)
- API GET: no-cache (SWR no client)
- Imagens: 1 dia
```

### 8.2 Invalidacao de Cache

```typescript
// cache.service.ts
export class CacheService {
  private redis: Redis;

  async get<T>(key: string): Promise<T | null> {
    const data = await this.redis.get(key);
    return data ? JSON.parse(data) : null;
  }

  async set(key: string, data: any, ttl: number): Promise<void> {
    await this.redis.setex(key, ttl, JSON.stringify(data));
  }

  async invalidate(pattern: string): Promise<void> {
    const keys = await this.redis.keys(pattern);
    if (keys.length) await this.redis.del(...keys);
  }

  // Invalidar cache do aluno quando atualizar
  async invalidateStudent(studentId: string): Promise<void> {
    await this.invalidate(`student:${studentId}:*`);
    await this.invalidate(`business:*:students`);
  }
}
```

### 8.3 Database Optimization

```typescript
// Paginacao cursor-based para listas grandes
async getStudents(cursor?: string, limit = 20) {
  return prisma.student.findMany({
    take: limit + 1,
    cursor: cursor ? { id: cursor } : undefined,
    orderBy: { createdAt: 'desc' },
    skip: cursor ? 1 : 0,
  });
}

// Eager loading para evitar N+1
async getStudentWithWorkouts(id: string) {
  return prisma.student.findUnique({
    where: { id },
    include: {
      workouts: {
        include: {
          exercises: {
            include: { exercise: true }
          }
        }
      }
    }
  });
}
```

---

## 9. Background Jobs

### 9.1 Arquitetura de Filas

```
FILAS:
├── notifications     # Notificacoes push/email
├── whatsapp         # Mensagens WhatsApp
├── reports          # Geracao de relatorios
├── churn            # Analise de churn
└── maintenance      # Tarefas de manutencao
```

### 9.2 Implementacao BullMQ

```typescript
// queues/index.ts
import { Queue } from 'bullmq';
import { redis } from '../config/redis';

export const notificationQueue = new Queue('notifications', { connection: redis });
export const whatsappQueue = new Queue('whatsapp', { connection: redis });

// jobs/notifications.job.ts
import { Worker } from 'bullmq';

const worker = new Worker('notifications', async (job) => {
  switch (job.name) {
    case 'appointment-reminder':
      await sendAppointmentReminder(job.data);
      break;
    case 'workout-reminder':
      await sendWorkoutReminder(job.data);
      break;
    case 'achievement':
      await sendAchievementNotification(job.data);
      break;
  }
}, { connection: redis });
```

### 9.3 Jobs Agendados

```typescript
// scheduler.ts
import { Queue } from 'bullmq';

// Churn analysis - daily at 6am
await churnQueue.add('analyze', {}, {
  repeat: { cron: '0 6 * * *' }
});

// Appointment reminders - every hour
await notificationQueue.add('check-reminders', {}, {
  repeat: { cron: '0 * * * *' }
});

// Inactive users alert - daily at 9am
await notificationQueue.add('inactive-alert', {}, {
  repeat: { cron: '0 9 * * *' }
});
```

---

## 10. Integracao WhatsApp

### 10.1 Evolution API Setup

```yaml
# docker-compose.yml
evolution-api:
  image: atendai/evolution-api:v2.1.1
  environment:
    - SERVER_URL=${EVOLUTION_SERVER_URL}
    - AUTHENTICATION_API_KEY=${EVOLUTION_API_KEY}
    - DATABASE_ENABLED=true
    - DATABASE_PROVIDER=postgresql
    - DATABASE_CONNECTION_URI=postgresql://...
    - CACHE_REDIS_ENABLED=true
    - CACHE_REDIS_URI=redis://redis:6379
```

### 10.2 WhatsApp Service

```typescript
// whatsapp.service.ts
export class WhatsAppService {
  private readonly baseUrl = process.env.EVOLUTION_API_URL;
  private readonly apiKey = process.env.EVOLUTION_API_KEY;

  async createInstance(businessId: string): Promise<string> {
    const response = await fetch(`${this.baseUrl}/instance/create`, {
      method: 'POST',
      headers: { 'apikey': this.apiKey },
      body: JSON.stringify({ instanceName: `fis360_${businessId}` })
    });
    return response.json();
  }

  async getQRCode(instanceName: string): Promise<string> {
    const response = await fetch(`${this.baseUrl}/instance/qrcode/${instanceName}`, {
      headers: { 'apikey': this.apiKey }
    });
    return response.json();
  }

  async sendText(instanceName: string, to: string, text: string): Promise<void> {
    await whatsappQueue.add('send-text', { instanceName, to, text });
  }
}
```

### 10.3 Templates de Mensagem

```typescript
// templates/whatsapp.ts
export const templates = {
  appointmentConfirmation: (data: any) => `
Ola ${data.studentName}!

Seu agendamento foi confirmado:
- Servico: ${data.service}
- Data: ${data.date}
- Horario: ${data.time}
- Profissional: ${data.professional}

Para cancelar ou remarcar, responda esta mensagem.

Ate la!
`,

  workoutReminder: (data: any) => `
Bom dia ${data.studentName}!

Hoje e dia de treino! Seu treino de ${data.workoutType} esta te esperando.

Sua sequencia atual: ${data.streak} dias!

Bora treinar?
`,

  achievementUnlocked: (data: any) => `
PARABENS ${data.studentName}!

Voce desbloqueou uma nova conquista:
*${data.badgeName}*

${data.badgeDescription}

Continue assim!
`,
};
```

---

## 11. Seguranca

### 11.1 Checklist de Seguranca

- [x] HTTPS obrigatorio
- [x] JWT com expiracao curta
- [x] Refresh tokens rotativos
- [x] Rate limiting por IP e usuario
- [x] Validacao de input com Zod
- [x] Sanitizacao de output
- [x] CORS configurado
- [x] Headers de seguranca (Helmet)
- [x] Senhas com bcrypt (cost 12)
- [x] SQL injection prevention (Prisma)
- [x] XSS prevention (React)
- [x] CSRF tokens para forms
- [x] Audit log de acoes sensiveis

### 11.2 Headers de Seguranca

```typescript
// security.middleware.ts
import helmet from 'helmet';

app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
    }
  },
  hsts: { maxAge: 31536000, includeSubDomains: true },
  noSniff: true,
  referrerPolicy: { policy: 'strict-origin-when-cross-origin' },
}));
```

### 11.3 Validacao de Input

```typescript
// students.schema.ts
import { z } from 'zod';

export const createStudentSchema = z.object({
  name: z.string().min(2).max(100),
  email: z.string().email(),
  phone: z.string().regex(/^\+?[0-9]{10,15}$/),
  birthDate: z.string().datetime().optional(),
  goals: z.array(z.nativeEnum(GoalType)).min(1),
  healthNotes: z.string().max(1000).optional(),
});

// Middleware de validacao
export const validate = (schema: z.ZodSchema) => {
  return (req, res, next) => {
    const result = schema.safeParse(req.body);
    if (!result.success) {
      return res.status(400).json({
        success: false,
        error: {
          code: 'VALIDATION_ERROR',
          details: result.error.errors
        }
      });
    }
    req.body = result.data;
    next();
  };
};
```

---

## 12. Monitoramento e Logs

### 12.1 Logging

```typescript
// logger.ts
import pino from 'pino';

export const logger = pino({
  level: process.env.LOG_LEVEL || 'info',
  transport: process.env.NODE_ENV === 'development'
    ? { target: 'pino-pretty' }
    : undefined,
});

// Request logging
app.use((req, res, next) => {
  const start = Date.now();
  res.on('finish', () => {
    logger.info({
      method: req.method,
      url: req.url,
      status: res.statusCode,
      duration: Date.now() - start,
      userId: req.user?.userId,
      businessId: req.user?.businessId,
    });
  });
  next();
});
```

### 12.2 Metricas

```
METRICAS COLETADAS:
- Request count by endpoint
- Response time (p50, p95, p99)
- Error rate
- Active connections
- Queue size
- Cache hit rate
- Database query time
```

### 12.3 Health Checks

```typescript
// health.controller.ts
router.get('/health', async (req, res) => {
  const checks = {
    database: await checkDatabase(),
    redis: await checkRedis(),
    whatsapp: await checkEvolutionAPI(),
  };

  const healthy = Object.values(checks).every(c => c.status === 'ok');

  res.status(healthy ? 200 : 503).json({
    status: healthy ? 'healthy' : 'unhealthy',
    checks,
    timestamp: new Date().toISOString(),
  });
});
```

---

## 13. Deploy e CI/CD

### 13.1 Docker Compose Producao

```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    restart: unless-stopped
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    restart: unless-stopped
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data

  evolution-api:
    image: atendai/evolution-api:v2.1.1
    restart: unless-stopped
    environment:
      - SERVER_URL=${EVOLUTION_SERVER_URL}
      - AUTHENTICATION_API_KEY=${EVOLUTION_API_KEY}
    depends_on:
      - postgres
      - redis

  api:
    build:
      context: .
      dockerfile: apps/api/Dockerfile
      target: production
    restart: unless-stopped
    environment:
      - NODE_ENV=production
      - DATABASE_URL=${DATABASE_URL}
      - REDIS_URL=${REDIS_URL}
    depends_on:
      - postgres
      - redis

  worker:
    build:
      context: .
      dockerfile: apps/api/Dockerfile
      target: production
    restart: unless-stopped
    command: node dist/worker.js
    depends_on:
      - api

  web:
    build:
      context: .
      dockerfile: apps/web/Dockerfile
      target: production
    restart: unless-stopped
    depends_on:
      - api

  nginx:
    image: nginx:alpine
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./docker/nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./docker/nginx/ssl:/etc/nginx/ssl:ro
    depends_on:
      - web
      - api

volumes:
  postgres_data:
  redis_data:
```

### 13.2 GitHub Actions

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v2
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: pnpm
      - run: pnpm install
      - run: pnpm test
      - run: pnpm lint

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to server
        run: |
          ssh ${{ secrets.SERVER }} "cd /app && git pull && docker compose -f docker-compose.prod.yml up -d --build"
```

---

## 14. Decisoes Arquiteturais (ADRs)

### ADR-001: Monorepo com pnpm workspaces

**Contexto**: Precisamos compartilhar codigo entre API e frontends.

**Decisao**: Usar monorepo com pnpm workspaces + Turborepo.

**Consequencias**:
- (+) Codigo compartilhado facilmente
- (+) Deploys atomicos
- (+) DX melhor
- (-) Build mais complexo
- (-) CI/CD mais lento

### ADR-002: PostgreSQL como banco principal

**Contexto**: Precisamos de um banco relacional robusto.

**Decisao**: PostgreSQL 15 com Prisma ORM.

**Consequencias**:
- (+) ACID compliance
- (+) JSON support
- (+) Full-text search
- (+) Prisma types
- (-) Escala vertical limitada

### ADR-003: PWA ao inves de React Native

**Contexto**: App do aluno precisa funcionar em iOS e Android.

**Decisao**: PWA com Next.js ao inves de React Native.

**Consequencias**:
- (+) Codigo unico
- (+) Deploy mais simples
- (+) Updates instantaneos
- (-) Sem acesso a algumas APIs nativas
- (-) Experiencia inferior em iOS

### ADR-004: Evolution API para WhatsApp

**Contexto**: Precisamos integrar WhatsApp.

**Decisao**: Evolution API v2 self-hosted.

**Consequencias**:
- (+) Controle total
- (+) Sem custos por mensagem
- (+) Multi-instancia
- (-) Manutencao propria
- (-) Risco de bloqueio do numero

---

*Documento gerado em 06/01/2026*
*Metodologia: BMad Framework*
