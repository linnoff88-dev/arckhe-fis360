# Stories - Indice

## FIS360 - User Stories para Desenvolvimento

---

## Backlog

### Epic 1: Autenticacao e Multi-tenancy

| Story | Titulo | Status | Prioridade |
|-------|--------|--------|------------|
| [001](./story-001-project-setup.md) | Project Setup e Infraestrutura Base | Draft | Must Have |
| [002](./story-002-auth-register.md) | Registro de Negocio | Draft | Must Have |
| 003 | Login de Usuario | Backlog | Must Have |
| 004 | Recuperacao de Senha | Backlog | Must Have |
| 005 | Gestao de Usuarios do Negocio | Backlog | Must Have |
| 006 | Perfil do Negocio | Backlog | Should Have |

### Epic 2: Gestao de Alunos

| Story | Titulo | Status | Prioridade |
|-------|--------|--------|------------|
| 007 | Cadastro de Aluno | Backlog | Must Have |
| 008 | Listagem de Alunos | Backlog | Must Have |
| 009 | Perfil do Aluno | Backlog | Must Have |
| 010 | Importacao de Alunos | Backlog | Should Have |
| 011 | Convite para App do Aluno | Backlog | Must Have |

### Epic 3: Biblioteca de Exercicios

| Story | Titulo | Status | Prioridade |
|-------|--------|--------|------------|
| 012 | Visualizar Biblioteca | Backlog | Must Have |
| 013 | Detalhes do Exercicio | Backlog | Must Have |
| 014 | Criar Exercicio Personalizado | Backlog | Should Have |
| 015 | Seed de Exercicios Globais | Backlog | Must Have |

### Epic 4: Prescricao de Treinos

| Story | Titulo | Status | Prioridade |
|-------|--------|--------|------------|
| 016 | Criar Template de Treino | Backlog | Must Have |
| 017 | Prescrever Treino para Aluno | Backlog | Must Have |
| 018 | Visualizar Treinos do Aluno | Backlog | Must Have |
| 019 | Divisao de Treino (ABC) | Backlog | Should Have |

### Epic 5: App do Aluno

| Story | Titulo | Status | Prioridade |
|-------|--------|--------|------------|
| 020 | Setup PWA Student App | Backlog | Must Have |
| 021 | Home do Aluno | Backlog | Must Have |
| 022 | Visualizar Treino | Backlog | Must Have |
| 023 | Executar Treino | Backlog | Must Have |
| 024 | Finalizar e Avaliar Treino | Backlog | Must Have |
| 025 | Historico de Treinos | Backlog | Should Have |
| 026 | Minha Evolucao | Backlog | Should Have |

---

## Status

- **Draft**: Story criada, aguardando revisao
- **Ready**: Story revisada e pronta para desenvolvimento
- **In Progress**: Em desenvolvimento
- **Review**: Em revisao de codigo
- **Done**: Concluida e deployada
- **Backlog**: Planejada mas ainda nao detalhada

---

## Ordem de Implementacao Sugerida

```
MVP Sprint 1 (Fundacao):
├── Story 001: Project Setup
├── Story 002: Registro
└── Story 003: Login

MVP Sprint 2 (Core):
├── Story 007: Cadastro Aluno
├── Story 008: Listagem Alunos
├── Story 012: Biblioteca Exercicios
└── Story 015: Seed Exercicios

MVP Sprint 3 (Treinos):
├── Story 016: Template Treino
├── Story 017: Prescrever Treino
├── Story 020: Setup PWA
└── Story 022: Visualizar Treino

MVP Sprint 4 (App Aluno):
├── Story 021: Home Aluno
├── Story 023: Executar Treino
├── Story 024: Finalizar Treino
└── Story 011: Convite App
```

---

## Convencoes

### Nomenclatura
- `story-XXX-<slug>.md`
- XXX = numero sequencial com 3 digitos
- slug = descricao curta em kebab-case

### Template de Story
Cada story deve conter:
1. Descricao (Como/Quero/Para)
2. Criterios de Aceite
3. Tarefas Tecnicas
4. Arquivos a Criar/Modificar
5. Testes
6. Referencias

---

*Atualizado em 06/01/2026*
