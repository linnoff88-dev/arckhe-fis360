# Epico 5: App do Aluno

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Alta

---

## Descricao

Aplicativo (PWA) para o aluno acessar treinos, registrar execucao, acompanhar evolucao e interagir com o profissional.

---

## User Stories

### US-5.1: Home do Aluno

**Como** um aluno
**Quero** ver minha tela inicial personalizada
**Para** saber o que fazer hoje

**Criterios de Aceite:**
- [ ] Saudacao personalizada
- [ ] Treino do dia destacado
- [ ] Streak atual (dias consecutivos)
- [ ] Proximos agendamentos
- [ ] Pontos e nivel atual
- [ ] Mensagem motivacional
- [ ] Acesso rapido a funcoes principais

---

### US-5.2: Visualizar Treino

**Como** um aluno
**Quero** ver meu treino prescrito
**Para** saber o que executar

**Criterios de Aceite:**
- [ ] Lista de exercicios com ordem
- [ ] Detalhes: series, reps, carga, descanso
- [ ] Acesso ao video de cada exercicio
- [ ] Notas do profissional
- [ ] Botao "Iniciar Treino"
- [ ] Indicador de treino ja realizado hoje

---

### US-5.3: Executar Treino

**Como** um aluno
**Quero** executar meu treino guiado pelo app
**Para** ter suporte durante o treino

**Criterios de Aceite:**
- [ ] Navegacao exercicio por exercicio
- [ ] Video do exercicio em loop
- [ ] Timer de descanso entre series
- [ ] Registrar carga usada por serie
- [ ] Marcar serie como concluida
- [ ] Contador de series restantes
- [ ] Botao "Pular exercicio"
- [ ] Botao "Finalizar treino"
- [ ] Tempo total de treino

---

### US-5.4: Finalizar e Avaliar Treino

**Como** um aluno
**Quero** finalizar e avaliar meu treino
**Para** registrar como foi

**Criterios de Aceite:**
- [ ] Resumo do treino (exercicios, volume total)
- [ ] Avaliacao de dificuldade (1-10 RPE)
- [ ] Avaliacao de humor (emojis)
- [ ] Campo de observacoes
- [ ] Opcao de tirar selfie
- [ ] Pontos ganhos exibidos
- [ ] Animacao de conquista se aplicavel
- [ ] Compartilhar no feed (opcional)

---

### US-5.5: Historico de Treinos

**Como** um aluno
**Quero** ver meu historico de treinos
**Para** acompanhar minha consistencia

**Criterios de Aceite:**
- [ ] Calendario com dias treinados marcados
- [ ] Lista de treinos por mes
- [ ] Detalhes de cada treino realizado
- [ ] Estatisticas: frequencia, volume, PRs
- [ ] Comparacao com metas

---

### US-5.6: Minha Evolucao

**Como** um aluno
**Quero** ver minha evolucao
**Para** me motivar

**Criterios de Aceite:**
- [ ] Grafico de peso ao longo do tempo
- [ ] Grafico de medidas (se houver)
- [ ] Fotos de progresso lado a lado
- [ ] Records pessoais (PRs) por exercicio
- [ ] Badges conquistados
- [ ] Timeline de conquistas

---

## Requisitos Tecnicos

- PWA com service worker para offline
- Sincronizacao quando voltar online
- Push notifications
- Local storage para treino em execucao
- Design responsivo (mobile-first)

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 3: Biblioteca de Exercicios
- Epico 4: Prescricao de Treinos

---

## Arquivos Relacionados

```
apps/student-app/
├── src/
│   ├── app/
│   │   ├── (app)/
│   │   │   ├── layout.tsx
│   │   │   ├── page.tsx              # Home
│   │   │   ├── treino/
│   │   │   │   ├── page.tsx          # Treino do dia
│   │   │   │   └── [id]/page.tsx     # Execucao
│   │   │   ├── historico/page.tsx
│   │   │   ├── evolucao/page.tsx
│   │   │   └── perfil/page.tsx
│   │   └── login/page.tsx
│   ├── components/
│   │   └── workout/
│   │       ├── exercise-card.tsx
│   │       ├── set-input.tsx
│   │       ├── timer.tsx
│   │       └── video-player.tsx
│   ├── hooks/
│   │   ├── use-workout.ts
│   │   └── use-offline.ts
│   └── lib/
│       ├── offline-storage.ts
│       └── sync.ts
└── public/
    └── manifest.json
```

---

*Referencia: docs/prd.md - Secao 8*
