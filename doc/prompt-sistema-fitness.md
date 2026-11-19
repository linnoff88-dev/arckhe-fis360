# Prompt de Instrucao Completa: Sistema Fis360

**Baseado na arquitetura e licoes aprendidas do projeto Bela360**

---

## PARTE 1: Analise do Setor e Problemas Resolvidos

### 1.1 Contexto do Projeto Base (Bela360)

O Bela360 e um sistema de gestao para saloes de beleza que resolveu:

- **Problema de CORS**: Usar apenas docker-compose.prod.yml em producao
- **Evolution API 403**: Verificar instancia existente antes de criar nova
- **Container web em dev**: Rebuildar com target production
- **QR Code WhatsApp**: Tratar multiplos formatos de resposta da Evolution API v2
- **Autenticacao**: JWT com refresh tokens e middleware de verificacao

### 1.2 Analise Profunda do Setor Fitness e Saude Fisica

#### Necessidades dos DONOS DE ACADEMIA

Principais dores:
- Controle de acesso e catraca manual ou desatualizado
- Alta taxa de desistencia (churn) nos primeiros 3 meses
- Dificuldade em medir engajamento dos alunos
- Gestao de planos e inadimplencia
- Falta de diferenciacao competitiva
- Dependencia excessiva de poucos professores
- Horarios de pico lotados, horarios vazios ociosos

**Necessidade central:** Gestao inteligente que reduza churn e maximize ocupacao

#### Necessidades dos PERSONAL TRAINERS

Principais dores:
- Agenda descentralizada (WhatsApp, papel, apps)
- Dificuldade em escalar (limite de horas)
- Controle financeiro manual
- Falta de historico estruturado dos alunos
- Concorrencia com apps de treino gratuitos
- Dificuldade em fidelizar clientes

**Necessidade central:** Profissionalizar servico e escalar sem perder qualidade

#### Necessidades dos FISIOTERAPEUTAS

Principais dores:
- Prontuarios em papel ou sistemas genericos
- Falta de acompanhamento entre sessoes
- Dificuldade em medir evolucao do paciente
- Agendamento manual com muitas remarcacoes
- Laudos e relatorios demorados
- Comunicacao com medicos/planos de saude

**Necessidade central:** Prontuario inteligente com acompanhamento continuo

#### Necessidades dos ALUNOS/PACIENTES

O que realmente querem:
- Facilidade para agendar/remarcar
- Ver evolucao de forma visual (fotos, medidas, cargas)
- Treinos acessiveis no celular
- Lembretes e motivacao
- Flexibilidade de horarios
- Sentir progresso e resultados
- Comunicacao facil com profissional

**Necessidade central:** Resultados visiveis + conveniencia + motivacao

---

## PARTE 2: Modelo de Negocio Escalavel

### 2.1 Niveis de Escala (do Tradicional ao Massivo)

```
NIVEL 1: Atendimento Presencial Individual
└── Personal trainer ou fisio tradicional
└── Limite: ~40 alunos/mes
└── Receita: R$ 8-20k/mes

NIVEL 2: Grupos e Turmas
└── Aulas coletivas, grupos de treino
└── Limite: ~100-200 alunos
└── Receita: R$ 20-50k/mes

NIVEL 3: Modelo Hibrido (Presencial + Online)
└── Treinos online + check-ins presenciais
└── Limite: ~500 alunos
└── Receita: R$ 50-150k/mes

NIVEL 4: Plataforma de Conteudo
└── Programas gravados + comunidade
└── Limite: ~5.000 assinantes
└── Receita: R$ 150-500k/mes

NIVEL 5: Franquia/Licenciamento
└── Outros profissionais usam sua metodologia
└── Limite: Ilimitado
└── Receita: R$ 500k+/mes
```

### 2.2 Verticais de Negocio Suportadas

1. **Academia tradicional** - Planos mensais, catraca, aulas
2. **Studio de Personal** - Agendamento, pacotes, evolucao
3. **Clinica de Fisioterapia** - Prontuario, sessoes, laudos
4. **Box de CrossFit** - WODs, rankings, comunidade
5. **Studio de Pilates/Yoga** - Turmas, equipamentos, professores
6. **Consultoria Online** - Treinos remotos, video-chamadas
7. **Plataforma de Cursos** - Programas de treino vendidos

---

## PARTE 3: Modulos Funcionais

### 3.1 Modulos Core

| Modulo | Descricao | Usuarios |
|--------|-----------|----------|
| Alunos/Pacientes | Cadastro, historico, evolucao | Todos |
| Agenda | Agendamento inteligente com regras | Todos |
| Treinos | Criacao, prescricao, biblioteca | Personal/Academia |
| Prontuario | Avaliacao, evolucao, sessoes | Fisio |
| Avaliacoes | Antropometria, testes, fotos | Todos |
| Financeiro | Planos, pagamentos, comissoes | Todos |
| Check-in | Controle de acesso, frequencia | Academia |
| Exercicios | Biblioteca com videos/instrucoes | Todos |

### 3.2 Modulos de Engajamento

| Modulo | Descricao |
|--------|-----------|
| Evolucao | Graficos, fotos antes/depois, PRs |
| Gamificacao | Pontos, badges, rankings, desafios |
| Comunidade | Feed, grupos, comentarios |
| Notificacoes | Push, WhatsApp, email automaticos |
| Desafios | Competicoes internas, metas coletivas |

### 3.3 Modulos de Escala

| Modulo | Descricao |
|--------|-----------|
| Programas | Cursos estruturados (ex: 12 semanas) |
| Assinaturas | Planos recorrentes com niveis |
| Video Aulas | Biblioteca de conteudo gravado |
| Lives | Aulas ao vivo com chat |
| Marketplace | Venda de programas de outros profissionais |

### 3.4 Modulos Especificos por Vertical

**Academia:**
- Catraca/Acesso
- Aulas coletivas
- Grade de horarios
- Gestao de equipamentos

**Fisioterapia:**
- Anamnese detalhada
- CID/Diagnostico
- Protocolos de tratamento
- Laudos e relatorios
- Integracao com planos de saude

**CrossFit/Funcional:**
- WODs (Workout of the Day)
- Benchmark workouts
- Leaderboard
- PRs (Personal Records)

---

## PARTE 4: Arquitetura Tecnica

### 4.1 Stack Tecnologico

```
Frontend (App):
- Next.js 14 (App Router) - Dashboard profissional
- React Native / Expo - App do aluno
- TailwindCSS + shadcn/ui
- TypeScript

Backend:
- Express.js + TypeScript
- Prisma ORM
- PostgreSQL 15
- Redis 7 (cache + filas)
- BullMQ (jobs agendados)

Integracao:
- Evolution API v2 (WhatsApp)
- Stripe/PagSeguro (pagamentos)
- AWS S3 (videos/fotos)
- Vimeo/Bunny (streaming)

Infraestrutura:
- Docker + Docker Compose
- Nginx (reverse proxy + SSL)
- GitHub Actions (CI/CD)
```

### 4.2 Estrutura do Monorepo

```
fis360/
├── apps/
│   ├── api/                 # Backend Express
│   │   ├── src/
│   │   │   ├── modules/
│   │   │   │   ├── auth/
│   │   │   │   ├── users/
│   │   │   │   ├── students/
│   │   │   │   ├── professionals/
│   │   │   │   ├── workouts/
│   │   │   │   ├── exercises/
│   │   │   │   ├── assessments/
│   │   │   │   ├── appointments/
│   │   │   │   ├── checkins/
│   │   │   │   ├── medical-records/
│   │   │   │   ├── programs/
│   │   │   │   ├── subscriptions/
│   │   │   │   ├── finance/
│   │   │   │   ├── gamification/
│   │   │   │   ├── notifications/
│   │   │   │   ├── whatsapp/
│   │   │   │   └── reports/
│   │   │   ├── config/
│   │   │   ├── middlewares/
│   │   │   └── utils/
│   │   └── prisma/
│   │       └── schema.prisma
│   │
│   ├── web/                 # Dashboard Next.js
│   │   └── src/
│   │       └── app/
│   │           ├── (auth)/
│   │           ├── (dashboard)/
│   │           │   ├── alunos/
│   │           │   ├── agenda/
│   │           │   ├── treinos/
│   │           │   ├── exercicios/
│   │           │   ├── avaliacoes/
│   │           │   ├── prontuario/
│   │           │   ├── checkin/
│   │           │   ├── turmas/
│   │           │   ├── programas/
│   │           │   ├── financeiro/
│   │           │   ├── gamificacao/
│   │           │   ├── relatorios/
│   │           │   ├── marketing/
│   │           │   └── configuracoes/
│   │           └── api/
│   │
│   └── mobile/              # App React Native
│       └── src/
│           ├── screens/
│           │   ├── Home/
│           │   ├── Workout/
│           │   ├── Progress/
│           │   ├── Schedule/
│           │   ├── Profile/
│           │   └── Community/
│           └── components/
│
├── packages/
│   └── shared/              # Tipos e utils compartilhados
│
├── docker-compose.yml
├── docker-compose.prod.yml
└── package.json
```

