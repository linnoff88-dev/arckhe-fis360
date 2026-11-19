# Epico 2: Gestao de Alunos

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

CRUD completo de alunos com informacoes pessoais, objetivos, restricoes de saude e historico de atividades.

---

## User Stories

### US-2.1: Cadastro de Aluno

**Como** um profissional
**Quero** cadastrar um novo aluno
**Para** comecar a atende-lo

**Criterios de Aceite:**
- [ ] Formulario com dados pessoais (nome, email, telefone, nascimento)
- [ ] Campos opcionais: CPF, endereco, foto
- [ ] Selecao de objetivos (multiplos)
- [ ] Campo de observacoes de saude
- [ ] Campo de lesoes/restricoes
- [ ] Contato de emergencia

**Objetivos disponiveis:**
- WEIGHT_LOSS
- MUSCLE_GAIN
- STRENGTH
- ENDURANCE
- FLEXIBILITY
- REHABILITATION
- HEALTH
- SPORT_SPECIFIC
- BODY_RECOMPOSITION

---

### US-2.2: Listagem de Alunos

**Como** um profissional
**Quero** ver a lista de todos os meus alunos
**Para** gerenciar minha carteira

**Criterios de Aceite:**
- [ ] Lista paginada (20 por pagina)
- [ ] Busca por nome, email ou telefone
- [ ] Filtro por status (ativo, inativo, pausado)
- [ ] Filtro por objetivo
- [ ] Ordenacao por nome, data de cadastro, ultima atividade
- [ ] Indicador visual de risco de churn
- [ ] Acesso rapido ao WhatsApp

---

### US-2.3: Perfil do Aluno

**Como** um profissional
**Quero** ver o perfil completo de um aluno
**Para** ter visao 360 graus

**Criterios de Aceite:**
- [ ] Dados pessoais editaveis
- [ ] Historico de treinos
- [ ] Evolucao (graficos)
- [ ] Avaliacoes realizadas
- [ ] Fotos de progresso
- [ ] Assinaturas/pagamentos
- [ ] Timeline de atividades
- [ ] Proximos agendamentos

---

### US-2.4: Importacao de Alunos

**Como** um profissional
**Quero** importar alunos de uma planilha
**Para** migrar de outro sistema

**Criterios de Aceite:**
- [ ] Upload de arquivo CSV/Excel
- [ ] Mapeamento de colunas
- [ ] Preview antes de importar
- [ ] Tratamento de duplicados
- [ ] Relatorio de erros
- [ ] Importacao em background para listas grandes

---

### US-2.5: Convite para App do Aluno

**Como** um profissional
**Quero** convidar um aluno para usar o app
**Para** que ele acompanhe seus treinos

**Criterios de Aceite:**
- [ ] Botao "Convidar para app" no perfil
- [ ] Envio de link por WhatsApp ou email
- [ ] Link gera conta automatica para o aluno
- [ ] Aluno define senha no primeiro acesso
- [ ] Notificacao ao profissional quando aluno ativar

---

## Requisitos Tecnicos

- Soft delete para alunos (nunca apagar dados)
- Criptografia de dados sensiveis (CPF, saude)
- Indice full-text para busca
- Cache de listagem com invalidacao

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy

---

## Arquivos Relacionados

```
apps/api/src/modules/students/
├── students.controller.ts
├── students.service.ts
├── students.routes.ts
├── students.schema.ts
└── students.types.ts

apps/web/src/app/(dashboard)/alunos/
├── page.tsx              # Lista
├── novo/page.tsx         # Criar
└── [id]/
    ├── page.tsx          # Perfil
    └── editar/page.tsx   # Editar
```

---

*Referencia: docs/prd.md - Secao 5*
