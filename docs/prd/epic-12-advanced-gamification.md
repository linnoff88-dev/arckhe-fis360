# Epico 12: Gamificacao Avancada

**Prioridade:** Should Have
**Fase:** 2
**Complexidade:** Alta

---

## Descricao

Recursos avancados de gamificacao incluindo desafios, rankings e sistema de Guilds.

---

## User Stories

### US-12.1: Desafios

**Como** um gerente
**Quero** criar desafios para os alunos
**Para** aumentar engajamento

**Tipos de desafio:**
| Tipo | Exemplo |
|------|---------|
| Frequencia | 20 treinos em 30 dias |
| Volume | Levantar 10.000kg total |
| Consistencia | 14 dias seguidos |
| Coletivo | Academia queimar 1M calorias |
| Especifico | 100 flexoes em um dia |

**Criterios de Aceite:**
- [ ] Criar desafio com regras e periodo
- [ ] Definir premios
- [ ] Ranking em tempo real
- [ ] Notificacoes de progresso
- [ ] Celebracao dos vencedores

---

### US-12.2: Rankings/Leaderboards

**Como** um aluno
**Quero** ver minha posicao no ranking
**Para** competir com outros

**Criterios de Aceite:**
- [ ] Ranking semanal/mensal
- [ ] Filtro por categoria (idade, objetivo)
- [ ] Top 10 destacado
- [ ] Minha posicao sempre visivel
- [ ] Reset periodico para dar chance a todos

---

### US-12.3: Sistema de Guilds

**Como** um aluno
**Quero** participar de uma Guild
**Para** treinar em grupo

**Criterios de Aceite:**
- [ ] Criar Guild (5-10 membros)
- [ ] Nome, descricao, objetivo
- [ ] Convite por link
- [ ] Meta coletiva semanal
- [ ] Chat da Guild
- [ ] Ranking entre Guilds
- [ ] Recompensas coletivas

---

## Modelo de Dados

```typescript
interface Challenge {
  id: string;
  businessId: string;
  name: string;
  description: string;
  type: ChallengeType;
  criteria: ChallengeCriteria;
  startDate: Date;
  endDate: Date;
  prizes: ChallengePrize[];
  status: 'DRAFT' | 'ACTIVE' | 'COMPLETED';
  isCollective: boolean;
}

interface ChallengeCriteria {
  type: 'WORKOUTS' | 'VOLUME' | 'STREAK' | 'CALORIES' | 'CUSTOM';
  target: number;
  unit: string;
  rules?: Record<string, any>;
}

interface ChallengeParticipant {
  id: string;
  challengeId: string;
  studentId: string;
  progress: number;
  rank?: number;
  completedAt?: Date;
}

interface Guild {
  id: string;
  businessId: string;
  name: string;
  description?: string;
  motto?: string;
  avatarUrl?: string;
  leaderId: string;
  weeklyGoal: number;
  weeklyProgress: number;
  totalPoints: number;
  createdAt: Date;
}

interface GuildMember {
  id: string;
  guildId: string;
  studentId: string;
  role: 'LEADER' | 'CO_LEADER' | 'MEMBER';
  joinedAt: Date;
  weeklyContribution: number;
}

interface Leaderboard {
  id: string;
  businessId: string;
  type: 'POINTS' | 'WORKOUTS' | 'STREAK' | 'GUILD';
  period: 'WEEKLY' | 'MONTHLY' | 'ALL_TIME';
  entries: LeaderboardEntry[];
  lastUpdated: Date;
}
```

---

## Regras de Guilds

1. **Criacao**:
   - Minimo 3 membros para criar
   - Maximo 10 membros por Guild
   - Aluno pode participar de apenas 1 Guild

2. **Metas**:
   - Meta semanal definida pelo lider
   - Progresso e soma dos pontos dos membros
   - Bonus se atingir meta: +500pts para cada membro

3. **Ranking de Guilds**:
   - Pontos totais da semana
   - Top 3 Guilds recebem destaque
   - Reset semanal (segundas)

4. **Chat**:
   - Mensagens de texto
   - Reacoes
   - Anuncios do lider

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 8: Gamificacao Basica

---

## Arquivos Relacionados

```
apps/api/src/modules/challenges/
├── challenges.controller.ts
├── challenges.service.ts
└── challenges.routes.ts

apps/api/src/modules/guilds/
├── guilds.controller.ts
├── guilds.service.ts
└── guilds.routes.ts

apps/api/src/modules/gamification/
└── leaderboard.service.ts

apps/student-app/src/app/(app)/desafios/
└── page.tsx

apps/student-app/src/app/(app)/guild/
├── page.tsx
├── criar/page.tsx
└── [id]/page.tsx
```

---

*Referencia: docs/prd.md - Secao 15*
