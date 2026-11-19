# Project Brief: FIS360

## Plataforma Inteligente de Gestao Fitness

**Versao:** 1.0
**Data:** 06/01/2026
**Status:** Aprovado

---

## 1. Visao Geral

### 1.1 Declaracao do Projeto

O FIS360 e uma plataforma SaaS completa para gestao de negocios fitness que unifica academias, personal trainers e fisioterapeutas em um unico ecossistema inteligente. Diferente das solucoes existentes que focam em apenas um segmento, o FIS360 oferece uma abordagem integrada com IA preditiva, gamificacao avancada e integracao nativa com wearables.

### 1.2 Problema a Resolver

**Para Academias:**
- Churn alto (6-8% ao mes) sem ferramentas efetivas de retencao
- Sistemas desatualizados e fragmentados
- Dificuldade em medir engajamento real dos alunos
- Falta de diferenciacao competitiva

**Para Personal Trainers:**
- Limite de escala (maximo de horas disponiveis)
- Ferramentas amadoras (WhatsApp, planilhas, PDFs)
- Dificuldade em fidelizar clientes
- Sem capacidade de oferecer servico hibrido

**Para Fisioterapeutas:**
- Prontuarios em papel ou sistemas genericos
- Falta de acompanhamento entre sessoes
- Dificuldade em medir evolucao do paciente
- Laudos e relatorios manuais

**Para Alunos/Pacientes:**
- Apps de treino genericos sem personalizacao real
- Falta de visibilidade do progresso
- Desmotivacao por falta de engajamento
- Experiencia fragmentada entre profissionais

### 1.3 Solucao Proposta

Uma plataforma AI-First que:

1. **Unifica** a gestao de academias, personal trainers e fisioterapeutas
2. **Prediz** risco de churn e sugere acoes automaticas
3. **Engaja** atraves de gamificacao social avancada (Guilds)
4. **Integra** dados de wearables para personalizacao real
5. **Escala** profissionais atraves de modelo hibrido e marketplace

---

## 2. Objetivos de Negocio

### 2.1 Objetivos Primarios

| Objetivo | Meta Ano 1 | Meta Ano 3 | Meta Ano 5 |
|----------|------------|------------|------------|
| Clientes ativos | 300 | 2.000 | 5.000 |
| MRR | R$ 84k | R$ 840k | R$ 2.5M |
| ARR | R$ 1M | R$ 10M | R$ 30M |
| Churn de clientes | < 4% | < 2.5% | < 2% |
| NPS | > 40 | > 55 | > 65 |

### 2.2 Objetivos Secundarios

- Reducao media de churn nas academias clientes: 40%
- Aumento de frequencia dos alunos: 25%
- Marketplace GMV Ano 5: R$ 10M
- Expansao LATAM iniciada ate Ano 4

### 2.3 Metricas de Sucesso (KPIs)

**Produto:**
- DAU/MAU App do Aluno > 35%
- Tempo medio no app > 5 min/sessao
- Taxa de completude de treino > 70%
- Engajamento gamificacao > 60% dos alunos

**Negocio:**
- LTV/CAC > 5x
- Payback < 5 meses
- Net Revenue Retention > 110%
- Gross Margin > 75%

---

## 3. Publico-Alvo

### 3.1 Segmentos Primarios

#### Segmento 1: Personal Trainers em Crescimento
```
PERFIL:
- 25-40 anos
- CREF ativo
- 15-50 alunos ativos
- Faturamento R$ 8-25k/mes
- Quer escalar sem trabalhar mais horas

NECESSIDADES:
- App profissional para alunos
- Prescricao digital de treinos
- Automacao de cobranca e lembretes
- Capacidade de atender online
```

#### Segmento 2: Studios Boutique (CrossFit, Funcional, Pilates)
```
PERFIL:
- 100-400 membros
- Faturamento R$ 40-150k/mes
- Comunidade forte
- Foco em experiencia premium

NECESSIDADES:
- WODs e rankings
- Reserva de aulas
- Comunidade no app
- Gamificacao e desafios
```

#### Segmento 3: Academias de Bairro
```
PERFIL:
- 200-800 alunos
- Faturamento R$ 50-200k/mes
- 5-20 funcionarios
- Problema cronico de churn

NECESSIDADES:
- Controle de acesso (catraca)
- Gestao financeira
- App do aluno diferenciado
- Retencao inteligente
```

#### Segmento 4: Clinicas de Fisioterapia
```
PERFIL:
- 2-10 fisioterapeutas
- 100-500 pacientes ativos
- Mix particular + convenio
- Foco em ortopedia/esportiva

NECESSIDADES:
- Prontuario digital completo
- Protocolos de tratamento
- Exercicios para casa
- Laudos automaticos
```

### 3.2 Segmentos Secundarios (Futuro)

- Redes de academias (multi-unidade)
- Wellness corporativo (B2B2C)
- Profissionais de nutricao (integracao)

---

## 4. Escopo do Projeto

### 4.1 Fase 1 - MVP (Q1-Q2 2026)

**Foco:** Personal Trainers

**Inclui:**
- [ ] Autenticacao e multi-tenancy
- [ ] Cadastro de alunos
- [ ] Biblioteca de exercicios com videos
- [ ] Prescricao de treinos
- [ ] App do aluno (PWA)
- [ ] Execucao de treino no app
- [ ] Agenda e agendamentos
- [ ] Integracao WhatsApp (Evolution API)
- [ ] Notificacoes automaticas
- [ ] Gamificacao basica (pontos, streaks)
- [ ] Dashboard de metricas

