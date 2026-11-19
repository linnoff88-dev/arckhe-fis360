# Source Tree

## FIS360 - Estrutura de Diretorios

---

## Estrutura Completa

```
fis360/
│
├── apps/
│   │
│   ├── api/                              # Backend Express.js
│   │   ├── src/
│   │   │   ├── config/                   # Configuracoes
│   │   │   │   ├── env.ts               # Variaveis de ambiente
│   │   │   │   ├── database.ts          # Prisma client
│   │   │   │   └── redis.ts             # Redis client
│   │   │   │
│   │   │   ├── modules/                  # Modulos de dominio
│   │   │   │   ├── auth/
│   │   │   │   │   ├── auth.controller.ts
│   │   │   │   │   ├── auth.service.ts
│   │   │   │   │   ├── auth.routes.ts
│   │   │   │   │   ├── auth.schema.ts
│   │   │   │   │   └── auth.types.ts
│   │   │   │   │
│   │   │   │   ├── users/
│   │   │   │   │   ├── users.controller.ts
│   │   │   │   │   ├── users.service.ts
│   │   │   │   │   ├── users.routes.ts
│   │   │   │   │   ├── users.schema.ts
│   │   │   │   │   └── users.types.ts
│   │   │   │   │
│   │   │   │   ├── businesses/
│   │   │   │   │   ├── businesses.controller.ts
│   │   │   │   │   ├── businesses.service.ts
│   │   │   │   │   ├── businesses.routes.ts
│   │   │   │   │   └── businesses.types.ts
│   │   │   │   │
│   │   │   │   ├── students/
│   │   │   │   │   ├── students.controller.ts
│   │   │   │   │   ├── students.service.ts
│   │   │   │   │   ├── students.routes.ts
│   │   │   │   │   ├── students.schema.ts
│   │   │   │   │   └── students.types.ts
│   │   │   │   │
│   │   │   │   ├── professionals/
│   │   │   │   │   ├── professionals.controller.ts
│   │   │   │   │   ├── professionals.service.ts
│   │   │   │   │   └── professionals.routes.ts
│   │   │   │   │
│   │   │   │   ├── exercises/
│   │   │   │   │   ├── exercises.controller.ts
│   │   │   │   │   ├── exercises.service.ts
│   │   │   │   │   ├── exercises.routes.ts
│   │   │   │   │   └── exercises.schema.ts
│   │   │   │   │
│   │   │   │   ├── workout-templates/
│   │   │   │   │   ├── workout-templates.controller.ts
│   │   │   │   │   ├── workout-templates.service.ts
│   │   │   │   │   └── workout-templates.routes.ts
│   │   │   │   │
│   │   │   │   ├── workouts/
│   │   │   │   │   ├── workouts.controller.ts
│   │   │   │   │   ├── workouts.service.ts
│   │   │   │   │   ├── workouts.routes.ts
│   │   │   │   │   └── workouts.schema.ts
│   │   │   │   │
│   │   │   │   ├── workout-logs/
│   │   │   │   │   ├── workout-logs.controller.ts
│   │   │   │   │   ├── workout-logs.service.ts
│   │   │   │   │   └── workout-logs.routes.ts
│   │   │   │   │
│   │   │   │   ├── appointments/
│   │   │   │   │   ├── appointments.controller.ts
│   │   │   │   │   ├── appointments.service.ts
│   │   │   │   │   ├── appointments.routes.ts
│   │   │   │   │   └── appointments.schema.ts
│   │   │   │   │
│   │   │   │   ├── assessments/
│   │   │   │   │   ├── assessments.controller.ts
│   │   │   │   │   ├── assessments.service.ts
│   │   │   │   │   └── assessments.routes.ts
│   │   │   │   │
│   │   │   │   ├── gamification/
│   │   │   │   │   ├── gamification.controller.ts
│   │   │   │   │   ├── gamification.service.ts
│   │   │   │   │   ├── gamification.routes.ts
│   │   │   │   │   ├── badges.service.ts
│   │   │   │   │   └── leaderboard.service.ts
│   │   │   │   │
│   │   │   │   ├── notifications/
│   │   │   │   │   ├── notifications.controller.ts
│   │   │   │   │   ├── notifications.service.ts
│   │   │   │   │   └── notifications.routes.ts
│   │   │   │   │
│   │   │   │   ├── whatsapp/
│   │   │   │   │   ├── whatsapp.controller.ts
│   │   │   │   │   ├── whatsapp.service.ts
│   │   │   │   │   ├── whatsapp.routes.ts
│   │   │   │   │   └── templates.ts
│   │   │   │   │
│   │   │   │   └── reports/
│   │   │   │       ├── reports.controller.ts
│   │   │   │       ├── reports.service.ts
│   │   │   │       └── reports.routes.ts
│   │   │   │
│   │   │   ├── middlewares/
│   │   │   │   ├── auth.middleware.ts
│   │   │   │   ├── tenant.middleware.ts
│   │   │   │   ├── error.middleware.ts
│   │   │   │   ├── rate-limit.middleware.ts
│   │   │   │   └── validate.middleware.ts
│   │   │   │
│   │   │   ├── jobs/
│   │   │   │   ├── index.ts
│   │   │   │   ├── notifications.job.ts
│   │   │   │   ├── whatsapp.job.ts
│   │   │   │   ├── churn.job.ts
│   │   │   │   └── scheduler.ts
│   │   │   │
│   │   │   ├── queues/
│   │   │   │   ├── index.ts
│   │   │   │   └── processors.ts
│   │   │   │
│   │   │   ├── utils/
│   │   │   │   ├── logger.ts
│   │   │   │   ├── response.ts
│   │   │   │   ├── helpers.ts
│   │   │   │   ├── password.ts
│   │   │   │   └── jwt.ts
│   │   │   │
│   │   │   ├── types/
│   │   │   │   ├── express.d.ts
│   │   │   │   └── global.d.ts
│   │   │   │
│   │   │   ├── app.ts                    # Express app setup
│   │   │   ├── routes.ts                 # Route aggregator
│   │   │   ├── server.ts                 # Server entry point
│   │   │   └── worker.ts                 # Worker entry point
│   │   │
│   │   ├── prisma/
│   │   │   ├── schema.prisma             # Database schema
│   │   │   ├── seed.ts                   # Seed data
│   │   │   └── migrations/               # Database migrations
│   │   │
│   │   ├── tests/
│   │   │   ├── setup.ts
│   │   │   ├── helpers.ts
│   │   │   └── modules/
│   │   │       ├── auth.test.ts
│   │   │       ├── students.test.ts
│   │   │       └── workouts.test.ts
│   │   │
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   └── vitest.config.ts
│   │
│   ├── web/                              # Dashboard Next.js
│   │   ├── src/
│   │   │   ├── app/
│   │   │   │   ├── (auth)/
│   │   │   │   │   ├── login/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── register/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── forgot-password/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   └── layout.tsx
│   │   │   │   │
│   │   │   │   ├── (dashboard)/
│   │   │   │   │   ├── layout.tsx        # Dashboard layout
│   │   │   │   │   ├── page.tsx          # Home/Dashboard
│   │   │   │   │   │
│   │   │   │   │   ├── alunos/
│   │   │   │   │   │   ├── page.tsx      # Lista de alunos
│   │   │   │   │   │   ├── novo/
│   │   │   │   │   │   │   └── page.tsx  # Criar aluno
│   │   │   │   │   │   └── [id]/
│   │   │   │   │   │       ├── page.tsx  # Perfil do aluno
│   │   │   │   │   │       └── editar/
│   │   │   │   │   │           └── page.tsx
│   │   │   │   │   │
│   │   │   │   │   ├── exercicios/
│   │   │   │   │   │   ├── page.tsx
│   │   │   │   │   │   ├── novo/
│   │   │   │   │   │   │   └── page.tsx
│   │   │   │   │   │   └── [id]/
│   │   │   │   │   │       └── page.tsx
│   │   │   │   │   │
│   │   │   │   │   ├── treinos/
│   │   │   │   │   │   ├── page.tsx      # Templates
│   │   │   │   │   │   ├── novo/
│   │   │   │   │   │   │   └── page.tsx
│   │   │   │   │   │   └── [id]/
│   │   │   │   │   │       └── page.tsx
│   │   │   │   │   │
│   │   │   │   │   ├── agenda/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   │
│   │   │   │   │   ├── relatorios/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   │
│   │   │   │   │   └── configuracoes/
│   │   │   │   │       ├── page.tsx
│   │   │   │   │       ├── perfil/
│   │   │   │   │       │   └── page.tsx
│   │   │   │   │       └── whatsapp/
│   │   │   │   │           └── page.tsx
│   │   │   │   │
│   │   │   │   ├── api/                  # Route handlers
│   │   │   │   │   └── auth/
│   │   │   │   │       └── [...nextauth]/
│   │   │   │   │           └── route.ts
│   │   │   │   │
│   │   │   │   ├── layout.tsx            # Root layout
│   │   │   │   ├── not-found.tsx
│   │   │   │   └── globals.css
│   │   │   │
│   │   │   ├── components/
│   │   │   │   ├── ui/                   # shadcn components
│   │   │   │   │   ├── button.tsx
│   │   │   │   │   ├── input.tsx
│   │   │   │   │   ├── card.tsx
│   │   │   │   │   ├── dialog.tsx
│   │   │   │   │   ├── dropdown-menu.tsx
│   │   │   │   │   ├── table.tsx
│   │   │   │   │   ├── form.tsx
│   │   │   │   │   └── ...
│   │   │   │   │
│   │   │   │   ├── forms/
│   │   │   │   │   ├── student-form.tsx
│   │   │   │   │   ├── exercise-form.tsx
│   │   │   │   │   ├── workout-form.tsx
│   │   │   │   │   └── appointment-form.tsx
│   │   │   │   │
│   │   │   │   ├── tables/
│   │   │   │   │   ├── students-table.tsx
│   │   │   │   │   ├── exercises-table.tsx
│   │   │   │   │   └── data-table.tsx
│   │   │   │   │
│   │   │   │   ├── charts/
│   │   │   │   │   ├── attendance-chart.tsx
│   │   │   │   │   └── stats-chart.tsx
│   │   │   │   │
│   │   │   │   └── layout/
│   │   │   │       ├── sidebar.tsx
│   │   │   │       ├── header.tsx
│   │   │   │       ├── mobile-nav.tsx
│   │   │   │       └── user-nav.tsx
│   │   │   │
│   │   │   ├── hooks/
│   │   │   │   ├── use-students.ts
│   │   │   │   ├── use-exercises.ts
│   │   │   │   ├── use-workouts.ts
│   │   │   │   ├── use-auth.ts
│   │   │   │   └── use-debounce.ts
│   │   │   │
│   │   │   ├── lib/
│   │   │   │   ├── api.ts               # API client
│   │   │   │   ├── auth.ts              # Auth utilities
│   │   │   │   ├── utils.ts             # General utilities
│   │   │   │   └── validations.ts       # Shared schemas
│   │   │   │
│   │   │   ├── stores/
│   │   │   │   ├── auth-store.ts
│   │   │   │   └── ui-store.ts
│   │   │   │
│   │   │   └── types/
│   │   │       └── index.ts
│   │   │
│   │   ├── public/
│   │   │   ├── logo.svg
│   │   │   └── favicon.ico
│   │   │
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   ├── next.config.js
│   │   ├── tailwind.config.js
│   │   ├── postcss.config.js
│   │   └── tsconfig.json
│   │
│   └── student-app/                      # App do Aluno (PWA)
│       ├── src/
│       │   ├── app/
│       │   │   ├── (app)/
│       │   │   │   ├── layout.tsx
│       │   │   │   ├── page.tsx          # Home
│       │   │   │   │
│       │   │   │   ├── treino/
│       │   │   │   │   ├── page.tsx      # Treino do dia
│       │   │   │   │   └── [id]/
│       │   │   │   │       └── page.tsx  # Execucao do treino
│       │   │   │   │
│       │   │   │   ├── historico/
│       │   │   │   │   └── page.tsx
│       │   │   │   │
│       │   │   │   ├── evolucao/
│       │   │   │   │   └── page.tsx
│       │   │   │   │
│       │   │   │   ├── agenda/
│       │   │   │   │   └── page.tsx
│       │   │   │   │
│       │   │   │   ├── conquistas/
│       │   │   │   │   └── page.tsx
│       │   │   │   │
│       │   │   │   └── perfil/
│       │   │   │       └── page.tsx
│       │   │   │
│       │   │   ├── login/
│       │   │   │   └── page.tsx
│       │   │   │
│       │   │   ├── layout.tsx
│       │   │   └── globals.css
│       │   │
│       │   ├── components/
│       │   │   ├── workout/
│       │   │   │   ├── exercise-card.tsx
│       │   │   │   ├── set-input.tsx
│       │   │   │   ├── timer.tsx
│       │   │   │   └── video-player.tsx
│       │   │   │
│       │   │   ├── gamification/
│       │   │   │   ├── streak-badge.tsx
│       │   │   │   ├── points-display.tsx
│       │   │   │   └── badge-card.tsx
│       │   │   │
│       │   │   └── layout/
│       │   │       ├── bottom-nav.tsx
│       │   │       └── header.tsx
│       │   │
│       │   ├── hooks/
│       │   │   ├── use-workout.ts
│       │   │   └── use-offline.ts
│       │   │
│       │   ├── lib/
│       │   │   ├── api.ts
│       │   │   ├── offline-storage.ts
│       │   │   └── sync.ts
│       │   │
│       │   └── stores/
│       │       ├── workout-store.ts
│       │       └── auth-store.ts
│       │
│       ├── public/
│       │   ├── manifest.json
│       │   ├── sw.js
│       │   └── icons/
│       │       ├── icon-192.png
│       │       └── icon-512.png
│       │
│       ├── Dockerfile
│       ├── package.json
│       ├── next.config.js
│       └── tsconfig.json
│
├── packages/
│   └── shared/                           # Codigo compartilhado
│       ├── src/
│       │   ├── types/
│       │   │   ├── api.ts               # API response types
│       │   │   ├── models.ts            # Domain models
│       │   │   ├── enums.ts             # Shared enums
│       │   │   └── index.ts
│       │   │
│       │   ├── constants/
│       │   │   ├── exercise-categories.ts
│       │   │   ├── muscle-groups.ts
│       │   │   └── index.ts
│       │   │
│       │   ├── utils/
│       │   │   ├── format.ts
│       │   │   ├── date.ts
│       │   │   └── index.ts
│       │   │
│       │   ├── validators/
│       │   │   ├── student.ts
│       │   │   ├── exercise.ts
│       │   │   └── index.ts
│       │   │
│       │   └── index.ts
│       │
│       ├── package.json
│       └── tsconfig.json
│
├── docker/
│   ├── nginx/
│   │   ├── nginx.conf
│   │   └── conf.d/
│   │       └── default.conf
│   │
│   └── postgres/
│       └── init.sql
│
├── docs/                                 # Documentacao
│   ├── project-brief.md
│   ├── prd.md
│   ├── front-end-spec.md
│   ├── architecture.md
│   │
│   ├── prd/                             # PRD shardado
│   │   ├── epic-1-auth.md
│   │   ├── epic-2-students.md
│   │   └── ...
│   │
│   ├── architecture/                    # Arquitetura shardada
│   │   ├── coding-standards.md
│   │   ├── tech-stack.md
│   │   └── source-tree.md
│   │
│   └── stories/                         # User stories
│       └── story-001.md
│
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
│
├── docker-compose.yml                   # Desenvolvimento
├── docker-compose.prod.yml              # Producao
├── package.json                         # Root package
├── pnpm-workspace.yaml
├── turbo.json
├── .env.example
├── .gitignore
├── .eslintrc.js
├── .prettierrc
└── README.md
```

---

*Documento gerado em 06/01/2026*