---

## PARTE 5: Schema Prisma Completo

```prisma
// schema.prisma - Fis360

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// ==================== ENUMS ====================

enum UserRole {
  SUPER_ADMIN
  BUSINESS_OWNER
  MANAGER
  PROFESSIONAL
  RECEPTIONIST
  STUDENT
}

enum BusinessType {
  GYM              // Academia tradicional
  PERSONAL_STUDIO  // Studio de personal
  PHYSIO_CLINIC    // Clinica de fisioterapia
  CROSSFIT_BOX     // Box de CrossFit
  PILATES_STUDIO   // Studio de Pilates/Yoga
  ONLINE_ONLY      // Apenas consultoria online
  HYBRID           // Modelo hibrido
}

enum Gender {
  MALE
  FEMALE
  OTHER
}

enum AppointmentStatus {
  SCHEDULED
  CONFIRMED
  IN_PROGRESS
  COMPLETED
  CANCELLED
  NO_SHOW
}

enum PaymentStatus {
  PENDING
  PAID
  OVERDUE
  CANCELLED
  REFUNDED
}

enum PaymentMethod {
  CREDIT_CARD
  DEBIT_CARD
  PIX
  BANK_SLIP
  CASH
  TRANSFER
}

enum SubscriptionStatus {
  ACTIVE
  PAUSED
  CANCELLED
  EXPIRED
  TRIAL
}

enum WorkoutType {
  STRENGTH        // Musculacao
  CARDIO          // Cardio
  HIIT            // Alta intensidade
  FLEXIBILITY     // Flexibilidade
  FUNCTIONAL      // Funcional
  CROSSFIT        // CrossFit
  PILATES         // Pilates
  YOGA            // Yoga
  REHABILITATION  // Reabilitacao
  CUSTOM          // Personalizado
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
  PECTORALIS_MAJOR
  LATISSIMUS_DORSI
  TRAPEZIUS
  DELTOIDS
  BICEPS_BRACHII
  TRICEPS_BRACHII
  RECTUS_ABDOMINIS
  OBLIQUES
  QUADRICEPS
  HAMSTRINGS
  GLUTEUS_MAXIMUS
  GASTROCNEMIUS
  ERECTOR_SPINAE
  CORE
}

enum DifficultyLevel {
  BEGINNER
  INTERMEDIATE
  ADVANCED
  EXPERT
}

enum SessionType {
  INDIVIDUAL
  DUO
  GROUP
  CLASS
  ONLINE
  HYBRID
}

enum PhysioSessionType {
  EVALUATION
  TREATMENT
  REEVALUATION
  DISCHARGE
  MAINTENANCE
}

enum InjuryStatus {
  ACTIVE
  RECOVERING
  HEALED
  CHRONIC
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

enum NotificationType {
  APPOINTMENT_REMINDER
  WORKOUT_REMINDER
  PAYMENT_DUE
  ACHIEVEMENT
  MOTIVATION
  CLASS_REMINDER
  ASSESSMENT_DUE
  INACTIVITY_ALERT
  BIRTHDAY
  RENEWAL_REMINDER
}

enum BadgeType {
  ATTENDANCE
  CONSISTENCY
  STRENGTH
  ENDURANCE
  WEIGHT_LOSS
  MUSCLE_GAIN
  SOCIAL
  CHALLENGE
  MILESTONE
}

// ==================== CORE MODELS ====================

model Business {
  id                String       @id @default(cuid())
  name              String
  slug              String       @unique
  type              BusinessType
  document          String?      // CNPJ
  email             String
  phone             String

  // Endereco
  address           String?
  city              String?
  state             String?
  zipCode           String?

  // Configuracoes
  timezone          String       @default("America/Sao_Paulo")
  currency          String       @default("BRL")

  // WhatsApp
  whatsappInstanceId  String?
  whatsappConnected   Boolean    @default(false)

  // Configuracoes de negocio
  workingHours      Json?        // Horario de funcionamento
  bookingRules      Json?        // Regras de agendamento
  cancellationPolicy Json?       // Politica de cancelamento

  // Branding
  logo              String?
  primaryColor      String?      @default("#10B981")

  // Plano
  plan              String       @default("starter")
  planExpiresAt     DateTime?

  // Timestamps
  createdAt         DateTime     @default(now())
  updatedAt         DateTime     @updatedAt

  // Relacionamentos
  users             User[]
  students          Student[]
  professionals     Professional[]
  locations         Location[]
  services          Service[]
  plans             Plan[]
  appointments      Appointment[]
  classes           Class[]
  exercises         Exercise[]
  workoutTemplates  WorkoutTemplate[]
  programs          Program[]
  challenges        Challenge[]
  campaigns         Campaign[]
  transactions      Transaction[]

  @@index([slug])
}

model Location {
  id          String   @id @default(cuid())
  businessId  String
  name        String
  address     String
  city        String
  state       String
  zipCode     String
  phone       String?
  isMain      Boolean  @default(false)
  isActive    Boolean  @default(true)

  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt

  business    Business @relation(fields: [businessId], references: [id], onDelete: Cascade)
  rooms       Room[]
  equipment   Equipment[]
  classes     Class[]
  checkins    Checkin[]

  @@index([businessId])
}

model Room {
  id          String   @id @default(cuid())
  locationId  String
  name        String
  capacity    Int
  description String?
  isActive    Boolean  @default(true)

  location    Location @relation(fields: [locationId], references: [id], onDelete: Cascade)
  classes     Class[]
  appointments Appointment[]

  @@index([locationId])
}

model Equipment {
  id          String   @id @default(cuid())
  locationId  String
  name        String
  brand       String?
  model       String?
  quantity    Int      @default(1)
  condition   String?  // Bom, Regular, Manutencao
  lastMaintenance DateTime?
  notes       String?

  location    Location @relation(fields: [locationId], references: [id], onDelete: Cascade)

  @@index([locationId])
}

// ==================== USER MODELS ====================

model User {
  id            String    @id @default(cuid())
  businessId    String
  email         String
  passwordHash  String
  role          UserRole
  isActive      Boolean   @default(true)
  lastLoginAt   DateTime?

  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt

  business      Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  student       Student?
  professional  Professional?

  @@unique([businessId, email])
  @@index([businessId])
}

model Student {
  id                String    @id @default(cuid())
  userId            String    @unique
  businessId        String

  // Dados pessoais
  name              String
  email             String
  phone             String
  cpf               String?
  birthDate         DateTime?
  gender            Gender?
  photo             String?

  // Endereco
  address           String?
  city              String?
  state             String?
  zipCode           String?

  // Contato emergencia
  emergencyContact  String?
  emergencyPhone    String?

  // Objetivos e restricoes
  goals             GoalType[]
  healthNotes       String?   // Observacoes de saude
  injuries          String?   // Lesoes conhecidas
  medications       String?

  // Preferencias
  preferredTime     String?   // Manha, Tarde, Noite
  preferredDays     String[]  // Segunda, Terca, etc

  // Status
  status            String    @default("active") // active, inactive, paused
  inactiveReason    String?

  // Indicacao
  referredBy        String?
  referralSource    String?   // Instagram, Google, Indicacao, etc

  // Gamificacao
  totalPoints       Int       @default(0)
  currentStreak     Int       @default(0)
  longestStreak     Int       @default(0)
  level             Int       @default(1)

  // Timestamps
  registeredAt      DateTime  @default(now())
  lastActivityAt    DateTime?
  createdAt         DateTime  @default(now())
  updatedAt         DateTime  @updatedAt

  // Relacionamentos
  user              User      @relation(fields: [userId], references: [id], onDelete: Cascade)
  business          Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  subscriptions     Subscription[]
  appointments      Appointment[]
  assessments       Assessment[]
  workouts          Workout[]
  workoutLogs       WorkoutLog[]
  checkins          Checkin[]
  medicalRecord     MedicalRecord?
  physioSessions    PhysioSession[]
  progressPhotos    ProgressPhoto[]
  measurements      Measurement[]
  personalRecords   PersonalRecord[]
  badges            StudentBadge[]
  challengeParticipations ChallengeParticipation[]
  notifications     Notification[]
  classAttendances  ClassAttendance[]
  payments          Payment[]
  programEnrollments ProgramEnrollment[]
  goals             Goal[]

  @@unique([businessId, email])
  @@unique([businessId, cpf])
  @@index([businessId])
  @@index([status])
}

model Professional {
  id              String    @id @default(cuid())
  userId          String    @unique
  businessId      String

  // Dados pessoais
  name            String
  email           String
  phone           String
  cpf             String?
  photo           String?
  bio             String?

  // Profissional
  specialty       String[]  // Personal, Fisioterapeuta, Pilates, etc
  cref            String?   // Registro profissional
  cofito          String?   // Para fisioterapeutas
  certifications  String[]
  experience      Int?      // Anos de experiencia

  // Trabalho
  workingHours    Json?     // Horarios disponiveis
  workingDays     String[]
  maxDailyClients Int       @default(10)
  sessionDuration Int       @default(60) // minutos

  // Financeiro
  commissionRate  Float     @default(0)
  fixedSalary     Float     @default(0)

  // Status
  isActive        Boolean   @default(true)
  hireDate        DateTime?

  // Redes sociais
  instagram       String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  // Relacionamentos
  user            User      @relation(fields: [userId], references: [id], onDelete: Cascade)
  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  appointments    Appointment[]
  classes         Class[]
  workoutTemplates WorkoutTemplate[]
  assessments     Assessment[]
  physioSessions  PhysioSession[]
  commissions     Commission[]

  @@unique([businessId, email])
  @@index([businessId])
}

// ==================== SUBSCRIPTION & PLANS ====================

model Plan {
  id              String    @id @default(cuid())
  businessId      String
  name            String
  description     String?

  // Preco
  price           Float
  billingCycle    String    // monthly, quarterly, semiannual, annual
  installments    Int       @default(1)

  // Beneficios
  features        String[]
  sessionsPerWeek Int?      // Limite de sessoes por semana
  sessionsPerMonth Int?     // Limite de sessoes por mes
  classesIncluded Boolean   @default(true)
  onlineAccess    Boolean   @default(false)

  // Configuracoes
  duration        Int       // Duracao em dias
  trialDays       Int       @default(0)
  isActive        Boolean   @default(true)
  isPopular       Boolean   @default(false)

  // Promocao
  discountPercent Float?
  discountValidUntil DateTime?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  subscriptions   Subscription[]

  @@index([businessId])
}

model Subscription {
  id              String             @id @default(cuid())
  studentId       String
  planId          String

  status          SubscriptionStatus
  startDate       DateTime
  endDate         DateTime
  trialEndsAt     DateTime?

  // Pagamento
  nextBillingDate DateTime?
  lastPaymentDate DateTime?
  paymentMethod   PaymentMethod?

  // Pausas
  pausedAt        DateTime?
  pauseReason     String?
  resumeDate      DateTime?

  // Cancelamento
  cancelledAt     DateTime?
  cancelReason    String?

  createdAt       DateTime           @default(now())
  updatedAt       DateTime           @updatedAt

  student         Student            @relation(fields: [studentId], references: [id], onDelete: Cascade)
  plan            Plan               @relation(fields: [planId], references: [id])
  payments        Payment[]

  @@index([studentId])
  @@index([status])
}

// ==================== APPOINTMENTS ====================

model Service {
  id              String    @id @default(cuid())
  businessId      String
  name            String
  description     String?
  duration        Int       // Duracao em minutos
  price           Float
  category        String    // Avaliacao, Treino, Fisio, etc
  color           String?
  isActive        Boolean   @default(true)

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  appointments    Appointment[]

  @@index([businessId])
}

model Appointment {
  id              String            @id @default(cuid())
  businessId      String
  studentId       String
  professionalId  String
  serviceId       String?
  roomId          String?

  // Horario
  date            DateTime
  startTime       DateTime
  endTime         DateTime

  // Status
  status          AppointmentStatus @default(SCHEDULED)
  type            SessionType       @default(INDIVIDUAL)

  // Detalhes
  notes           String?
  internalNotes   String?

  // Confirmacao
  confirmedAt     DateTime?
  confirmedVia    String?           // whatsapp, app, phone

  // Cancelamento
  cancelledAt     DateTime?
  cancelledBy     String?
  cancelReason    String?

  // Conclusao
  completedAt     DateTime?
  feedback        String?
  rating          Int?

  // Recorrencia
  isRecurring     Boolean   @default(false)
  recurrenceRule  String?   // RRULE format
  parentId        String?   // ID do agendamento pai

  createdAt       DateTime          @default(now())
  updatedAt       DateTime          @updatedAt

  business        Business          @relation(fields: [businessId], references: [id], onDelete: Cascade)
  student         Student           @relation(fields: [studentId], references: [id])
  professional    Professional      @relation(fields: [professionalId], references: [id])
  service         Service?          @relation(fields: [serviceId], references: [id])
  room            Room?             @relation(fields: [roomId], references: [id])

  @@index([businessId])
  @@index([studentId])
  @@index([professionalId])
  @@index([date])
  @@index([status])
}

// ==================== CLASSES (AULAS COLETIVAS) ====================

model Class {
  id              String    @id @default(cuid())
  businessId      String
  locationId      String
  roomId          String?
  professionalId  String

  name            String
  description     String?
  type            WorkoutType
  duration        Int       // Duracao em minutos
  capacity        Int       // Limite de alunos

  // Horario
  dayOfWeek       Int       // 0-6 (domingo-sabado)
  startTime       String    // HH:mm
  endTime         String    // HH:mm

  // Configuracoes
  isActive        Boolean   @default(true)
  requiresBooking Boolean   @default(true)
  bookingDeadline Int?      // Minutos antes para reservar
  cancellationDeadline Int? // Minutos antes para cancelar

  color           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  location        Location  @relation(fields: [locationId], references: [id])
  room            Room?     @relation(fields: [roomId], references: [id])
  professional    Professional @relation(fields: [professionalId], references: [id])
  sessions        ClassSession[]

  @@index([businessId])
  @@index([dayOfWeek])
}

model ClassSession {
  id              String    @id @default(cuid())
  classId         String
  date            DateTime
  startTime       DateTime
  endTime         DateTime

  status          String    @default("scheduled") // scheduled, in_progress, completed, cancelled
  notes           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  class           Class     @relation(fields: [classId], references: [id], onDelete: Cascade)
  attendances     ClassAttendance[]

  @@index([classId])
  @@index([date])
}

model ClassAttendance {
  id              String    @id @default(cuid())
  classSessionId  String
  studentId       String

  status          String    @default("booked") // booked, attended, no_show, cancelled
  bookedAt        DateTime  @default(now())
  checkedInAt     DateTime?
  cancelledAt     DateTime?

  classSession    ClassSession @relation(fields: [classSessionId], references: [id], onDelete: Cascade)
  student         Student   @relation(fields: [studentId], references: [id])

  @@unique([classSessionId, studentId])
  @@index([studentId])
}

// ==================== CHECK-IN ====================

model Checkin {
  id          String    @id @default(cuid())
  locationId  String
  studentId   String

  checkinAt   DateTime  @default(now())
  checkoutAt  DateTime?
  method      String    @default("manual") // manual, qrcode, card, biometric

  location    Location  @relation(fields: [locationId], references: [id])
  student     Student   @relation(fields: [studentId], references: [id])

  @@index([locationId])
  @@index([studentId])
  @@index([checkinAt])
}

// ==================== EXERCISES & WORKOUTS ====================

model Exercise {
  id              String    @id @default(cuid())
  businessId      String?   // null = exercicio global

  name            String
  description     String?
  instructions    String?

  category        ExerciseCategory
  muscleGroups    MuscleGroup[]
  equipment       String[]

  // Midia
  videoUrl        String?
  thumbnailUrl    String?
  gifUrl          String?
  images          String[]

  // Configuracoes
  difficulty      DifficultyLevel
  isCompound      Boolean   @default(false) // Exercicio composto
  isUnilateral    Boolean   @default(false) // Exercicio unilateral

  // Metricas possiveis
  hasReps         Boolean   @default(true)
  hasWeight       Boolean   @default(true)
  hasTime         Boolean   @default(false)
  hasDistance     Boolean   @default(false)

  isActive        Boolean   @default(true)
  isGlobal        Boolean   @default(false) // Disponivel para todos

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business? @relation(fields: [businessId], references: [id], onDelete: Cascade)
  workoutExercises WorkoutExercise[]
  personalRecords PersonalRecord[]

  @@index([businessId])
  @@index([category])
}

model WorkoutTemplate {
  id              String    @id @default(cuid())
  businessId      String
  professionalId  String?

  name            String
  description     String?
  type            WorkoutType
  difficulty      DifficultyLevel
  duration        Int?      // Duracao estimada em minutos

  // Organizacao
  category        String?   // Iniciante A, Hipertrofia B, etc
  tags            String[]

  isActive        Boolean   @default(true)
  isTemplate      Boolean   @default(true)

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  professional    Professional? @relation(fields: [professionalId], references: [id])
  exercises       WorkoutTemplateExercise[]
  workouts        Workout[]

  @@index([businessId])
}

model WorkoutTemplateExercise {
  id                String    @id @default(cuid())
  templateId        String
  exerciseId        String

  order             Int
  sets              Int
  reps              String?   // "10-12" ou "10"
  weight            String?   // "20kg" ou "progressivo"
  rest              Int?      // Segundos de descanso
  tempo             String?   // "3-1-2" (exc-pause-conc)
  notes             String?

  // Supersets/Circuits
  groupId           String?   // Agrupa exercicios (superset)
  groupType         String?   // superset, circuit, dropset

  template          WorkoutTemplate @relation(fields: [templateId], references: [id], onDelete: Cascade)

  @@index([templateId])
}

model Workout {
  id              String    @id @default(cuid())
  studentId       String
  templateId      String?

  name            String
  description     String?
  type            WorkoutType

  // Periodo de validade
  startDate       DateTime
  endDate         DateTime?

  // Frequencia
  frequency       Int?      // Vezes por semana
  dayOfWeek       Int[]     // Dias da semana [1,3,5]

  isActive        Boolean   @default(true)

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  template        WorkoutTemplate? @relation(fields: [templateId], references: [id])
  exercises       WorkoutExercise[]
  logs            WorkoutLog[]

  @@index([studentId])
}

model WorkoutExercise {
  id              String    @id @default(cuid())
  workoutId       String
  exerciseId      String

  order           Int
  sets            Int
  reps            String?
  weight          String?
  rest            Int?
  tempo           String?
  notes           String?

  // Supersets
  groupId         String?
  groupType       String?

  workout         Workout   @relation(fields: [workoutId], references: [id], onDelete: Cascade)
  exercise        Exercise  @relation(fields: [exerciseId], references: [id])
  logs            ExerciseLog[]

  @@index([workoutId])
}

// ==================== WORKOUT LOGS ====================

model WorkoutLog {
  id              String    @id @default(cuid())
  studentId       String
  workoutId       String?

  date            DateTime
  startTime       DateTime?
  endTime         DateTime?
  duration        Int?      // Duracao em minutos

  // Feedback
  rating          Int?      // 1-5
  difficulty      Int?      // 1-10 (RPE)
  notes           String?
  mood            String?   // great, good, ok, tired, exhausted

  // Metricas
  totalVolume     Float?    // Peso total levantado
  totalSets       Int?
  totalReps       Int?
  caloriesBurned  Int?

  createdAt       DateTime  @default(now())

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  workout         Workout?  @relation(fields: [workoutId], references: [id])
  exercises       ExerciseLog[]

  @@index([studentId])
  @@index([date])
}

model ExerciseLog {
  id                String    @id @default(cuid())
  workoutLogId      String
  workoutExerciseId String?

  // Sets executados
  sets              Json      // [{reps: 10, weight: 20, completed: true}, ...]

  // Feedback
  notes             String?
  wasHard           Boolean?

  createdAt         DateTime  @default(now())

  workoutLog        WorkoutLog @relation(fields: [workoutLogId], references: [id], onDelete: Cascade)
  workoutExercise   WorkoutExercise? @relation(fields: [workoutExerciseId], references: [id])

  @@index([workoutLogId])
}

// ==================== ASSESSMENTS (AVALIACOES) ====================

model Assessment {
  id              String    @id @default(cuid())
  studentId       String
  professionalId  String

  date            DateTime
  type            String    // initial, periodic, final

  // Antropometria basica
  weight          Float?    // kg
  height          Float?    // cm

  // Circunferencias (cm)
  neck            Float?
  chest           Float?
  waist           Float?
  hips            Float?
  rightArm        Float?
  leftArm         Float?
  rightForearm    Float?
  leftForearm     Float?
  rightThigh      Float?
  leftThigh       Float?
  rightCalf       Float?
  leftCalf        Float?

  // Dobras cutaneas (mm) - Protocolo Pollock
  triceps         Float?
  subscapular     Float?
  suprailiac      Float?
  abdominal       Float?
  thigh           Float?
  pectoral        Float?
  axilla          Float?

  // Composicao corporal calculada
  bodyFatPercent  Float?
  leanMass        Float?
  fatMass         Float?
  bmi             Float?

  // Bioimpedancia (se disponivel)
  bioimpedanceData Json?

  // Testes fisicos
  flexibility     Json?     // Sentar e alcancar, etc
  strength        Json?     // 1RM estimado, testes
  cardio          Json?     // VO2, Cooper, etc
  functional      Json?     // FMS, etc

  // Observacoes
  notes           String?
  recommendations String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  professional    Professional @relation(fields: [professionalId], references: [id])

  @@index([studentId])
  @@index([date])
}

model Measurement {
  id              String    @id @default(cuid())
  studentId       String
  date            DateTime

  weight          Float?
  bodyFatPercent  Float?
  muscleMass      Float?
  waterPercent    Float?
  visceralFat     Float?
  metabolicAge    Int?

  notes           String?
  source          String?   // manual, scale, bioimpedance

  createdAt       DateTime  @default(now())

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)

  @@index([studentId])
  @@index([date])
}

model ProgressPhoto {
  id          String    @id @default(cuid())
  studentId   String
  date        DateTime

  frontUrl    String?
  sideUrl     String?
  backUrl     String?

  weight      Float?
  notes       String?
  isPrivate   Boolean   @default(true)

  createdAt   DateTime  @default(now())

  student     Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)

  @@index([studentId])
}

model PersonalRecord {
  id          String    @id @default(cuid())
  studentId   String
  exerciseId  String

  weight      Float?    // kg
  reps        Int?
  time        Int?      // segundos
  distance    Float?    // metros

  date        DateTime
  notes       String?
  videoUrl    String?

  createdAt   DateTime  @default(now())

  student     Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  exercise    Exercise  @relation(fields: [exerciseId], references: [id])

  @@index([studentId])
  @@index([exerciseId])
}

// ==================== FISIOTERAPIA ====================

model MedicalRecord {
  id              String    @id @default(cuid())
  studentId       String    @unique

  // Anamnese
  mainComplaint   String?
  historyOfPresentIllness String?
  pastMedicalHistory String?
  familyHistory   String?
  socialHistory   String?

  // Medicamentos e alergias
  currentMedications Json?
  allergies       String[]

  // Condicoes
  conditions      String[]  // Hipertensao, Diabetes, etc
  surgeries       Json?     // Cirurgias anteriores

  // Ocupacional
  occupation      String?
  workPosture     String?
  physicalActivity String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  injuries        Injury[]
  diagnoses       Diagnosis[]
}

model Injury {
  id              String    @id @default(cuid())
  medicalRecordId String

  name            String
  description     String?
  bodyPart        String
  side            String?   // left, right, bilateral

  dateOfOnset     DateTime?
  mechanism       String?   // Como ocorreu
  status          InjuryStatus

  treatment       String?
  notes           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  medicalRecord   MedicalRecord @relation(fields: [medicalRecordId], references: [id], onDelete: Cascade)

  @@index([medicalRecordId])
}

model Diagnosis {
  id              String    @id @default(cuid())
  medicalRecordId String

  cid10           String?   // Codigo CID-10
  description     String
  diagnosedAt     DateTime
  diagnosedBy     String?

  notes           String?

  createdAt       DateTime  @default(now())

  medicalRecord   MedicalRecord @relation(fields: [medicalRecordId], references: [id], onDelete: Cascade)

  @@index([medicalRecordId])
}

model PhysioSession {
  id              String    @id @default(cuid())
  studentId       String
  professionalId  String

  date            DateTime
  type            PhysioSessionType
  duration        Int       // minutos

  // Avaliacao (para sessoes de avaliacao)
  painLevel       Int?      // 0-10
  functionalStatus String?
  physicalExam    Json?     // Exame fisico detalhado

  // Tratamento
  procedures      Json?     // Procedimentos realizados
  techniques      String[]  // Tecnicas utilizadas
  exercises       Json?     // Exercicios prescritos

  // Evolucao
  evolution       String?
  response        String?   // Resposta ao tratamento

  // Proxima sessao
  nextSessionPlan String?
  homeExercises   Json?     // Exercicios para casa

  // Anexos
  attachments     String[]  // URLs de arquivos

  notes           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  professional    Professional @relation(fields: [professionalId], references: [id])

  @@index([studentId])
  @@index([professionalId])
  @@index([date])
}

// ==================== PROGRAMS (CURSOS) ====================

model Program {
  id              String    @id @default(cuid())
  businessId      String

  name            String
  description     String?
  shortDescription String?

  type            String    // weight_loss, muscle_gain, challenge, etc
  difficulty      DifficultyLevel
  duration        Int       // Duracao em semanas

  // Conteudo
  totalModules    Int       @default(0)
  totalLessons    Int       @default(0)
  totalWorkouts   Int       @default(0)

  // Preco
  price           Float?
  isFreemium      Boolean   @default(false)

  // Midia
  thumbnailUrl    String?
  trailerUrl      String?

  isActive        Boolean   @default(true)
  isPublished     Boolean   @default(false)
  publishedAt     DateTime?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  modules         ProgramModule[]
  enrollments     ProgramEnrollment[]

  @@index([businessId])
}

model ProgramModule {
  id          String    @id @default(cuid())
  programId   String

  title       String
  description String?
  order       Int

  // Liberacao
  unlockAfterDays Int?    // Dias apos inicio para liberar
  unlockAfterModule String? // ID do modulo anterior

  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  program     Program   @relation(fields: [programId], references: [id], onDelete: Cascade)
  lessons     ProgramLesson[]

  @@index([programId])
}

model ProgramLesson {
  id          String    @id @default(cuid())
  moduleId    String

  title       String
  description String?
  type        String    // video, text, workout, quiz
  order       Int

  // Conteudo
  content     String?   // Texto/HTML
  videoUrl    String?
  duration    Int?      // Duracao em minutos
  workoutData Json?     // Treino estruturado

  // Recursos
  attachments String[]

  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  module      ProgramModule @relation(fields: [moduleId], references: [id], onDelete: Cascade)
  progress    LessonProgress[]

  @@index([moduleId])
}

model ProgramEnrollment {
  id              String    @id @default(cuid())
  studentId       String
  programId       String

  startDate       DateTime
  completedAt     DateTime?

  progress        Float     @default(0) // 0-100
  currentModuleId String?
  currentLessonId String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  program         Program   @relation(fields: [programId], references: [id])
  lessonProgress  LessonProgress[]

  @@unique([studentId, programId])
  @@index([studentId])
}

model LessonProgress {
  id              String    @id @default(cuid())
  enrollmentId    String
  lessonId        String

  status          String    @default("not_started") // not_started, in_progress, completed
  startedAt       DateTime?
  completedAt     DateTime?

  // Para videos
  watchedSeconds  Int       @default(0)

  // Para quizzes
  quizScore       Float?

  enrollment      ProgramEnrollment @relation(fields: [enrollmentId], references: [id], onDelete: Cascade)
  lesson          ProgramLesson @relation(fields: [lessonId], references: [id])

  @@unique([enrollmentId, lessonId])
}

// ==================== GAMIFICATION ====================

model Goal {
  id              String    @id @default(cuid())
  studentId       String

  type            GoalType
  title           String
  description     String?

  // Meta
  targetValue     Float
  currentValue    Float     @default(0)
  unit            String    // kg, %, cm, sessions, etc

  // Periodo
  startDate       DateTime
  targetDate      DateTime
  completedAt     DateTime?

  // Status
  status          String    @default("active") // active, completed, failed, abandoned

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  student         Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)

  @@index([studentId])
}

model Badge {
  id          String    @id @default(cuid())

  name        String
  description String
  type        BadgeType

  // Criterio
  criteria    Json      // Criterios para ganhar

  // Visual
  iconUrl     String?
  color       String?

  // Pontos
  points      Int       @default(0)

  isActive    Boolean   @default(true)

  createdAt   DateTime  @default(now())

  students    StudentBadge[]
}

model StudentBadge {
  id          String    @id @default(cuid())
  studentId   String
  badgeId     String

  earnedAt    DateTime  @default(now())

  student     Student   @relation(fields: [studentId], references: [id], onDelete: Cascade)
  badge       Badge     @relation(fields: [badgeId], references: [id])

  @@unique([studentId, badgeId])
}

model Challenge {
  id              String    @id @default(cuid())
  businessId      String

  name            String
  description     String

  type            String    // attendance, volume, weight_loss, etc

  // Regras
  rules           Json
  targetValue     Float
  unit            String

  // Periodo
  startDate       DateTime
  endDate         DateTime

  // Premios
  prizes          Json?
  points          Int       @default(0)

  // Configuracoes
  isTeamBased     Boolean   @default(false)
  maxParticipants Int?

  isActive        Boolean   @default(true)

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)
  participations  ChallengeParticipation[]

  @@index([businessId])
}

model ChallengeParticipation {
  id              String    @id @default(cuid())
  challengeId     String
  studentId       String

  currentValue    Float     @default(0)
  rank            Int?

  joinedAt        DateTime  @default(now())
  completedAt     DateTime?

  challenge       Challenge @relation(fields: [challengeId], references: [id], onDelete: Cascade)
  student         Student   @relation(fields: [studentId], references: [id])

  @@unique([challengeId, studentId])
}

// ==================== FINANCE ====================

model Transaction {
  id              String    @id @default(cuid())
  businessId      String

  type            String    // income, expense
  category        String    // subscription, service, product, salary, rent, etc

  description     String
  amount          Float

  date            DateTime
  dueDate         DateTime?
  paidAt          DateTime?

  status          PaymentStatus
  paymentMethod   PaymentMethod?

  // Referencia
  referenceType   String?   // subscription, appointment, etc
  referenceId     String?

  notes           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)

  @@index([businessId])
  @@index([date])
  @@index([status])
}

model Payment {
  id              String    @id @default(cuid())
  subscriptionId  String?
  studentId       String

  amount          Float
  discount        Float     @default(0)
  finalAmount     Float

  dueDate         DateTime
  paidAt          DateTime?

  status          PaymentStatus
  method          PaymentMethod?

  // Gateway
  gatewayId       String?
  gatewayResponse Json?

  notes           String?

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  subscription    Subscription? @relation(fields: [subscriptionId], references: [id])
  student         Student   @relation(fields: [studentId], references: [id])

  @@index([studentId])
  @@index([status])
  @@index([dueDate])
}

model Commission {
  id              String    @id @default(cuid())
  professionalId  String

  referenceType   String    // appointment, class, sale
  referenceId     String

  amount          Float
  rate            Float     // Percentual aplicado

  date            DateTime
  paidAt          DateTime?

  notes           String?

  createdAt       DateTime  @default(now())

  professional    Professional @relation(fields: [professionalId], references: [id])

  @@index([professionalId])
  @@index([date])
}

// ==================== MARKETING ====================

model Campaign {
  id              String    @id @default(cuid())
  businessId      String

  name            String
  type            String    // whatsapp, email, sms, push

  // Segmentacao
  targetSegment   String    // all, inactive, vip, birthday, etc
  targetFilters   Json?

  // Conteudo
  subject         String?
  content         String
  mediaUrl        String?

  // Agendamento
  scheduledAt     DateTime?
  sentAt          DateTime?

  // Metricas
  totalRecipients Int       @default(0)
  delivered       Int       @default(0)
  opened          Int       @default(0)
  clicked         Int       @default(0)

  status          String    @default("draft") // draft, scheduled, sending, sent

  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  business        Business  @relation(fields: [businessId], references: [id], onDelete: Cascade)

  @@index([businessId])
}

// ==================== NOTIFICATIONS ====================

model Notification {
  id          String           @id @default(cuid())
  studentId   String

  type        NotificationType
  title       String
  message     String

  // Envio
  channel     String           // whatsapp, push, email
  sentAt      DateTime?
  readAt      DateTime?

  // Referencia
  referenceType String?
  referenceId   String?

  createdAt   DateTime         @default(now())

  student     Student          @relation(fields: [studentId], references: [id], onDelete: Cascade)

  @@index([studentId])
  @@index([type])
}
```