**Nao Inclui (Fase 1):**
- Integracao com catracas
- Modulo financeiro completo
- Prontuario de fisioterapia
- Marketplace
- Multi-unidades

### 4.2 Fase 2 - Studios (Q3-Q4 2026)

**Adiciona:**
- [ ] Aulas coletivas e reservas
- [ ] WODs e benchmark workouts
- [ ] Rankings e leaderboards
- [ ] Desafios e competicoes
- [ ] Comunidade/Feed social
- [ ] Sistema de Guilds
- [ ] Check-in por QR Code
- [ ] Avaliacoes fisicas completas
- [ ] Fotos de progresso
- [ ] Graficos de evolucao

### 4.3 Fase 3 - Academias (2027 H1)

**Adiciona:**
- [ ] Integracao com catracas
- [ ] Gestao financeira completa
- [ ] Planos e assinaturas
- [ ] Controle de inadimplencia
- [ ] Multi-profissional
- [ ] Comissoes
- [ ] Relatorios avancados
- [ ] Sistema de churn prediction

### 4.4 Fase 4 - Fisioterapia (2027 H2)

**Adiciona:**
- [ ] Prontuario digital (anamnese, evolucao)
- [ ] CID-10 integrado
- [ ] Protocolos de tratamento
- [ ] Sessoes de fisioterapia
- [ ] Laudos e relatorios automaticos
- [ ] Exercicios para casa

### 4.5 Fase 5 - Ecossistema (2028)

**Adiciona:**
- [ ] Marketplace de programas
- [ ] API publica
- [ ] White-label
- [ ] Integracao wearables avancada
- [ ] IA para geracao de treinos
- [ ] Multi-unidades

---

## 5. Premissas e Restricoes

### 5.1 Premissas

1. O mercado fitness brasileiro continuara crescendo (+10%/ano minimo)
2. Personal trainers e studios sao early adopters de tecnologia
3. Integracao WhatsApp e essencial (canal dominante no Brasil)
4. Modelo hibrido (presencial + online) e o novo padrao
5. Gamificacao aumenta retencao significativamente

### 5.2 Restricoes

1. **Tecnicas:**
   - Stack: Next.js, Express, PostgreSQL, Redis (definido)
   - Hospedagem inicial em VPS/Docker (custo controlado)
   - Evolution API para WhatsApp (dependencia externa)

2. **Negocio:**
   - Bootstrap inicial (sem investimento externo)
   - Time enxuto (1-3 desenvolvedores)
   - Lancamento MVP em 3 meses

3. **Regulatorias:**
   - LGPD compliance obrigatorio
   - Dados de saude requerem cuidado especial
   - CREF/COFITO para validacao profissional

### 5.3 Dependencias

- Evolution API v2 para integracao WhatsApp
- Biblioteca de exercicios (criar ou licenciar)
- Gateway de pagamento (Stripe ou PagSeguro)
- Servico de video hosting (Bunny ou Vimeo)

---

## 6. Riscos Identificados

| Risco | Probabilidade | Impacto | Mitigacao |
|-------|---------------|---------|-----------|
| Concorrentes reagirem | Alta | Medio | Features unicas, nicho inicial |
| Resistencia a adocao | Media | Alto | Trial longo, onboarding assistido |
| Integracao catraca complexa | Media | Alto | Fase 3, parcerias com fabricantes |
| Evolution API instavel | Media | Medio | Fallback para outras APIs |
| Churn proprio alto | Media | Alto | Demonstrar ROI claro |

---

## 7. Stakeholders

### 7.1 Time Core

| Papel | Responsabilidade |
|-------|------------------|
| Product Owner | Visao do produto, priorizacao |
| Tech Lead | Arquitetura, decisoes tecnicas |
| Full-Stack Dev | Desenvolvimento |
| UX Designer | Interface e experiencia |

### 7.2 Stakeholders Externos

- Personal trainers beta testers
- Academias parceiras para piloto
- Fornecedores de catracas
- Parceiros de conteudo (videos)

---

## 8. Cronograma Macro

```
2026 Q1 (Jan-Mar): MVP Development
├── Semanas 1-4: Setup + Auth + Alunos
├── Semanas 5-8: Exercicios + Treinos
└── Semanas 9-12: App Aluno + WhatsApp

2026 Q2 (Abr-Jun): MVP Launch + Iteration
├── Lancamento beta fechado
├── 50 personal trainers
└── Iteracao baseada em feedback

2026 Q3-Q4: Studios + Scale
├── Features de aulas coletivas
├── Gamificacao avancada
├── 300 clientes

2027: Academias + Fisio
├── Integracao catracas
├── Modulo financeiro
├── Prontuario fisio
├── 2.000 clientes

2028: Ecossistema
├── Marketplace
├── API publica
├── Expansao LATAM
```

---

## 9. Aprovacoes

| Papel | Nome | Data | Status |
|-------|------|------|--------|
| Product Owner | - | 06/01/2026 | Aprovado |
| Tech Lead | - | 06/01/2026 | Aprovado |
| Stakeholder | - | 06/01/2026 | Aprovado |

---

## 10. Referencias

- Analise Estrategica: `/doc/analise-estrategica-fitness.md`
- Prompt Sistema: `/doc/prompt-sistema-fitness.md`
- Pesquisa de Mercado 2026: Dados atualizados via web research

---

*Documento gerado em 06/01/2026*
*Metodologia: BMad Framework*
