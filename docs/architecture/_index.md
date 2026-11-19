# Arquitetura - Indice

## FIS360 - Documentacao Tecnica

---

## Documentos

| Documento | Descricao |
|-----------|-----------|
| [architecture.md](../architecture.md) | Documento principal de arquitetura |
| [coding-standards.md](./coding-standards.md) | Padroes de codigo TypeScript/React |
| [tech-stack.md](./tech-stack.md) | Stack tecnologico detalhado |
| [source-tree.md](./source-tree.md) | Estrutura de diretorios do monorepo |
| [api-design.md](./api-design.md) | Design da API REST |
| [database.md](./database.md) | Design do banco de dados |

---

## Topicos por Documento

### architecture.md (Principal)
- Visao geral de alto nivel
- Diagrama de arquitetura
- Principios arquiteturais
- Fluxo de autenticacao
- Multi-tenancy
- Cache e performance
- Background jobs
- Integracao WhatsApp
- Seguranca
- Monitoramento
- Deploy e CI/CD
- ADRs (Architectural Decision Records)

### coding-standards.md
- Configuracao TypeScript
- Convencoes de nomenclatura
- Padroes de imports
- Backend patterns (Controller, Service)
- Error handling
- Frontend patterns (Components, Hooks)
- React Query usage
- Forms com React Hook Form
- Testes
- Git commits

### tech-stack.md
- Stack backend (Node, Express, Prisma)
- Stack frontend (Next.js, React, Tailwind)
- PWA (Workbox, Service Worker)
- DevOps (Docker, Nginx)
- Servicos externos
- Versoes minimas

### source-tree.md
- Estrutura completa do monorepo
- Apps: api, web, student-app
- Packages: shared
- Docker configs
- Docs structure

### api-design.md
- Convencoes REST
- Formato de resposta
- Autenticacao
- Rate limiting
- Endpoints completos
- Paginacao
- Filtros e ordenacao

### database.md
- Modelos Prisma
- Enums
- Indices
- Migrations
- Seed data

---

## Quick Links

### Para Desenvolvedores
1. Comece por [tech-stack.md](./tech-stack.md) para entender as tecnologias
2. Leia [coding-standards.md](./coding-standards.md) para os padroes
3. Consulte [source-tree.md](./source-tree.md) para a estrutura

### Para Arquitetos
1. Leia [architecture.md](../architecture.md) completo
2. Revise [api-design.md](./api-design.md) para integracao
3. Consulte [database.md](./database.md) para o modelo

---

*Referencia: docs/architecture.md*
