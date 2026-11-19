# Epico 7: Integracao WhatsApp

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Media

---

## Descricao

Integracao com WhatsApp via Evolution API para comunicacao automatizada e manual com alunos.

---

## User Stories

### US-7.1: Conectar WhatsApp

**Como** um dono de negocio
**Quero** conectar meu WhatsApp ao sistema
**Para** automatizar comunicacao

**Criterios de Aceite:**
- [ ] Gerar QR Code para conexao
- [ ] Exibir status de conexao
- [ ] Reconectar automaticamente se desconectar
- [ ] Notificar se desconectado por muito tempo
- [ ] Opcao de desconectar

---

### US-7.2: Enviar Mensagem Manual

**Como** um profissional
**Quero** enviar mensagem para um aluno
**Para** comunicar algo especifico

**Criterios de Aceite:**
- [ ] Botao de WhatsApp no perfil do aluno
- [ ] Abrir conversa no WhatsApp Web ou app
- [ ] Alternativa: enviar pelo sistema
- [ ] Historico de mensagens enviadas

---

### US-7.3: Mensagens Automaticas

**Como** sistema
**Quero** enviar mensagens automaticas
**Para** engajar alunos

**Tipos de mensagem:**
- [ ] Confirmacao de agendamento
- [ ] Lembrete de agendamento
- [ ] Novo treino prescrito
- [ ] Parabens por conquista
- [ ] Lembrete de inatividade
- [ ] Feliz aniversario
- [ ] Cobranca de pagamento

**Criterios de Aceite:**
- [ ] Templates configuraveis
- [ ] Variaveis dinamicas (nome, data, etc)
- [ ] Fila de envio para evitar spam
- [ ] Log de mensagens enviadas
- [ ] Metricas de entrega

---

### US-7.4: Chatbot Basico

**Como** sistema
**Quero** responder mensagens simples automaticamente
**Para** agilizar atendimento

**Criterios de Aceite:**
- [ ] Respostas para perguntas frequentes
- [ ] Confirmacao de agendamento por resposta
- [ ] Encaminhar para humano quando necessario
- [ ] Horario de funcionamento automatico

---

## Templates de Mensagem

```typescript
// templates/whatsapp.ts
export const templates = {
  appointmentConfirmation: (data: any) => `
Ola ${data.studentName}!

Seu agendamento foi confirmado:
- Servico: ${data.service}
- Data: ${data.date}
- Horario: ${data.time}
- Profissional: ${data.professional}

Para cancelar ou remarcar, responda esta mensagem.

Ate la!
`,

  workoutReminder: (data: any) => `
Bom dia ${data.studentName}!

Hoje e dia de treino! Seu treino de ${data.workoutType} esta te esperando.

Sua sequencia atual: ${data.streak} dias!

Bora treinar?
`,

  achievementUnlocked: (data: any) => `
PARABENS ${data.studentName}!

Voce desbloqueou uma nova conquista:
*${data.badgeName}*

${data.badgeDescription}

Continue assim!
`,

  inactivityAlert: (data: any) => `
Ola ${data.studentName}!

Sentimos sua falta! Faz ${data.daysSince} dias que voce nao treina.

Que tal voltar hoje? Seu treino esta te esperando!
`,

  birthdayWish: (data: any) => `
FELIZ ANIVERSARIO ${data.studentName}!

A equipe ${data.businessName} deseja um dia incrivel!

Passe aqui para um treino especial de aniversario!
`,
};
```

---

## Requisitos Tecnicos

- Evolution API v2 self-hosted
- Webhook para receber mensagens
- Fila Redis para envio (rate limiting)
- Retry com backoff exponencial
- Fallback para SMS se WhatsApp falhar

---

## Limites e Rate Limiting

```
LIMITES:
- 30 mensagens por minuto por instancia
- Intervalo minimo de 2 segundos entre mensagens
- Maximo de 5 retries por mensagem
- Backoff exponencial: 5s, 15s, 60s, 300s, 900s
```

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy

---

## Arquivos Relacionados

```
apps/api/src/modules/whatsapp/
├── whatsapp.controller.ts
├── whatsapp.service.ts
├── whatsapp.routes.ts
└── templates.ts

apps/api/src/jobs/
└── whatsapp.job.ts

apps/api/src/queues/
└── index.ts    # whatsappQueue

apps/web/src/app/(dashboard)/configuracoes/whatsapp/
└── page.tsx

docker-compose.yml   # evolution-api service
```

---

*Referencia: docs/prd.md - Secao 10*
