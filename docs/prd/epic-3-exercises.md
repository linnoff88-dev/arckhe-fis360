# Epico 3: Biblioteca de Exercicios

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

Biblioteca completa de exercicios com videos demonstrativos, instrucoes e categorizacao por grupo muscular e equipamento.

---

## User Stories

### US-3.1: Visualizar Biblioteca

**Como** um profissional
**Quero** navegar pela biblioteca de exercicios
**Para** montar treinos

**Criterios de Aceite:**
- [ ] Grid de exercicios com thumbnail
- [ ] Filtro por categoria (peito, costas, pernas, etc)
- [ ] Filtro por equipamento
- [ ] Filtro por dificuldade
- [ ] Busca por nome
- [ ] Exercicios globais + exercicios do negocio

---

### US-3.2: Detalhes do Exercicio

**Como** um profissional ou aluno
**Quero** ver detalhes de um exercicio
**Para** entender a execucao correta

**Criterios de Aceite:**
- [ ] Video demonstrativo (loop)
- [ ] Nome e descricao
- [ ] Instrucoes passo a passo
- [ ] Musculos trabalhados (visual)
- [ ] Equipamento necessario
- [ ] Nivel de dificuldade
- [ ] Exercicios alternativos sugeridos

---

### US-3.3: Criar Exercicio Personalizado

**Como** um profissional
**Quero** criar um exercicio personalizado
**Para** adicionar a minha biblioteca

**Criterios de Aceite:**
- [ ] Formulario com nome, descricao, instrucoes
- [ ] Upload de video (ate 100MB)
- [ ] Selecao de categoria e musculos
- [ ] Selecao de equipamentos
- [ ] Definir dificuldade
- [ ] Opcao de clonar exercicio existente

---

### US-3.4: Biblioteca Global Seed

**Como** administrador da plataforma
**Quero** disponibilizar biblioteca inicial
**Para** que negocios ja tenham exercicios

**Criterios de Aceite:**
- [ ] Minimo 200 exercicios base
- [ ] Cobertura de todos os grupos musculares
- [ ] Videos de qualidade profissional
- [ ] Exercicios para iniciantes ate avancados
- [ ] Exercicios com e sem equipamento

---

## Categorias de Exercicios

```typescript
enum ExerciseCategory {
  CHEST = 'CHEST',
  BACK = 'BACK',
  SHOULDERS = 'SHOULDERS',
  BICEPS = 'BICEPS',
  TRICEPS = 'TRICEPS',
  FOREARMS = 'FOREARMS',
  ABS = 'ABS',
  QUADRICEPS = 'QUADRICEPS',
  HAMSTRINGS = 'HAMSTRINGS',
  GLUTES = 'GLUTES',
  CALVES = 'CALVES',
  FULL_BODY = 'FULL_BODY',
  CARDIO = 'CARDIO',
  MOBILITY = 'MOBILITY',
  REHABILITATION = 'REHABILITATION'
}
```

---

## Requisitos Tecnicos

- Videos em CDN (Bunny ou CloudFront)
- Transcoding automatico (720p, 480p)
- Lazy loading de videos
- Cache agressivo de thumbnails

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy

---

## Arquivos Relacionados

```
apps/api/src/modules/exercises/
├── exercises.controller.ts
├── exercises.service.ts
├── exercises.routes.ts
└── exercises.schema.ts

apps/web/src/app/(dashboard)/exercicios/
├── page.tsx              # Lista/Grid
├── novo/page.tsx         # Criar
└── [id]/page.tsx         # Detalhes

packages/shared/src/constants/
├── exercise-categories.ts
└── muscle-groups.ts
```

---

*Referencia: docs/prd.md - Secao 6*