---

## PARTE 6: Endpoints da API

### 6.1 Autenticacao

```
POST   /api/auth/register           # Registro de usuario
POST   /api/auth/login              # Login
POST   /api/auth/logout             # Logout
POST   /api/auth/refresh            # Refresh token
POST   /api/auth/forgot-password    # Esqueci senha
POST   /api/auth/reset-password     # Resetar senha
GET    /api/auth/me                 # Usuario atual
```

### 6.2 Alunos/Pacientes

```
GET    /api/students                # Listar alunos
POST   /api/students                # Criar aluno
GET    /api/students/:id            # Detalhes do aluno
PUT    /api/students/:id            # Atualizar aluno
DELETE /api/students/:id            # Remover aluno

GET    /api/students/:id/workouts   # Treinos do aluno
GET    /api/students/:id/assessments # Avaliacoes do aluno
GET    /api/students/:id/progress   # Evolucao do aluno
GET    /api/students/:id/appointments # Agendamentos do aluno
GET    /api/students/:id/checkins   # Check-ins do aluno
GET    /api/students/:id/payments   # Pagamentos do aluno
GET    /api/students/:id/goals      # Metas do aluno
GET    /api/students/:id/badges     # Badges do aluno
GET    /api/students/:id/stats      # Estatisticas do aluno
```

