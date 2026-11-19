# Epico 6: Agenda e Agendamentos

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

Sistema de agendamento de sessoes, aulas e consultas com confirmacao automatica e lembretes.

---

## User Stories

### US-6.1: Visualizar Agenda (Profissional)

**Como** um profissional
**Quero** ver minha agenda de atendimentos
**Para** organizar meu dia

**Criterios de Aceite:**
- [ ] Visao de dia, semana e mes
- [ ] Agendamentos coloridos por status
- [ ] Horarios disponiveis vs ocupados
- [ ] Arrastar para remarcar
- [ ] Click para ver detalhes
- [ ] Filtro por tipo de servico

---

### US-6.2: Criar Agendamento

**Como** um profissional ou recepcionista
**Quero** criar um novo agendamento
**Para** reservar horario com aluno

**Criterios de Aceite:**
- [ ] Selecionar aluno
- [ ] Selecionar servico
- [ ] Selecionar data e hora
- [ ] Verificar conflitos automaticamente
- [ ] Definir recorrencia (opcional)
- [ ] Adicionar observacoes
- [ ] Enviar confirmacao por WhatsApp

---

### US-6.3: Confirmar/Cancelar Agendamento

**Como** um profissional ou aluno
**Quero** confirmar ou cancelar um agendamento
**Para** gerenciar minha agenda

**Criterios de Aceite:**
- [ ] Botao de confirmar no app/WhatsApp
- [ ] Botao de cancelar com motivo
- [ ] Politica de cancelamento configuravel
- [ ] Notificacao para ambas as partes
- [ ] Liberacao do horario automatica

---

### US-6.4: Lembretes Automaticos

**Como** sistema
**Quero** enviar lembretes de agendamentos
**Para** reduzir no-shows

**Criterios de Aceite:**
- [ ] Lembrete 24h antes (WhatsApp)
- [ ] Lembrete 1h antes (push notification)
- [ ] Link para confirmar/cancelar no lembrete
- [ ] Configuracao de horarios de lembrete

---

### US-6.5: Agendamento pelo Aluno

**Como** um aluno
**Quero** agendar uma sessao pelo app
**Para** ter autonomia

**Criterios de Aceite:**
- [ ] Ver horarios disponiveis do profissional
- [ ] Selecionar data e hora
- [ ] Confirmar agendamento
- [ ] Receber confirmacao
- [ ] Ver meus agendamentos futuros
- [ ] Cancelar com antecedencia minima

---

## Configuracoes de Agenda

```typescript
interface ScheduleSettings {
  // Horario de funcionamento por dia
  businessHours: {
    [day: number]: {
      open: string;  // "08:00"
      close: string; // "22:00"
      breaks?: { start: string; end: string }[];
    };
  };

  // Configuracoes gerais
  defaultDuration: number;        // minutos
  minAdvanceBooking: number;      // horas
  maxAdvanceBooking: number;      // dias
  minCancelAdvance: number;       // horas
  maxDailyBookings?: number;

  // Lembretes
  reminder24h: boolean;
  reminder1h: boolean;
}
```

---

## Status de Agendamento

```typescript
enum AppointmentStatus {
  PENDING = 'PENDING',         // Aguardando confirmacao
  CONFIRMED = 'CONFIRMED',     // Confirmado
  CANCELLED = 'CANCELLED',     // Cancelado
  NO_SHOW = 'NO_SHOW',        // Faltou
  COMPLETED = 'COMPLETED',     // Realizado
  RESCHEDULED = 'RESCHEDULED' // Remarcado
}
```

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 2: Gestao de Alunos
- Epico 7: Integracao WhatsApp (para lembretes)

---

## Arquivos Relacionados

```
apps/api/src/modules/appointments/
├── appointments.controller.ts
├── appointments.service.ts
├── appointments.routes.ts
└── appointments.schema.ts

apps/web/src/app/(dashboard)/agenda/
└── page.tsx

apps/student-app/src/app/(app)/agenda/
└── page.tsx

apps/api/src/jobs/
└── notifications.job.ts   # Lembretes
```

---

*Referencia: docs/prd.md - Secao 9*
