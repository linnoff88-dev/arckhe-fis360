# Database Design

## FIS360 - Design do Banco de Dados

---

## 1. Visao Geral

- **Banco**: PostgreSQL 15
- **ORM**: Prisma 5.x
- **Estrategia Multi-tenancy**: Shared database, shared schema

---

## 2. Modelos Principais

### 2.1 Business (Tenant)

```prisma
model Business {
  id        String   @id @default(cuid())
  name      String
  slug      String   @unique
  type      BusinessType
  logoUrl   String?
  primaryColor String @default("#6366f1")

  // Endereco
  address   String?
  city      String?
  state     String?
  zipCode   String?
  phone     String?

  // Config
  timezone  String   @default("America/Sao_Paulo")
  settings  Json     @default("{}")

  // Trial/Subscription
  trialEndsAt   DateTime?
  subscriptionId String?

  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  deletedAt DateTime?

  // Relations
  users         User[]
  students      Student[]
  professionals Professional[]
  exercises     Exercise[]
  // ...
}

enum BusinessType {
  GYM
  PERSONAL_STUDIO
  PHYSIO_CLINIC
  CROSSFIT_BOX
  PILATES_STUDIO
  ONLINE_ONLY
  HYBRID
}
```

### 2.2 User

```prisma
model User {
  id           String   @id @default(cuid())
  businessId   String
  email        String
  passwordHash String
  role         UserRole
  isActive     Boolean  @default(true)

  // Profile
  name         String?
  avatarUrl    String?
  phone        String?

  // Timestamps
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
  lastLoginAt  DateTime?

  // Relations
  business     Business @relation(fields: [businessId], references: [id])
  student      Student?
  professional Professional?

  @@unique([businessId, email])
  @@index([businessId])
}

enum UserRole {
  BUSINESS_OWNER
  MANAGER
  PROFESSIONAL
  RECEPTIONIST
  STUDENT
}
```

### 2.3 Student

```prisma
model Student {
  id         String   @id @default(cuid())
  userId     String?  @unique
  businessId String

  // Dados pessoais
  name       String
  email      String
  phone      String
  birthDate  DateTime?
  cpf        String?
  avatarUrl  String?

  // Objetivos e saude
  goals      GoalType[]
  healthNotes String?
  injuries    String?
  emergencyContact String?
  emergencyPhone   String?

  // Status
  status     StudentStatus @default(ACTIVE)

  // Gamificacao
  totalPoints   Int @default(0)
  currentStreak Int @default(0)
  longestStreak Int @default(0)
  level         Int @default(1)
  lastWorkoutAt DateTime?

  // Timestamps
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
  deletedAt  DateTime?

  // Relations
  business      Business @relation(fields: [businessId], references: [id])
  user          User?    @relation(fields: [userId], references: [id])
  workouts      Workout[]
  workoutLogs   WorkoutLog[]
  appointments  Appointment[]
  assessments   Assessment[]
  badges        StudentBadge[]

  @@unique([businessId, email])
  @@index([businessId])
  @@index([businessId, status])
}

enum StudentStatus {
  ACTIVE
  INACTIVE
  PAUSED
  CANCELLED
}

enum GoalType {
  WEIGHT_LOSS
  MUSCLE_GAIN
  STRENGTH
  ENDURANCE
  FLEXIBILITY
  REHABILITATION
  HEALTH
  SPORT_SPECIFIC
  BODY_RECOMPOSITION
}
```

### 2.4 Exercise

```prisma
model Exercise {
  id          String   @id @default(cuid())
  businessId  String?  // null = global
  name        String
  description String?
  instructions String?
  videoUrl    String?
  thumbnailUrl String?

  category    ExerciseCategory
  muscles     MuscleGroup[]
  equipment   Equipment[]
  difficulty  Difficulty @default(INTERMEDIATE)

  isGlobal    Boolean @default(false)

  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt

  business    Business? @relation(fields: [businessId], references: [id])

  @@index([businessId])
  @@index([category])
}

enum ExerciseCategory {
  CHEST
  BACK
  SHOULDERS
  BICEPS
  TRICEPS
  FOREARMS
  ABS
  QUADRICEPS
  HAMSTRINGS
  GLUTES
  CALVES
  FULL_BODY
  CARDIO
  MOBILITY
  REHABILITATION
}

enum MuscleGroup {
  // Similar to ExerciseCategory
}

enum Equipment {
  BARBELL
  DUMBBELL
  CABLE
  MACHINE
  BODYWEIGHT
  KETTLEBELL
  RESISTANCE_BAND
  MEDICINE_BALL
  FOAM_ROLLER
  TRX
  NONE
}

enum Difficulty {
  BEGINNER
  INTERMEDIATE
  ADVANCED
}
```

### 2.5 Workout

```prisma
model WorkoutTemplate {
  id          String   @id @default(cuid())
  businessId  String
  name        String
  description String?
  type        WorkoutType
  difficulty  Difficulty @default(INTERMEDIATE)
  estimatedDuration Int? // minutos

  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt

  business    Business @relation(fields: [businessId], references: [id])
  exercises   WorkoutTemplateExercise[]
  workouts    Workout[]

  @@index([businessId])
}

model Workout {
  id         String   @id @default(cuid())
  studentId  String
  templateId String?
  name       String

  validFrom  DateTime
  validUntil DateTime?
  weekDays   Int[]    // 0-6
  frequency  Int?     // treinos por semana
  status     WorkoutStatus @default(ACTIVE)

  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt

  student    Student  @relation(fields: [studentId], references: [id])
  template   WorkoutTemplate? @relation(fields: [templateId], references: [id])
  exercises  WorkoutExercise[]
  logs       WorkoutLog[]

  @@index([studentId])
  @@index([studentId, status])
}

enum WorkoutType {
  STRENGTH
  HYPERTROPHY
  CARDIO
  HIIT
  FUNCTIONAL
  MOBILITY
  REHABILITATION
  MIXED
}

enum WorkoutStatus {
  ACTIVE
  PAUSED
  EXPIRED
  COMPLETED
}
```

---

## 3. Indices

```sql
-- Multi-tenancy
CREATE INDEX idx_students_business ON students(business_id);
CREATE INDEX idx_workouts_student ON workouts(student_id);
CREATE INDEX idx_appointments_business_date ON appointments(business_id, date);

-- Busca
CREATE INDEX idx_students_name ON students USING gin(name gin_trgm_ops);
CREATE INDEX idx_exercises_name ON exercises USING gin(name gin_trgm_ops);

-- Performance
CREATE INDEX idx_workout_logs_date ON workout_logs(date);
CREATE INDEX idx_checkins_date ON checkins(checkin_at);
```

---

## 4. Migrations

```bash
# Criar migration
pnpm --filter api prisma migrate dev --name add_gamification

# Aplicar em producao
pnpm --filter api prisma migrate deploy

# Reset (dev only)
pnpm --filter api prisma migrate reset
```

---

## 5. Seed

```typescript
// prisma/seed.ts
async function main() {
  // Criar exercicios globais
  await prisma.exercise.createMany({
    data: exercises.map(e => ({
      ...e,
      isGlobal: true,
      businessId: null
    }))
  });

  // Criar badges
  await prisma.badge.createMany({
    data: badges
  });
}
```

---

*Referencia: docs/architecture.md - Secao 4*