### 6.3 Profissionais

```
GET    /api/professionals           # Listar profissionais
POST   /api/professionals           # Criar profissional
GET    /api/professionals/:id       # Detalhes
PUT    /api/professionals/:id       # Atualizar
DELETE /api/professionals/:id       # Remover

GET    /api/professionals/:id/schedule      # Agenda do profissional
GET    /api/professionals/:id/appointments  # Atendimentos
GET    /api/professionals/:id/students      # Alunos vinculados
GET    /api/professionals/:id/commissions   # Comissoes
GET    /api/professionals/:id/availability  # Disponibilidade
```

### 6.4 Agendamentos

```
GET    /api/appointments            # Listar agendamentos
POST   /api/appointments            # Criar agendamento
GET    /api/appointments/:id        # Detalhes
PUT    /api/appointments/:id        # Atualizar
DELETE /api/appointments/:id        # Cancelar

POST   /api/appointments/:id/confirm    # Confirmar
POST   /api/appointments/:id/complete   # Concluir
POST   /api/appointments/:id/no-show    # Marcar falta

GET    /api/appointments/availability   # Horarios disponiveis
GET    /api/appointments/conflicts      # Verificar conflitos
```

### 6.5 Aulas Coletivas

```
GET    /api/classes                 # Listar aulas
POST   /api/classes                 # Criar aula
GET    /api/classes/:id             # Detalhes
PUT    /api/classes/:id             # Atualizar
DELETE /api/classes/:id             # Remover

GET    /api/classes/:id/sessions    # Sessoes da aula
POST   /api/classes/:id/sessions    # Criar sessao
GET    /api/classes/:id/sessions/:sessionId/attendees # Participantes

POST   /api/class-sessions/:id/book     # Reservar vaga
POST   /api/class-sessions/:id/cancel   # Cancelar reserva
POST   /api/class-sessions/:id/checkin  # Check-in na aula
```

