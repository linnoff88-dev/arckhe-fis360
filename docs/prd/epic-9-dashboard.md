# Epico 9: Dashboard e Metricas

**Prioridade:** Should Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

Dashboard para profissionais acompanharem metricas do negocio e dos alunos.

---

## User Stories

### US-9.1: Dashboard Principal

**Como** um profissional
**Quero** ver metricas do meu negocio
**Para** tomar decisoes

**Metricas principais:**
- [ ] Total de alunos ativos
- [ ] Novos alunos no mes
- [ ] Alunos em risco de churn
- [ ] Treinos realizados na semana
- [ ] Agendamentos de hoje
- [ ] Taxa de frequencia media
- [ ] Receita do mes (se modulo financeiro)

**Criterios de Aceite:**
- [ ] Graficos interativos
- [ ] Comparacao com periodo anterior
- [ ] Filtro por periodo
- [ ] Export para PDF/Excel

---

### US-9.2: Alertas de Churn

**Como** um profissional
**Quero** ser alertado sobre alunos em risco
**Para** agir proativamente

**Criterios de risco:**
| Indicador | Peso |
|-----------|------|
| Nao treinou ha 7+ dias | Alto |
| Frequencia caiu 50%+ | Alto |
| Nao abre app ha 5+ dias | Medio |
| Cancelou agendamentos recentes | Medio |
| Pagamento atrasado | Alto |

**Niveis de Risco:**
- **Verde**: Aluno ativo e engajado
- **Amarelo**: Queda de atividade (acao preventiva)
- **Laranja**: Risco moderado (contato necessario)
- **Vermelho**: Risco alto (acao urgente)

**Criterios de Aceite:**
- [ ] Lista de alunos em risco
- [ ] Nivel de risco (amarelo, laranja, vermelho)
- [ ] Sugestao de acao
- [ ] Botao para contatar
- [ ] Marcar como "tratado"

---

### US-9.3: Relatorio de Aluno

**Como** um profissional
**Quero** gerar relatorio de um aluno
**Para** mostrar evolucao

**Criterios de Aceite:**
- [ ] Selecionar periodo
- [ ] Incluir: frequencia, treinos, evolucao
- [ ] Graficos de progresso
- [ ] Comparativo de avaliacoes
- [ ] Export para PDF
- [ ] Enviar por WhatsApp/email

---

## Cards do Dashboard

```typescript
interface DashboardCard {
  title: string;
  value: number | string;
  change?: number;       // % de mudanca
  changeType?: 'positive' | 'negative' | 'neutral';
  icon: string;
  link?: string;
}

// Exemplo de cards
const dashboardCards = [
  {
    title: 'Alunos Ativos',
    value: 127,
    change: 8,
    changeType: 'positive',
    icon: 'users',
    link: '/alunos'
  },
  {
    title: 'Em Risco',
    value: 12,
    change: -3,
    changeType: 'positive',
    icon: 'alert-triangle',
    link: '/alunos?filter=risco'
  },
  {
    title: 'Treinos Semana',
    value: 342,
    change: 15,
    changeType: 'positive',
    icon: 'activity'
  },
  {
    title: 'Agendamentos Hoje',
    value: 18,
    icon: 'calendar',
    link: '/agenda'
  }
];
```

---

## Graficos

1. **Frequencia Semanal**: Treinos por dia da semana (bar chart)
2. **Evolucao de Alunos**: Novos vs cancelados por mes (line chart)
3. **Taxa de Retencao**: % de alunos ativos ao longo do tempo
4. **Horarios Populares**: Heat map de agendamentos por horario
5. **Distribuicao por Objetivo**: Pie chart de objetivos dos alunos

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 2: Gestao de Alunos

---

## Arquivos Relacionados

```
apps/api/src/modules/reports/
├── reports.controller.ts
├── reports.service.ts
└── reports.routes.ts

apps/api/src/jobs/
└── churn.job.ts

apps/web/src/app/(dashboard)/
├── page.tsx                  # Dashboard principal

apps/web/src/app/(dashboard)/relatorios/
└── page.tsx

apps/web/src/components/charts/
├── attendance-chart.tsx
└── stats-chart.tsx
```

---

*Referencia: docs/prd.md - Secao 12*
