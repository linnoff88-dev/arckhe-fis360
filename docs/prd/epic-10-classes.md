# Epico 10: Aulas Coletivas

**Prioridade:** Must Have
**Fase:** 2
**Complexidade:** Media

---

## Descricao

Sistema para gerenciar aulas em grupo com reserva de vagas, check-in e waitlist.

---

## User Stories

### US-10.1: Criar Grade de Aulas

**Como** um gerente
**Quero** criar a grade semanal de aulas
**Para** organizar a programacao

**Criterios de Aceite:**
- [ ] Criar aula com: nome, instrutor, sala, horario
- [ ] Definir capacidade maxima
- [ ] Definir dias da semana de recorrencia
- [ ] Cor para identificacao visual
- [ ] Ativar/desativar aula

---

### US-10.2: Reservar Vaga em Aula

**Como** um aluno
**Quero** reservar vaga em uma aula
**Para** garantir minha participacao

**Criterios de Aceite:**
- [ ] Ver aulas disponiveis
- [ ] Ver vagas restantes
- [ ] Reservar com 1 click
- [ ] Entrar em waitlist se lotado
- [ ] Cancelar reserva
- [ ] Notificacao se sair da waitlist

---

### US-10.3: Check-in em Aula

**Como** um instrutor ou recepcionista
**Quero** fazer check-in dos alunos
**Para** controlar presenca

**Criterios de Aceite:**
- [ ] Lista de alunos com reserva
- [ ] Marcar presenca
- [ ] Marcar no-show
- [ ] Adicionar aluno sem reserva (se houver vaga)
- [ ] Check-in por QR Code (aluno)

---

## Modelo de Dados

```typescript
interface GroupClass {
  id: string;
  businessId: string;
  name: string;
  description?: string;
  instructorId: string;
  room?: string;
  capacity: number;
  duration: number;        // minutos
  color: string;
  isActive: boolean;
}

interface ClassSchedule {
  id: string;
  classId: string;
  weekDay: number;         // 0-6
  startTime: string;       // "07:00"
  validFrom: Date;
  validUntil?: Date;
}

interface ClassSession {
  id: string;
  scheduleId: string;
  date: Date;
  status: 'SCHEDULED' | 'COMPLETED' | 'CANCELLED';
  bookings: ClassBooking[];
}

interface ClassBooking {
  id: string;
  sessionId: string;
  studentId: string;
  status: 'BOOKED' | 'WAITLIST' | 'CHECKED_IN' | 'NO_SHOW' | 'CANCELLED';
  waitlistPosition?: number;
  bookedAt: Date;
  checkedInAt?: Date;
}
```

---

## Regras de Negocio

1. **Reserva**:
   - Aluno pode reservar com ate X horas de antecedencia
   - Aluno pode ter maximo de Y reservas ativas
   - Cancelamento com menos de Z horas conta como no-show

2. **Waitlist**:
   - Quando vaga liberar, notificar primeiro da lista
   - Tempo limite para confirmar (ex: 2 horas)
   - Se nao confirmar, passa para proximo

3. **No-show**:
   - 3 no-shows bloqueiam reservas por 7 dias
   - Contador reseta apos periodo

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 2: Gestao de Alunos
- Epico 6: Agenda e Agendamentos

---

## Arquivos Relacionados

```
apps/api/src/modules/classes/
├── classes.controller.ts
├── classes.service.ts
├── classes.routes.ts
├── bookings.service.ts
└── waitlist.service.ts

apps/web/src/app/(dashboard)/aulas/
├── page.tsx              # Grade de aulas
├── nova/page.tsx         # Criar aula
└── [id]/page.tsx         # Detalhes/checkin

apps/student-app/src/app/(app)/aulas/
└── page.tsx              # Reservar aula
```

---

*Referencia: docs/prd.md - Secao 13*