### 6.6 Check-in

```
GET    /api/checkins                # Listar check-ins
POST   /api/checkins                # Registrar check-in
POST   /api/checkins/:id/checkout   # Registrar checkout

GET    /api/checkins/today          # Check-ins de hoje
GET    /api/checkins/stats          # Estatisticas de frequencia
```

### 6.7 Exercicios

```
GET    /api/exercises               # Listar exercicios
POST   /api/exercises               # Criar exercicio
GET    /api/exercises/:id           # Detalhes
PUT    /api/exercises/:id           # Atualizar
DELETE /api/exercises/:id           # Remover

GET    /api/exercises/categories    # Categorias
GET    /api/exercises/search        # Buscar exercicios
POST   /api/exercises/import        # Importar biblioteca
```

### 6.8 Treinos

```
GET    /api/workout-templates       # Templates de treino
POST   /api/workout-templates       # Criar template
GET    /api/workout-templates/:id   # Detalhes
PUT    /api/workout-templates/:id   # Atualizar
DELETE /api/workout-templates/:id   # Remover
POST   /api/workout-templates/:id/duplicate # Duplicar

GET    /api/workouts                # Treinos prescritos
POST   /api/workouts                # Prescrever treino
GET    /api/workouts/:id            # Detalhes
PUT    /api/workouts/:id            # Atualizar
DELETE /api/workouts/:id            # Remover

POST   /api/workout-logs            # Registrar treino realizado
GET    /api/workout-logs            # Historico de treinos
GET    /api/workout-logs/:id        # Detalhes do log
```

