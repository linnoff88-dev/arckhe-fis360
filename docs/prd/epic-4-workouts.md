# Epico 4: Prescricao de Treinos

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Alta

---

## Descricao

Sistema completo para criar, prescrever e gerenciar treinos personalizados para alunos.

---

## User Stories

### US-4.1: Criar Template de Treino

**Como** um profissional
**Quero** criar um template de treino reutilizavel
**Para** agilizar a prescricao

**Criterios de Aceite:**
- [ ] Nome e descricao do treino
- [ ] Tipo (musculacao, cardio, HIIT, funcional, etc)
- [ ] Nivel de dificuldade
- [ ] Duracao estimada
- [ ] Adicionar exercicios com: series, reps, carga, descanso
- [ ] Ordenar exercicios (drag and drop)
- [ ] Agrupar exercicios (superset, circuito)
- [ ] Notas por exercicio
- [ ] Salvar como template

---

### US-4.2: Prescrever Treino para Aluno

**Como** um profissional
**Quero** prescrever um treino para um aluno
**Para** que ele execute

**Criterios de Aceite:**
- [ ] Selecionar aluno
- [ ] Criar treino do zero ou usar template
- [ ] Personalizar exercicios para o aluno
- [ ] Definir periodo de validade
- [ ] Definir dias da semana
- [ ] Definir frequencia semanal
- [ ] Notificar aluno via WhatsApp/push

---

### US-4.3: Visualizar Treinos do Aluno

**Como** um profissional
**Quero** ver todos os treinos de um aluno
**Para** acompanhar sua programacao

**Criterios de Aceite:**
- [ ] Lista de treinos ativos
- [ ] Historico de treinos anteriores
- [ ] Status de cada treino (ativo, expirado, pausado)
- [ ] Estatisticas de adesao
- [ ] Duplicar treino existente

---

### US-4.4: Divisao de Treino (ABC)

**Como** um profissional
**Quero** criar divisao de treino em series
**Para** organizar treinos semanais

**Criterios de Aceite:**
- [ ] Criar divisao (A, B, C, D, etc)
- [ ] Associar treino a cada letra
- [ ] Definir rotacao automatica
- [ ] Visualizacao em calendario
- [ ] Aluno ve proximo treino da serie

---

## Modelo de Dados

```typescript
interface WorkoutTemplate {
  id: string;
  businessId: string;
  name: string;
  description?: string;
  type: WorkoutType;
  difficulty: Difficulty;
  estimatedDuration: number; // minutos
  exercises: WorkoutTemplateExercise[];
  createdAt: Date;
  updatedAt: Date;
}

interface WorkoutTemplateExercise {
  id: string;
  exerciseId: string;
  order: number;
  sets: number;
  reps: string; // "10" ou "8-12" ou "AMRAP"
  load?: string; // "20kg" ou "70% 1RM"
  rest: number; // segundos
  notes?: string;
  groupId?: string; // para supersets
  groupType?: 'SUPERSET' | 'CIRCUIT' | 'DROP_SET';
}

interface Workout {
  id: string;
  studentId: string;
  templateId?: string;
  name: string;
  validFrom: Date;
  validUntil?: Date;
  weekDays: number[]; // 0-6
  status: 'ACTIVE' | 'PAUSED' | 'EXPIRED';
  exercises: WorkoutExercise[];
}
```

---

## Requisitos Tecnicos

- Versionamento de treinos (historico de alteracoes)
- Clone profundo de templates
- Validacao de exercicios ao prescrever

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 2: Gestao de Alunos
- Epico 3: Biblioteca de Exercicios

---

## Arquivos Relacionados

```
apps/api/src/modules/workout-templates/
├── workout-templates.controller.ts
├── workout-templates.service.ts
└── workout-templates.routes.ts

apps/api/src/modules/workouts/
├── workouts.controller.ts
├── workouts.service.ts
├── workouts.routes.ts
└── workouts.schema.ts

apps/web/src/app/(dashboard)/treinos/
├── page.tsx              # Lista templates
├── novo/page.tsx         # Criar template
└── [id]/page.tsx         # Editar template

apps/web/src/components/forms/
└── workout-form.tsx      # Formulario de treino
```

---

*Referencia: docs/prd.md - Secao 7*
