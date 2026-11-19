# Story 001: Project Setup e Infraestrutura Base

**Epic:** E1 - Autenticacao e Multi-tenancy
**Status:** Draft
**Prioridade:** Must Have
**Estimativa:** -

---

## Descricao

Configurar a infraestrutura base do projeto incluindo monorepo, Docker, banco de dados e estrutura inicial de codigo.

---

## Objetivo

Ter o ambiente de desenvolvimento funcionando com:
- Monorepo com pnpm workspaces
- Docker Compose para PostgreSQL e Redis
- Estrutura base da API Express
- Estrutura base do Dashboard Next.js
- Prisma configurado com schema inicial
- Lint, Prettier e TypeScript configurados

---

## Criterios de Aceite

### 1. Estrutura do Monorepo
- [ ] Criar estrutura de pastas conforme source-tree.md
- [ ] Configurar pnpm-workspace.yaml
- [ ] Configurar turbo.json
- [ ] Criar package.json root com scripts

### 2. Docker
- [ ] Criar docker-compose.yml com PostgreSQL e Redis
- [ ] Criar .env.example com variaveis necessarias
- [ ] Verificar que containers sobem corretamente

### 3. API (apps/api)
- [ ] Inicializar projeto Express com TypeScript
- [ ] Configurar estrutura de pastas (src/modules, middlewares, etc)
- [ ] Configurar Prisma com schema inicial
- [ ] Criar endpoint de health check (GET /health)
- [ ] Configurar variaveis de ambiente

### 4. Web Dashboard (apps/web)
- [ ] Inicializar projeto Next.js 14 com App Router
- [ ] Configurar TailwindCSS
- [ ] Instalar e configurar shadcn/ui
- [ ] Criar layout base
- [ ] Criar pagina inicial placeholder

### 5. Shared Package (packages/shared)
- [ ] Criar estrutura de types
- [ ] Exportar tipos basicos
- [ ] Configurar build

### 6. Qualidade de Codigo
- [ ] Configurar ESLint
- [ ] Configurar Prettier
- [ ] Configurar tsconfig base
- [ ] Configurar husky + lint-staged (opcional)

---

## Tarefas Tecnicas

### 1. Inicializacao

```bash
# Criar estrutura
mkdir -p apps/{api,web,student-app}/src
mkdir -p packages/shared/src
mkdir -p docker/{nginx,postgres}
mkdir -p docs/{prd,architecture,stories}

# Inicializar root
pnpm init

# Configurar workspaces
# pnpm-workspace.yaml
```

### 2. Docker Compose

```yaml
# docker-compose.yml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: fis360
      POSTGRES_PASSWORD: fis360dev
      POSTGRES_DB: fis360
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data

volumes:
  postgres_data:
  redis_data:
```

### 3. API Setup

```bash
cd apps/api
pnpm init
pnpm add express cors helmet zod bcrypt jsonwebtoken
pnpm add @prisma/client ioredis pino
pnpm add -D prisma typescript @types/node @types/express ts-node-dev
```

### 4. Prisma Schema Inicial

```prisma
// prisma/schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model Business {
  id        String   @id @default(cuid())
  name      String
  slug      String   @unique
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model User {
  id           String   @id @default(cuid())
  email        String   @unique
  passwordHash String
  createdAt    DateTime @default(now())
}
```

### 5. Web Setup

```bash
cd apps/web
pnpm create next-app . --typescript --tailwind --app --src-dir
pnpm add @tanstack/react-query zustand
pnpm dlx shadcn-ui@latest init
```

---

## Arquivos a Criar

```
fis360/
├── package.json
├── pnpm-workspace.yaml
├── turbo.json
├── docker-compose.yml
├── .env.example
├── .gitignore
├── .eslintrc.js
├── .prettierrc
│
├── apps/
│   ├── api/
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── prisma/
│   │   │   └── schema.prisma
│   │   └── src/
│   │       ├── app.ts
│   │       ├── server.ts
│   │       └── config/
│   │           ├── env.ts
│   │           └── database.ts
│   │
│   └── web/
│       ├── package.json
│       ├── tsconfig.json
│       ├── tailwind.config.js
│       ├── next.config.js
│       └── src/
│           └── app/
│               ├── layout.tsx
│               └── page.tsx
│
└── packages/
    └── shared/
        ├── package.json
        ├── tsconfig.json
        └── src/
            └── types/
                └── index.ts
```

---

## Validacao

1. `docker compose up -d` deve subir PostgreSQL e Redis
2. `pnpm install` na raiz deve instalar todas as dependencias
3. `pnpm --filter api dev` deve iniciar a API na porta 3001
4. `pnpm --filter web dev` deve iniciar o dashboard na porta 3000
5. Acessar http://localhost:3001/health deve retornar `{ "status": "ok" }`
6. Acessar http://localhost:3000 deve mostrar pagina inicial

---

## Notas

- Esta story e pre-requisito para todas as outras
- Foco em infraestrutura, nao em features
- Student App (PWA) sera configurado em story posterior

---

## Dependencias

- Nenhuma (story inicial)

---

## Referencias

- [source-tree.md](../architecture/source-tree.md)
- [tech-stack.md](../architecture/tech-stack.md)
- [coding-standards.md](../architecture/coding-standards.md)

---

*Story criada em 06/01/2026*