### 6.9 Avaliacoes

```
GET    /api/assessments             # Listar avaliacoes
POST   /api/assessments             # Criar avaliacao
GET    /api/assessments/:id         # Detalhes
PUT    /api/assessments/:id         # Atualizar
DELETE /api/assessments/:id         # Remover

GET    /api/assessments/:id/compare # Comparar com anterior
POST   /api/assessments/:id/pdf     # Gerar PDF

GET    /api/measurements            # Medidas rapidas
POST   /api/measurements            # Registrar medida

GET    /api/progress-photos         # Fotos de progresso
POST   /api/progress-photos         # Upload foto
DELETE /api/progress-photos/:id     # Remover foto

GET    /api/personal-records        # Records pessoais
POST   /api/personal-records        # Registrar PR
```

### 6.10 Fisioterapia (Prontuario)

```
GET    /api/medical-records/:studentId      # Prontuario do paciente
PUT    /api/medical-records/:studentId      # Atualizar prontuario

GET    /api/medical-records/:studentId/injuries     # Lesoes
POST   /api/medical-records/:studentId/injuries     # Adicionar lesao
PUT    /api/medical-records/:studentId/injuries/:id # Atualizar lesao

GET    /api/medical-records/:studentId/diagnoses    # Diagnosticos
POST   /api/medical-records/:studentId/diagnoses    # Adicionar diagnostico

GET    /api/physio-sessions                 # Sessoes de fisio
POST   /api/physio-sessions                 # Criar sessao
GET    /api/physio-sessions/:id             # Detalhes
PUT    /api/physio-sessions/:id             # Atualizar

POST   /api/physio-sessions/:id/report      # Gerar relatorio
POST   /api/physio-sessions/:id/evolution   # Registrar evolucao
```

### 6.11 Planos e Assinaturas

```
GET    /api/plans                   # Listar planos
POST   /api/plans                   # Criar plano
GET    /api/plans/:id               # Detalhes
PUT    /api/plans/:id               # Atualizar
DELETE /api/plans/:id               # Remover

GET    /api/subscriptions           # Listar assinaturas
POST   /api/subscriptions           # Criar assinatura
GET    /api/subscriptions/:id       # Detalhes
PUT    /api/subscriptions/:id       # Atualizar

POST   /api/subscriptions/:id/pause   # Pausar
POST   /api/subscriptions/:id/resume  # Retomar
POST   /api/subscriptions/:id/cancel  # Cancelar
POST   /api/subscriptions/:id/renew   # Renovar
```

### 6.12 Programas/Cursos

```
GET    /api/programs                # Listar programas
POST   /api/programs                # Criar programa
GET    /api/programs/:id            # Detalhes
PUT    /api/programs/:id            # Atualizar
DELETE /api/programs/:id            # Remover

GET    /api/programs/:id/modules    # Modulos
POST   /api/programs/:id/modules    # Adicionar modulo

GET    /api/program-modules/:id/lessons  # Licoes do modulo
POST   /api/program-modules/:id/lessons  # Adicionar licao

POST   /api/programs/:id/enroll     # Matricular aluno
GET    /api/enrollments             # Minhas matriculas
GET    /api/enrollments/:id         # Detalhes da matricula
POST   /api/enrollments/:id/progress # Atualizar progresso
```

### 6.13 Gamificacao

```
GET    /api/goals                   # Listar metas
POST   /api/goals                   # Criar meta
PUT    /api/goals/:id               # Atualizar meta
POST   /api/goals/:id/complete      # Completar meta

GET    /api/badges                  # Badges disponiveis
GET    /api/badges/my               # Meus badges

GET    /api/challenges              # Desafios ativos
GET    /api/challenges/:id          # Detalhes do desafio
POST   /api/challenges/:id/join     # Participar
GET    /api/challenges/:id/leaderboard # Ranking

GET    /api/leaderboard             # Ranking geral
GET    /api/leaderboard/weekly      # Ranking semanal
```

### 6.14 Financeiro

```
GET    /api/transactions            # Listar transacoes
POST   /api/transactions            # Criar transacao
GET    /api/transactions/:id        # Detalhes
PUT    /api/transactions/:id        # Atualizar
DELETE /api/transactions/:id        # Remover

GET    /api/payments                # Pagamentos
POST   /api/payments                # Registrar pagamento
GET    /api/payments/pending        # Pendentes
GET    /api/payments/overdue        # Em atraso

GET    /api/commissions             # Comissoes
GET    /api/commissions/summary     # Resumo por profissional
POST   /api/commissions/pay         # Pagar comissoes

GET    /api/finance/dashboard       # Dashboard financeiro
GET    /api/finance/reports         # Relatorios
```

### 6.15 Marketing e Notificacoes

```
GET    /api/campaigns               # Listar campanhas
POST   /api/campaigns               # Criar campanha
GET    /api/campaigns/:id           # Detalhes
PUT    /api/campaigns/:id           # Atualizar
DELETE /api/campaigns/:id           # Remover
POST   /api/campaigns/:id/send      # Enviar campanha
GET    /api/campaigns/:id/stats     # Estatisticas

GET    /api/notifications           # Notificacoes
POST   /api/notifications/send      # Enviar notificacao
PUT    /api/notifications/:id/read  # Marcar como lida
```

### 6.16 WhatsApp

