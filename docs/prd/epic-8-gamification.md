# Epico 8: Gamificacao Basica

**Prioridade:** Should Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

Sistema de pontos, streaks e badges para motivar alunos e aumentar engajamento.

---

## User Stories

### US-8.1: Sistema de Pontos

**Como** um aluno
**Quero** ganhar pontos por minhas atividades
**Para** me sentir recompensado

**Eventos que geram pontos:**
| Evento | Pontos |
|--------|--------|
| Check-in na academia | 10 pts |
| Treino completado | 50 pts |
| Treino com avaliacao | +10 pts |
| PR batido | 100 pts |
| Meta semanal atingida | 200 pts |
| Indicacao de amigo | 500 pts |

**Criterios de Aceite:**
- [ ] Exibir pontos totais no perfil
- [ ] Historico de pontos ganhos
- [ ] Animacao ao ganhar pontos
- [ ] Nivel baseado em pontos

---

### US-8.2: Sistema de Streaks

**Como** um aluno
**Quero** manter minha sequencia de treinos
**Para** criar habito

**Criterios de Aceite:**
- [ ] Contador de dias consecutivos
- [ ] Definicao de "dia treinado" (1+ treino)
- [ ] Tolerancia de 1 dia (configuravel)
- [ ] Alerta de streak em risco
- [ ] Record de maior streak
- [ ] Bonus de pontos por streak (multiplicador)

**Multiplicadores de Streak:**
| Streak | Multiplicador |
|--------|---------------|
| 7 dias | 1.5x |
| 14 dias | 2x |
| 30 dias | 2.5x |
| 60 dias | 3x |
| 90+ dias | 4x |

---

### US-8.3: Badges e Conquistas

**Como** um aluno
**Quero** desbloquear badges
**Para** colecionar conquistas

**Badges iniciais:**
| Badge | Criterio |
|-------|----------|
| "Primeira Semana" | 7 dias seguidos |
| "Madrugador" | 10 treinos antes das 7h |
| "Noturno" | 10 treinos apos 21h |
| "Consistente" | 30 dias sem faltar |
| "Centenario" | 100 treinos |
| "PR Hunter" | 10 PRs em 1 mes |
| "Social" | 10 interacoes no feed |
| "Iniciante" | Primeiro treino |
| "Dedicado" | 50 treinos |
| "Maratonista" | 365 treinos |

**Criterios de Aceite:**
- [ ] Notificacao ao desbloquear
- [ ] Animacao especial
- [ ] Exibir no perfil
- [ ] Compartilhar conquista

---

### US-8.4: Niveis

**Como** um aluno
**Quero** subir de nivel
**Para** mostrar minha dedicacao

**Niveis:**
| Nivel | Nome | Pontos |
|-------|------|--------|
| 1 | Iniciante | 0 - 1.000 |
| 2 | Regular | 1.000 - 5.000 |
| 3 | Dedicado | 5.000 - 15.000 |
| 4 | Atleta | 15.000 - 50.000 |
| 5 | Elite | 50.000+ |

**Criterios de Aceite:**
- [ ] Exibir nivel no perfil
- [ ] Barra de progresso para proximo nivel
- [ ] Celebracao ao subir de nivel
- [ ] Beneficios por nivel (futuro)

---

## Modelo de Dados

```typescript
interface StudentGamification {
  studentId: string;
  totalPoints: number;
  level: number;
  currentStreak: number;
  longestStreak: number;
  lastWorkoutAt: Date;
  badges: StudentBadge[];
}

interface StudentBadge {
  id: string;
  studentId: string;
  badgeId: string;
  unlockedAt: Date;
  shared: boolean;
}

interface Badge {
  id: string;
  name: string;
  description: string;
  icon: string;
  category: 'CONSISTENCY' | 'PERFORMANCE' | 'SOCIAL' | 'MILESTONE';
  criteria: BadgeCriteria;
  points: number;
}
```

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 5: App do Aluno

---

## Arquivos Relacionados

```
apps/api/src/modules/gamification/
├── gamification.controller.ts
├── gamification.service.ts
├── gamification.routes.ts
├── badges.service.ts
└── leaderboard.service.ts

apps/student-app/src/app/(app)/conquistas/
└── page.tsx

apps/student-app/src/components/gamification/
├── streak-badge.tsx
├── points-display.tsx
└── badge-card.tsx
```

---

*Referencia: docs/prd.md - Secao 11*
