# Tech Stack

## FIS360 - Stack Tecnologico

---

## 1. Overview

```
┌─────────────────────────────────────────────────────────────┐
│                      FRONTEND                                │
├─────────────────────────────────────────────────────────────┤
│  Next.js 14 │ React 18 │ TypeScript │ TailwindCSS           │
│  shadcn/ui │ React Query │ Zustand │ React Hook Form        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       BACKEND                                │
├─────────────────────────────────────────────────────────────┤
│  Node.js 20 │ Express.js │ TypeScript │ Prisma ORM          │
│  Zod │ BullMQ │ JWT │ bcrypt                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       DATABASE                               │
├─────────────────────────────────────────────────────────────┤
│  PostgreSQL 15 │ Redis 7 │ AWS S3/R2                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Backend Stack

### 2.1 Runtime & Framework

| Tecnologia | Versao | Proposito | Documentacao |
|------------|--------|-----------|--------------|
| Node.js | 20 LTS | Runtime JavaScript | https://nodejs.org/ |
| Express.js | 4.x | Framework HTTP | https://expressjs.com/ |
| TypeScript | 5.x | Tipagem estatica | https://typescriptlang.org/ |

### 2.2 Database & ORM

| Tecnologia | Versao | Proposito | Documentacao |
|------------|--------|-----------|--------------|
| PostgreSQL | 15 | Banco relacional | https://postgresql.org/ |
| Prisma | 5.x | ORM type-safe | https://prisma.io/ |
| Redis | 7 | Cache/Sessions/Queue | https://redis.io/ |

### 2.3 Autenticacao & Seguranca

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| jsonwebtoken | 9.x | JWT tokens |
| bcrypt | 5.x | Hash de senhas |
| helmet | 7.x | Headers de seguranca |
| cors | 2.x | CORS middleware |

### 2.4 Validacao & Utils

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Zod | 3.x | Schema validation |
| dayjs | 1.x | Manipulacao de datas |
| uuid | 9.x | Geracao de IDs |
| pino | 8.x | Logging |

### 2.5 Background Jobs

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| BullMQ | 5.x | Job queue |
| node-cron | 3.x | Agendamento (opcional) |

---

## 3. Frontend Stack

### 3.1 Framework & Build

| Tecnologia | Versao | Proposito | Documentacao |
|------------|--------|-----------|--------------|
| Next.js | 14 | Framework React | https://nextjs.org/ |
| React | 18 | UI Library | https://react.dev/ |
| TypeScript | 5.x | Tipagem estatica | https://typescriptlang.org/ |

### 3.2 Styling

| Tecnologia | Versao | Proposito | Documentacao |
|------------|--------|-----------|--------------|
| TailwindCSS | 3.x | Utility-first CSS | https://tailwindcss.com/ |
| shadcn/ui | - | Component library | https://ui.shadcn.com/ |
| Lucide React | - | Icons | https://lucide.dev/ |
| clsx/tailwind-merge | - | Class utilities | - |

### 3.3 State & Data

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| React Query | 5.x | Server state |
| Zustand | 4.x | Client state |
| React Hook Form | 7.x | Forms |
| @hookform/resolvers | - | Zod integration |

### 3.4 PWA (Student App)

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Workbox | 7.x | Service Worker |
| next-pwa | 5.x | PWA plugin |
| idb | 8.x | IndexedDB wrapper |

### 3.5 UI Utilities

| Tecnologia | Versao | Proposito |
|------------|--------|-----------|
| Recharts | 2.x | Graficos |
| react-hot-toast | 2.x | Notificacoes |
| date-fns | 3.x | Formatacao de datas |
| cmdk | - | Command palette |

---

## 4. DevOps & Infra

### 4.1 Containerizacao

| Tecnologia | Proposito |
|------------|-----------|
| Docker | Containerizacao |
| Docker Compose | Orquestracao local |

### 4.2 Web Server

| Tecnologia | Proposito |
|------------|-----------|
| Nginx | Reverse proxy |
| Let's Encrypt | SSL/TLS |

### 4.3 CI/CD

| Tecnologia | Proposito |
|------------|-----------|
| GitHub Actions | CI/CD pipeline |
| pnpm | Package manager |
| Turborepo | Monorepo build |

---

## 5. Servicos Externos

### 5.1 Comunicacao

| Servico | Proposito | Documentacao |
|---------|-----------|--------------|
| Evolution API v2 | WhatsApp Business | https://doc.evolution-api.com/ |
| Resend | Email transacional | https://resend.com/docs |

### 5.2 Storage

| Servico | Proposito |
|---------|-----------|
| AWS S3 / Cloudflare R2 | Object storage |
| Bunny CDN | Video streaming |

### 5.3 Pagamentos

| Servico | Proposito |
|---------|-----------|
| Stripe | Pagamentos internacionais |
| PagSeguro / Asaas | Pagamentos Brasil |

---

## 6. Development Tools

### 6.1 Qualidade de Codigo

| Ferramenta | Proposito |
|------------|-----------|
| ESLint | Linting |
| Prettier | Formatacao |
| Husky | Git hooks |
| lint-staged | Pre-commit linting |

### 6.2 Testes

| Ferramenta | Proposito |
|------------|-----------|
| Vitest | Unit/Integration tests |
| Playwright | E2E tests |
| MSW | API mocking |

### 6.3 Documentacao

| Ferramenta | Proposito |
|------------|-----------|
| TypeDoc | API docs |
| Storybook | Component docs |

---

## 7. Versoes Minimas

```json
{
  "engines": {
    "node": ">=20.0.0",
    "pnpm": ">=8.0.0"
  }
}
```

---

## 8. Instalacao Base

```bash
# Backend
pnpm add express cors helmet zod bcrypt jsonwebtoken
pnpm add @prisma/client bullmq ioredis pino
pnpm add -D prisma typescript @types/node @types/express vitest

# Frontend
pnpm add next react react-dom
pnpm add @tanstack/react-query zustand react-hook-form @hookform/resolvers
pnpm add tailwindcss postcss autoprefixer
pnpm add lucide-react clsx tailwind-merge class-variance-authority
pnpm add -D typescript @types/react @types/node
```

---

*Documento gerado em 06/01/2026*