```
POST   /api/whatsapp/instance       # Criar instancia
GET    /api/whatsapp/instance       # Status da instancia
GET    /api/whatsapp/qrcode         # Obter QR Code
POST   /api/whatsapp/webhook        # Webhook de mensagens

POST   /api/whatsapp/send-text      # Enviar texto
POST   /api/whatsapp/send-media     # Enviar midia
POST   /api/whatsapp/send-template  # Enviar template
```

### 6.17 Relatorios

```
GET    /api/reports/overview        # Visao geral
GET    /api/reports/attendance      # Frequencia
GET    /api/reports/revenue         # Faturamento
GET    /api/reports/churn           # Taxa de cancelamento
GET    /api/reports/retention       # Retencao
GET    /api/reports/professionals   # Por profissional
GET    /api/reports/services        # Por servico
GET    /api/reports/classes         # Por aula
GET    /api/reports/export          # Exportar dados
```

---

## PARTE 7: Paginas do Dashboard (Frontend)

### 7.1 Paginas Principais

```
/dashboard              # Home com metricas
/alunos                 # Lista de alunos
/alunos/novo            # Cadastro de aluno
/alunos/[id]            # Perfil do aluno
/alunos/[id]/evolucao   # Evolucao detalhada
/alunos/[id]/treinos    # Treinos do aluno
/alunos/[id]/avaliacoes # Avaliacoes
/alunos/[id]/pagamentos # Financeiro do aluno
```

### 7.2 Agenda

```
/agenda                 # Visao calendario
/agenda/dia             # Agenda do dia
/agenda/novo            # Novo agendamento
/agenda/[id]            # Detalhes agendamento
```

### 7.3 Treinos

```
/treinos                # Biblioteca de templates
/treinos/novo           # Criar template
/treinos/[id]           # Editar template
/treinos/prescrever     # Prescrever treino
/treinos/logs           # Historico de treinos
```

### 7.4 Exercicios

```
/exercicios             # Biblioteca de exercicios
/exercicios/novo        # Criar exercicio
/exercicios/[id]        # Editar exercicio
/exercicios/importar    # Importar biblioteca
```

### 7.5 Avaliacoes

```
/avaliacoes             # Lista de avaliacoes
/avaliacoes/nova        # Nova avaliacao
/avaliacoes/[id]        # Detalhes/Editar
/avaliacoes/comparar    # Comparar avaliacoes
```

### 7.6 Aulas Coletivas

```
/turmas                 # Grade de aulas
/turmas/nova            # Nova aula
/turmas/[id]            # Detalhes da aula
/turmas/[id]/sessoes    # Sessoes
/turmas/calendario      # Calendario de aulas
```

### 7.7 Check-in

```
/checkin                # Painel de check-in
/checkin/historico      # Historico
/checkin/estatisticas   # Estatisticas de frequencia
```

### 7.8 Fisioterapia

```
/prontuario             # Lista de pacientes
/prontuario/[id]        # Prontuario completo
/prontuario/[id]/sessoes # Sessoes
/prontuario/[id]/nova-sessao # Nova sessao
/prontuario/[id]/relatorio # Gerar relatorio
```

### 7.9 Programas

```
/programas              # Lista de programas
/programas/novo         # Criar programa
/programas/[id]         # Editar programa
/programas/[id]/modulos # Gerenciar modulos
/programas/[id]/alunos  # Alunos matriculados
```

### 7.10 Gamificacao

```
/gamificacao            # Dashboard gamificacao
/gamificacao/desafios   # Desafios
/gamificacao/desafios/novo # Novo desafio
/gamificacao/ranking    # Leaderboard
/gamificacao/badges     # Badges
```

### 7.11 Financeiro

```
/financeiro             # Dashboard financeiro
/financeiro/transacoes  # Transacoes
/financeiro/pagamentos  # Pagamentos de alunos
/financeiro/comissoes   # Comissoes profissionais
/financeiro/planos      # Planos disponiveis
/financeiro/relatorios  # Relatorios financeiros
```

### 7.12 Marketing

```
/marketing              # Dashboard marketing
/marketing/campanhas    # Campanhas
/marketing/campanhas/nova # Nova campanha
/marketing/segmentos    # Segmentacao
/marketing/automacoes   # Automacoes
```

### 7.13 Equipe

```
/equipe                 # Lista de profissionais
/equipe/novo            # Novo profissional
/equipe/[id]            # Perfil do profissional
/equipe/[id]/agenda     # Agenda do profissional
/equipe/escalas         # Escalas de trabalho
```

### 7.14 Configuracoes

```
/configuracoes          # Geral
/configuracoes/perfil   # Perfil do negocio
/configuracoes/horarios # Horarios de funcionamento
/configuracoes/servicos # Servicos oferecidos
/configuracoes/locais   # Unidades
/configuracoes/whatsapp # Integracao WhatsApp
/configuracoes/pagamentos # Gateway de pagamento
/configuracoes/usuarios # Usuarios do sistema
```

---

## PARTE 8: App do Aluno (Mobile/PWA)

### 8.1 Funcionalidades do App

```
/home                   # Dashboard pessoal
/treino                 # Treino do dia
/treino/[id]            # Executar treino
/treino/historico       # Historico de treinos

/agenda                 # Meus agendamentos
/agenda/agendar         # Novo agendamento
/agenda/aulas           # Aulas disponiveis

/evolucao               # Minha evolucao
/evolucao/medidas       # Minhas medidas
/evolucao/fotos         # Fotos de progresso
/evolucao/records       # Meus PRs

/perfil                 # Meu perfil
/perfil/metas           # Minhas metas
/perfil/badges          # Minhas conquistas
/perfil/assinatura      # Minha assinatura

/comunidade             # Feed/Comunidade
/comunidade/desafios    # Desafios ativos
/comunidade/ranking     # Ranking

/programas              # Meus programas
/programas/[id]         # Conteudo do programa

/notificacoes           # Central de notificacoes
```

### 8.2 Recursos do App

- Treino offline (sincroniza depois)
- Timer de descanso
- Contador de series
- Video dos exercicios
- Registro de carga
- Selfie de conclusao
- Notificacoes push
- Widget de treino do dia

---

## PARTE 9: Automacoes WhatsApp

### 9.1 Automacoes Configuradas

| Trigger | Acao | Timing |
|---------|------|--------|
| Agendamento criado | Confirmacao + instrucoes | Imediato |
| 24h antes | Lembrete de agendamento | 24h antes |
| 1h antes | Lembrete final | 1h antes |
| Agendamento concluido | Pesquisa de satisfacao | 2h depois |
| No-show | Mensagem de reagendamento | 30min depois |
| Pagamento pendente | Lembrete de pagamento | 3 dias antes |
| Pagamento atrasado | Cobranca | No vencimento |
| Inatividade 7 dias | Motivacao | 7 dias sem treino |
| Inatividade 30 dias | Reativacao | 30 dias sem visita |
| Aniversario | Felicitacao + presente | No dia |
| Meta atingida | Parabens | Imediato |
| Novo badge | Conquista desbloqueada | Imediato |
| Renovacao proxima | Lembrete de renovacao | 7 dias antes |
| Aula cancelada | Aviso aos participantes | Imediato |

### 9.2 Templates de Mensagem

```javascript
// Confirmacao de agendamento
const appointmentConfirmation = {
  text: `Ola {{nome}}!

Seu agendamento foi confirmado:
- Servico: {{servico}}
- Data: {{data}}
- Horario: {{horario}}
- Profissional: {{profissional}}

Endereco: {{endereco}}

Para cancelar ou remarcar, responda esta mensagem.

Ate la! 💪`,
};

// Lembrete de treino
const workoutReminder = {
  text: `Bom dia {{nome}}! 🌅

Hoje e dia de treino! Seu treino de {{tipo}} esta te esperando.

Vamos manter o ritmo? Sua sequencia atual e de {{streak}} dias consecutivos!

Abra o app para ver seu treino do dia 👇`,
};

// Conquista desbloqueada
const achievementUnlocked = {
  text: `🏆 PARABENS {{nome}}!

Voce desbloqueou uma nova conquista:
*{{badge_name}}*

{{badge_description}}

Continue assim! Voce ja tem {{total_badges}} conquistas!

Ver todas as conquistas no app 👇`,
};
```

---

## PARTE 10: Docker Compose Producao

```yaml
# docker-compose.prod.yml

services:
  postgres:
    image: postgres:15-alpine
    container_name: fis360_postgres
    restart: unless-stopped
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - fis360_network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    container_name: fis360_redis
    restart: unless-stopped
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data
    networks:
      - fis360_network
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5

  evolution-api:
    image: atendai/evolution-api:v2.1.1
    container_name: fis360_evolution
    restart: unless-stopped
    environment:
      - SERVER_URL=${EVOLUTION_SERVER_URL}
      - AUTHENTICATION_API_KEY=${EVOLUTION_API_KEY}
      - DATABASE_ENABLED=true
      - DATABASE_PROVIDER=postgresql
      - DATABASE_CONNECTION_URI=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@postgres:5432/evolution
      - DATABASE_CONNECTION_CLIENT_NAME=evolution
      - CACHE_REDIS_ENABLED=true
      - CACHE_REDIS_URI=redis://redis:6379
      - CACHE_REDIS_PREFIX_KEY=evolution
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    networks:
      - fis360_network

  api:
    build:
      context: .
      dockerfile: apps/api/Dockerfile
      target: production
    container_name: fis360_api
    restart: unless-stopped
    environment:
      - NODE_ENV=production
      - PORT=3001
      - DATABASE_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@postgres:5432/${POSTGRES_DB}
      - REDIS_URL=redis://redis:6379
      - JWT_SECRET=${JWT_SECRET}
      - JWT_REFRESH_SECRET=${JWT_REFRESH_SECRET}
      - EVOLUTION_API_URL=http://evolution-api:8080
      - EVOLUTION_API_KEY=${EVOLUTION_API_KEY}
      - CORS_ORIGIN=${CORS_ORIGIN}
      - AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
      - AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
      - AWS_S3_BUCKET=${AWS_S3_BUCKET}
      - STRIPE_SECRET_KEY=${STRIPE_SECRET_KEY}
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    networks:
      - fis360_network

  worker:
    build:
      context: .
      dockerfile: apps/api/Dockerfile
      target: production
    container_name: fis360_worker
    restart: unless-stopped
    command: node dist/worker.js
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@postgres:5432/${POSTGRES_DB}
      - REDIS_URL=redis://redis:6379
      - EVOLUTION_API_URL=http://evolution-api:8080
      - EVOLUTION_API_KEY=${EVOLUTION_API_KEY}
    depends_on:
      - api
    networks:
      - fis360_network

  web:
    build:
      context: .
      dockerfile: apps/web/Dockerfile
      target: production
    container_name: fis360_web
    restart: unless-stopped
    environment:
      - NODE_ENV=production
      - NEXT_PUBLIC_API_URL=${NEXT_PUBLIC_API_URL}
    depends_on:
      - api
    networks:
      - fis360_network

  nginx:
    image: nginx:alpine
    container_name: fis360_nginx
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/ssl:/etc/nginx/ssl:ro
      - ./nginx/conf.d:/etc/nginx/conf.d:ro
    depends_on:
      - web
      - api
      - evolution-api
    networks:
      - fis360_network

volumes:
  postgres_data:
  redis_data:

networks:
  fis360_network:
    driver: bridge
```

---

## PARTE 11: Diferenciais Competitivos

### 11.1 Para Academias

1. **Reducao de Churn**
   - Alertas de inatividade
   - Gamificacao para engajamento
   - Comunicacao proativa

2. **Ocupacao Inteligente**
   - Analise de horarios de pico
   - Precificacao dinamica
   - Incentivos para horarios vazios

3. **Experiencia Premium**
   - App do aluno moderno
   - Check-in automatico
   - Evolucao visual

### 11.2 Para Personal Trainers

1. **Escalabilidade**
   - Treinos online + presencial
   - Programas vendidos
   - Varios alunos simultaneos

2. **Profissionalismo**
   - App proprio
   - Prescricao digital
   - Relatorios automaticos

3. **Fidelizacao**
   - Historico completo
   - Metas e conquistas
   - Comunicacao automatizada

### 11.3 Para Fisioterapeutas

1. **Prontuario Inteligente**
   - Anamnese estruturada
   - Evolucao automatica
   - Laudos em 1 clique

2. **Acompanhamento Continuo**
   - Exercicios para casa
   - Monitoramento remoto
   - Comunicacao entre sessoes

3. **Conformidade**
   - CID-10 integrado
   - Relatorios para convenios
   - Assinatura digital

---

## PARTE 12: Integracao com Equipamentos

### 12.1 Integracoes Possiveis

- **Catracas**: Tecnologia, Control iD, Henry
- **Balancas**: InBody, Tanita, Omron
- **Smartwatches**: Apple Watch, Garmin, Fitbit
- **Apps de saude**: Apple Health, Google Fit, Strava
- **Equipamentos cardio**: Technogym, Life Fitness

### 12.2 API de Integracao

```javascript
// Webhook para receber dados de equipamentos
POST /api/integrations/webhook

// Dados de smartwatch
POST /api/integrations/wearables
{
  "studentId": "xxx",
  "source": "apple_health",
  "data": {
    "steps": 8500,
    "calories": 450,
    "heartRate": {
      "avg": 72,
      "max": 145,
      "resting": 58
    },
    "sleep": {
      "duration": 420,
      "quality": "good"
    }
  }
}
```

---

## PARTE 13: Checklist de Implementacao

### Fase 1: Setup Inicial (1-2 semanas)
- [ ] Criar monorepo com pnpm workspaces
- [ ] Configurar TypeScript em todos os pacotes
- [ ] Setup Prisma com schema inicial
- [ ] Configurar Docker Compose dev
- [ ] Setup ESLint + Prettier
- [ ] Criar estrutura de pastas

### Fase 2: Autenticacao (1 semana)
- [ ] Implementar registro/login
- [ ] JWT com refresh tokens
- [ ] Middleware de autenticacao
- [ ] Roles e permissoes
- [ ] Tela de login/registro

### Fase 3: CRUD Base (2 semanas)
- [ ] CRUD de alunos
- [ ] CRUD de profissionais
- [ ] CRUD de servicos
- [ ] CRUD de planos
- [ ] CRUD de assinaturas

### Fase 4: Agenda (1-2 semanas)
- [ ] API de agendamentos
- [ ] Verificacao de conflitos
- [ ] Calendario visual
- [ ] Agendamentos recorrentes
- [ ] Notificacoes

### Fase 5: Treinos (2-3 semanas)
- [ ] Biblioteca de exercicios
- [ ] Templates de treino
- [ ] Prescricao de treinos
- [ ] Registro de treinos (logs)
- [ ] App do aluno (treino)

### Fase 6: Avaliacoes (1-2 semanas)
- [ ] Formulario de avaliacao
- [ ] Calculos automaticos
- [ ] Fotos de progresso
- [ ] Comparacao de avaliacoes
- [ ] Graficos de evolucao

### Fase 7: Aulas e Check-in (1 semana)
- [ ] Grade de aulas
- [ ] Reserva de vagas
- [ ] Sistema de check-in
- [ ] Controle de frequencia

### Fase 8: Fisioterapia (2 semanas)
- [ ] Prontuario digital
- [ ] Sessoes de fisio
- [ ] Evolucao de paciente
- [ ] Geracao de laudos

### Fase 9: Financeiro (1-2 semanas)
- [ ] Gestao de pagamentos
- [ ] Calculo de comissoes
- [ ] Dashboard financeiro
- [ ] Relatorios

### Fase 10: WhatsApp (1 semana)
- [ ] Integracao Evolution API
- [ ] Templates de mensagem
- [ ] Automacoes configuradas
- [ ] Webhook de respostas

### Fase 11: Gamificacao (1 semana)
- [ ] Sistema de pontos
- [ ] Badges e conquistas
- [ ] Desafios
- [ ] Leaderboard

### Fase 12: App Mobile (2-3 semanas)
- [ ] Setup React Native/Expo
- [ ] Telas principais
- [ ] Execucao de treino
- [ ] Notificacoes push
- [ ] Modo offline

### Fase 13: Testes e Deploy (1-2 semanas)
- [ ] Testes unitarios
- [ ] Testes E2E
- [ ] Docker Compose prod
- [ ] CI/CD pipeline
- [ ] Monitoramento

---

## PARTE 14: Ideias Adicionais

### 14.1 Recursos Avancados

1. **IA para Treinos**
   - Geracao automatica de treinos
   - Ajuste de carga baseado em performance
   - Recomendacao de exercicios alternativos

2. **Analise de Video**
   - Correcao de postura por IA
   - Contagem automatica de reps
   - Feedback em tempo real

3. **Realidade Aumentada**
   - Demonstracao de exercicios em AR
   - Overlay de forma correta
   - Guia interativo

4. **Wearables Proprio**
   - Pulseira com a marca do negocio
   - Monitoramento em tempo real
   - Check-in automatico

### 14.2 Modelos de Monetizacao

1. **SaaS por Plano**
   - Starter: R$ 99/mes (ate 50 alunos)
   - Pro: R$ 199/mes (ate 200 alunos)
   - Enterprise: R$ 399/mes (ilimitado)

2. **Por Transacao**
   - Taxa sobre pagamentos processados
   - Comissao sobre vendas de programas

3. **White Label**
   - App com marca do cliente
   - Dominio proprio
   - Personalizacao total

---

*Documento gerado em 05/01/2026 baseado na experiencia do projeto Bela360*
