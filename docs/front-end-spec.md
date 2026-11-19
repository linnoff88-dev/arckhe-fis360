# Front-End Specification

## FIS360 - Plataforma Inteligente de Gestao Fitness

**Versao:** 1.0
**Data:** 06/01/2026
**Status:** Aprovado

---

## 1. Visao Geral

### 1.1 Aplicacoes

O FIS360 possui duas aplicacoes front-end distintas:

1. **Dashboard Web** - Para profissionais (Next.js)
2. **App do Aluno** - Para alunos (PWA/React Native)

### 1.2 Principios de Design

1. **Mobile-First**: Todas as interfaces projetadas para mobile primeiro
2. **Simplicidade**: UI limpa, sem distracao
3. **Feedback Visual**: Cada acao tem feedback imediato
4. **Acessibilidade**: WCAG 2.1 AA compliance
5. **Performance**: Core Web Vitals otimizados

---

## 2. Design System

### 2.1 Cores

```css
/* Cores Primarias */
--primary-50: #ECFDF5;
--primary-100: #D1FAE5;
--primary-200: #A7F3D0;
--primary-300: #6EE7B7;
--primary-400: #34D399;
--primary-500: #10B981;  /* Principal */
--primary-600: #059669;
--primary-700: #047857;
--primary-800: #065F46;
--primary-900: #064E3B;

/* Cores Secundarias */
--secondary-500: #6366F1;  /* Indigo - Gamificacao */
--accent-500: #F59E0B;     /* Amber - Alertas/Destaque */

/* Cores Semanticas */
--success: #22C55E;
--warning: #F59E0B;
--error: #EF4444;
--info: #3B82F6;

/* Neutros */
--gray-50: #F9FAFB;
--gray-100: #F3F4F6;
--gray-200: #E5E7EB;
--gray-300: #D1D5DB;
--gray-400: #9CA3AF;
--gray-500: #6B7280;
--gray-600: #4B5563;
--gray-700: #374151;
--gray-800: #1F2937;
--gray-900: #111827;

/* Tema Escuro */
--dark-bg: #0F172A;
--dark-surface: #1E293B;
--dark-border: #334155;
```

### 2.2 Tipografia

```css
/* Font Family */
--font-sans: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
--font-mono: 'JetBrains Mono', monospace;

/* Font Sizes */
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
--text-4xl: 2.25rem;   /* 36px */

/* Font Weights */
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;

/* Line Heights */
--leading-tight: 1.25;
--leading-normal: 1.5;
--leading-relaxed: 1.75;
```

### 2.3 Espacamento

```css
/* Escala de espacamento (base 4px) */
--space-0: 0;
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
```

### 2.4 Border Radius

```css
--radius-sm: 0.25rem;   /* 4px */
--radius-md: 0.375rem;  /* 6px */
--radius-lg: 0.5rem;    /* 8px */
--radius-xl: 0.75rem;   /* 12px */
--radius-2xl: 1rem;     /* 16px */
--radius-full: 9999px;
```

### 2.5 Sombras

```css
--shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
--shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
--shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
--shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
```

---

## 3. Componentes Base

### 3.1 Botoes

```
VARIANTES:
├── Primary (verde, acoes principais)
├── Secondary (outline, acoes secundarias)
├── Destructive (vermelho, acoes perigosas)
├── Ghost (transparente, acoes sutis)
└── Link (texto, navegacao)

TAMANHOS:
├── sm: h-8 px-3 text-sm
├── md: h-10 px-4 text-base (padrao)
├── lg: h-12 px-6 text-lg
└── icon: h-10 w-10 (apenas icone)

ESTADOS:
├── Default
├── Hover (escurece 10%)
├── Active (escurece 20%)
├── Disabled (opacity 50%, cursor not-allowed)
└── Loading (spinner, disabled)
```

### 3.2 Inputs

```
TIPOS:
├── Text
├── Email
├── Password (com toggle de visibilidade)
├── Number
├── Phone (mascara automatica)
├── Date
├── Time
├── Textarea
└── Select

ESTADOS:
├── Default (border gray-300)
├── Focus (ring primary-500)
├── Error (border red-500, mensagem abaixo)
├── Disabled (bg gray-100, cursor not-allowed)
└── With Icon (icone a esquerda ou direita)

ESTRUTURA:
├── Label (acima)
├── Input
├── Helper text (abaixo, cinza)
└── Error message (abaixo, vermelho)
```

### 3.3 Cards

```
VARIANTES:
├── Default (bg white, shadow-sm, rounded-lg)
├── Elevated (shadow-md)
├── Outlined (border, no shadow)
└── Interactive (hover:shadow-md, cursor pointer)

PARTES:
├── Card Header (titulo, acoes)
├── Card Content (conteudo principal)
└── Card Footer (acoes, informacoes)
```

### 3.4 Modais

```
TAMANHOS:
├── sm: max-w-sm (alertas)
├── md: max-w-md (formularios simples)
├── lg: max-w-lg (formularios complexos)
├── xl: max-w-xl (conteudo extenso)
└── full: max-w-4xl (tabelas, listas)

ESTRUTURA:
├── Overlay (bg black/50, click to close)
├── Modal Container (centered, animated)
├── Modal Header (titulo, botao fechar)
├── Modal Content (scroll se necessario)
└── Modal Footer (acoes)

ANIMACAO:
├── Entrada: fade in + scale up (150ms)
└── Saida: fade out + scale down (100ms)
```

### 3.5 Tabelas

```
FEATURES:
├── Header fixo
├── Ordenacao por coluna
├── Paginacao
├── Selecao de linhas
├── Acoes por linha
├── Responsivo (horizontal scroll em mobile)
└── Estados vazios

DENSIDADE:
├── Compact: py-2
├── Default: py-3
└── Comfortable: py-4
```

### 3.6 Navegacao

```
SIDEBAR (Desktop):
├── Logo
├── Menu items com icones
├── Submenus colapsaveis
├── Indicador de item ativo
├── User info no footer
└── Colapsavel para icones only

BOTTOM NAV (Mobile App):
├── 4-5 items maximos
├── Icone + label
├── Indicador de item ativo
├── Badge para notificacoes
```

---

## 4. Dashboard Web - Telas

### 4.1 Autenticacao

#### Tela: Login
```
LAYOUT:
┌─────────────────────────────────────────┐
│                                         │
│              [LOGO FIS360]              │
│                                         │
│         ┌─────────────────────┐         │
│         │      Email          │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │      Senha          │         │
│         └─────────────────────┘         │
│                                         │
│         [  ] Lembrar de mim             │
│                                         │
│         ┌─────────────────────┐         │
│         │      ENTRAR         │         │
│         └─────────────────────┘         │
│                                         │
│         Esqueci minha senha             │
│                                         │
│         ─────── ou ───────              │
│                                         │
│         Criar nova conta                │
│                                         │
└─────────────────────────────────────────┘

COMPORTAMENTOS:
- Validacao em tempo real
- Mostrar/ocultar senha
- Loading state no botao
- Redirect apos login
```

#### Tela: Registro
```
LAYOUT:
┌─────────────────────────────────────────┐
│              [LOGO FIS360]              │
│                                         │
│       Crie sua conta gratuita           │
│                                         │
│         ┌─────────────────────┐         │
│         │   Nome do negocio   │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │   Seu nome          │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │   Email             │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │   Telefone          │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │   Tipo de negocio ▼ │         │
│         └─────────────────────┘         │
│         ┌─────────────────────┐         │
│         │   Senha             │         │
│         └─────────────────────┘         │
│                                         │
│         ┌─────────────────────┐         │
│         │   CRIAR CONTA       │         │
│         └─────────────────────┘         │
│                                         │
│         Ja tem conta? Entrar            │
│                                         │
└─────────────────────────────────────────┘
```

### 4.2 Dashboard Principal

```
LAYOUT:
┌──────────────────────────────────────────────────────────────┐
│ [≡] FIS360                                    [🔔] [Avatar] │
├────────────┬─────────────────────────────────────────────────┤
│            │                                                 │
│  Dashboard │   Bom dia, Rafaela!                            │
│  ─────────│                                                 │
│  Alunos    │   ┌──────────┐ ┌──────────┐ ┌──────────┐      │
│  Treinos   │   │ 25       │ │ 142      │ │ 3        │      │
│  Exercicios│   │ Alunos   │ │ Treinos  │ │ Alertas  │      │
│  Agenda    │   │ ativos   │ │ semana   │ │ churn    │      │
│  WhatsApp  │   └──────────┘ └──────────┘ └──────────┘      │
│            │                                                 │
│  ─────────│   Alunos em risco                              │
│  Relatorios│   ┌─────────────────────────────────────┐      │
│  Config    │   │ 🟡 Maria Silva - 7 dias sem treinar │      │
│            │   │ 🟠 Joao Santos - 14 dias inativo    │      │
│            │   │ 🔴 Pedro Lima - pagto atrasado      │      │
│            │   └─────────────────────────────────────┘      │
│            │                                                 │
│            │   Agenda de hoje                               │
│            │   ┌─────────────────────────────────────┐      │
│            │   │ 08:00 - Maria Silva (Treino)        │      │
│            │   │ 09:00 - Joao Santos (Avaliacao)     │      │
│            │   │ 10:00 - [Disponivel]                │      │
│            │   └─────────────────────────────────────┘      │
│            │                                                 │
└────────────┴─────────────────────────────────────────────────┘
```

### 4.3 Lista de Alunos

```
LAYOUT:
┌─────────────────────────────────────────────────────────────┐
│ Alunos                                    [+ Novo Aluno]    │
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🔍 Buscar aluno...          [Status ▼] [Objetivo ▼]    │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [Foto] Maria Silva         Ativo    Hipertrofia  [···] │ │
│ │        maria@email.com     📱 WhatsApp                  │ │
│ ├─────────────────────────────────────────────────────────┤ │
│ │ [Foto] Joao Santos         Ativo    Emagrecimento[···] │ │
│ │        joao@email.com      ⚠️ 7 dias sem treinar       │ │
│ ├─────────────────────────────────────────────────────────┤ │
│ │ [Foto] Pedro Lima          🔴Inativo Forca       [···] │ │
│ │        pedro@email.com     Ultimo treino: 30 dias      │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│              ◀ 1  2  3  4  5 ▶    20 por pagina            │
└─────────────────────────────────────────────────────────────┘

ACOES [···]:
- Ver perfil
- Prescrever treino
- Agendar sessao
- Enviar mensagem
- Editar
```

### 4.4 Perfil do Aluno

```
LAYOUT:
┌─────────────────────────────────────────────────────────────┐
│ ← Voltar                                                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────┐   Maria Silva                                │
│  │          │   maria@email.com | (11) 99999-9999          │
│  │  [Foto]  │   Objetivo: Hipertrofia                      │
│  │          │   Aluna desde: 15/03/2025                    │
│  └──────────┘                                              │
│                                                             │
│  [Prescrever Treino] [Agendar] [WhatsApp] [Editar]         │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  [Treinos] [Evolucao] [Avaliacoes] [Agenda] [Pagamentos]   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Treinos Ativos                                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Treino A - Superior                                 │   │
│  │ Valido ate: 30/03/2026 | Frequencia: 3x/semana     │   │
│  │ Ultimo treino: Ontem                                │   │
│  └─────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Treino B - Inferior                                 │   │
│  │ Valido ate: 30/03/2026 | Frequencia: 2x/semana     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  Estatisticas                                              │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │ 45      │ │ 12      │ │ 8       │ │ 5       │          │
│  │ Treinos │ │ Streak  │ │ PRs     │ │ Badges  │          │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 4.5 Criar/Editar Treino

```
LAYOUT:
┌─────────────────────────────────────────────────────────────┐
│ Novo Treino                              [Cancelar] [Salvar]│
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Nome do treino: [Treino A - Superior________________]     │
│  Tipo: [Musculacao ▼]    Dificuldade: [Intermediario ▼]   │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Exercicios                              [+ Adicionar]      │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ⋮⋮ 1. Supino Reto                            [🗑️]  │   │
│  │    Series: [4]  Reps: [10-12]  Descanso: [60s]     │   │
│  │    Carga: [Progressiva]  Notas: [______________]   │   │
│  └─────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ⋮⋮ 2. Supino Inclinado                       [🗑️]  │   │
│  │    Series: [4]  Reps: [10-12]  Descanso: [60s]     │   │
│  └─────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ⋮⋮ 3. Crucifixo                              [🗑️]  │   │
│  │    Series: [3]  Reps: [12-15]  Descanso: [45s]     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  [+ Adicionar Superset]                                    │
│                                                             │
└─────────────────────────────────────────────────────────────┘

MODAL: Adicionar Exercicio
┌─────────────────────────────────────────────────────────────┐
│ Adicionar Exercicio                                    [X] │
├─────────────────────────────────────────────────────────────┤
│ 🔍 Buscar exercicio...                                     │
│                                                             │
│ Filtros: [Peito ▼] [Halteres ▼] [Todos niveis ▼]          │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐│
│ │ [🎬] Supino Reto com Barra                              ││
│ │      Peito, Triceps | Barra, Banco                      ││
│ ├─────────────────────────────────────────────────────────┤│
│ │ [🎬] Supino Inclinado com Halteres                      ││
│ │      Peito superior | Halteres, Banco                   ││
│ ├─────────────────────────────────────────────────────────┤│
│ │ [🎬] Crucifixo com Halteres                             ││
│ │      Peito | Halteres, Banco                            ││
│ └─────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────┘
```

### 4.6 Agenda

```
LAYOUT:
┌─────────────────────────────────────────────────────────────┐
│ Agenda                                    [+ Novo]  [Hoje] │
├─────────────────────────────────────────────────────────────┤
│  ◀  Janeiro 2026  ▶          [Dia] [Semana] [Mes]          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  VISAO SEMANA:                                             │
│                                                             │
│         Seg     Ter     Qua     Qui     Sex     Sab        │
│          6       7       8       9      10      11         │
│  ┌──────┬──────┬──────┬──────┬──────┬──────┐              │
│  │      │      │      │      │      │      │ 07:00        │
│  ├──────┼──────┼──────┼──────┼──────┼──────┤              │
│  │Maria │      │Maria │      │Maria │      │ 08:00        │
│  │Treino│      │Treino│      │Treino│      │              │
│  ├──────┼──────┼──────┼──────┼──────┼──────┤              │
│  │Joao  │Pedro │      │Joao  │      │      │ 09:00        │
│  │Aval. │Treino│      │Treino│      │      │              │
│  ├──────┼──────┼──────┼──────┼──────┼──────┤              │
│  │      │      │Pedro │      │Ana   │      │ 10:00        │
│  │      │      │Treino│      │Treino│      │              │
│  └──────┴──────┴──────┴──────┴──────┴──────┘              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. App do Aluno - Telas

### 5.1 Home

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│                        [🔔] │
│                             │
│  Ola, Maria! 👋             │
│  Bora treinar?              │
│                             │
│  ┌───────────────────────┐  │
│  │   🔥 12 dias          │  │
│  │   de sequencia!       │  │
│  │                       │  │
│  │   ████████████░░░     │  │
│  │   Nivel 3 - Dedicada  │  │
│  │   4.250 / 5.000 pts   │  │
│  └───────────────────────┘  │
│                             │
│  Treino de Hoje             │
│  ┌───────────────────────┐  │
│  │  💪 Treino A          │  │
│  │     Superior          │  │
│  │                       │  │
│  │  8 exercicios         │  │
│  │  ~45 min              │  │
│  │                       │  │
│  │  [   INICIAR   ]      │  │
│  └───────────────────────┘  │
│                             │
│  Proximos Agendamentos      │
│  ┌───────────────────────┐  │
│  │ 📅 Ter, 09/01 - 08:00 │  │
│  │    Treino com Rafaela │  │
│  └───────────────────────┘  │
│                             │
├─────────────────────────────┤
│  [🏠]  [💪]  [📊]  [👤]   │
│  Home  Treino Evolucao Eu   │
└─────────────────────────────┘
```

### 5.2 Treino

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│ ← Treino A - Superior       │
├─────────────────────────────┤
│                             │
│  8 exercicios | ~45 min     │
│                             │
│  ┌───────────────────────┐  │
│  │ 1. Supino Reto        │  │
│  │    4x 10-12 | 60s     │  │
│  │    [Ver video]        │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ 2. Supino Inclinado   │  │
│  │    4x 10-12 | 60s     │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ 3. Crucifixo          │  │
│  │    3x 12-15 | 45s     │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ 4. Desenvolvimento    │  │
│  │    4x 10-12 | 60s     │  │
│  └───────────────────────┘  │
│          ...                │
│                             │
│  ┌───────────────────────┐  │
│  │   [INICIAR TREINO]    │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

### 5.3 Execucao de Treino

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│ [X]              02:34:12   │
├─────────────────────────────┤
│                             │
│  Exercicio 1 de 8           │
│                             │
│  ┌───────────────────────┐  │
│  │                       │  │
│  │      [VIDEO DO        │  │
│  │      EXERCICIO        │  │
│  │      EM LOOP]         │  │
│  │                       │  │
│  └───────────────────────┘  │
│                             │
│  Supino Reto com Barra      │
│  4 series | 10-12 reps      │
│                             │
│  Serie 2 de 4               │
│                             │
│  Carga: [____] kg           │
│  Reps:  [____]              │
│                             │
│  ┌───────────────────────┐  │
│  │  [✓ SERIE CONCLUIDA]  │  │
│  └───────────────────────┘  │
│                             │
│  ─────────────────────────  │
│  Series: ✓ ✓ ○ ○            │
│                             │
│  [Pular exercicio]          │
│                             │
└─────────────────────────────┘

TIMER DE DESCANSO:
┌─────────────────────────────┐
│                             │
│         DESCANSO            │
│                             │
│           0:45              │
│         ━━━━━━━━━           │
│                             │
│  Proxima serie: 3 de 4      │
│                             │
│  [Pular descanso]           │
│                             │
└─────────────────────────────┘
```

### 5.4 Finalizacao de Treino

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│                             │
│        🎉 PARABENS!         │
│                             │
│    Treino concluido!        │
│                             │
│  ┌───────────────────────┐  │
│  │  Tempo: 47:23         │  │
│  │  Exercicios: 8/8      │  │
│  │  Volume: 4.520 kg     │  │
│  │  +50 pontos!          │  │
│  └───────────────────────┘  │
│                             │
│  Como foi o treino?         │
│  ┌───────────────────────┐  │
│  │ Dificuldade (RPE)     │  │
│  │ 1 2 3 4 5 6 [7] 8 9 10│  │
│  └───────────────────────┘  │
│                             │
│  Como voce esta?            │
│  ┌───────────────────────┐  │
│  │  😫  😐  🙂  😄  🔥   │  │
│  └───────────────────────┘  │
│                             │
│  Observacoes (opcional)     │
│  ┌───────────────────────┐  │
│  │                       │  │
│  └───────────────────────┘  │
│                             │
│  [📷 Adicionar selfie]      │
│                             │
│  ┌───────────────────────┐  │
│  │     [FINALIZAR]       │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

### 5.5 Evolucao

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│ Minha Evolucao              │
├─────────────────────────────┤
│                             │
│  [Peso] [Medidas] [PRs]     │
│                             │
│  Peso ao longo do tempo     │
│  ┌───────────────────────┐  │
│  │     📈                │  │
│  │   /    \    /\        │  │
│  │  /      \  /  \___    │  │
│  │ /        \/           │  │
│  │ Jan  Fev  Mar  Abr    │  │
│  └───────────────────────┘  │
│                             │
│  Peso atual: 72.5 kg        │
│  Meta: 70 kg (-2.5 kg)      │
│                             │
│  Records Pessoais           │
│  ┌───────────────────────┐  │
│  │ 🏆 Supino Reto        │  │
│  │    80 kg (10/01/26)   │  │
│  │    +5 kg desde inicio │  │
│  ├───────────────────────┤  │
│  │ 🏆 Agachamento        │  │
│  │    100 kg (08/01/26)  │  │
│  ├───────────────────────┤  │
│  │ 🏆 Levantamento Terra │  │
│  │    120 kg (05/01/26)  │  │
│  └───────────────────────┘  │
│                             │
│  [Ver fotos de progresso]   │
│                             │
└─────────────────────────────┘
```

### 5.6 Perfil / Conquistas

```
LAYOUT MOBILE:
┌─────────────────────────────┐
│ Meu Perfil                  │
├─────────────────────────────┤
│                             │
│      ┌─────────┐            │
│      │ [Foto]  │            │
│      └─────────┘            │
│      Maria Silva            │
│      Nivel 3 - Dedicada     │
│      4.250 pontos           │
│                             │
│  ┌─────────┬─────────┐      │
│  │ 45      │ 12      │      │
│  │ Treinos │ Streak  │      │
│  │ total   │ max     │      │
│  └─────────┴─────────┘      │
│                             │
│  Minhas Conquistas (5/20)   │
│  ┌───────────────────────┐  │
│  │ 🏅 Primeira Semana    │  │
│  │ 🏅 Madrugador         │  │
│  │ 🏅 Consistente        │  │
│  │ 🏅 PR Hunter          │  │
│  │ 🏅 Social             │  │
│  │ 🔒 Centenario         │  │
│  │ 🔒 Elite              │  │
│  │ 🔒 ...                │  │
│  └───────────────────────┘  │
│                             │
│  [Configuracoes]            │
│  [Sair]                     │
│                             │
└─────────────────────────────┘
```

---

## 6. Padroes de Interacao

### 6.1 Loading States

```
SKELETON LOADING:
- Usar para carregamento inicial de paginas
- Formas que imitam o conteudo final
- Animacao de pulse suave

SPINNER:
- Usar para acoes pontuais (salvar, enviar)
- Centralizado no botao ou area

PROGRESS BAR:
- Usar para operacoes longas (upload, import)
- Mostrar porcentagem quando possivel
```

### 6.2 Estados Vazios

```
ESTRUTURA:
┌─────────────────────────────┐
│                             │
│      [Ilustracao]           │
│                             │
│   Nenhum aluno cadastrado   │
│                             │
│   Comece adicionando seu    │
│   primeiro aluno.           │
│                             │
│   [+ Adicionar Aluno]       │
│                             │
└─────────────────────────────┘

PRINCIPIOS:
- Ilustracao amigavel
- Mensagem clara
- CTA para acao
```

### 6.3 Feedback de Acoes

```
TOAST NOTIFICATIONS:
- Sucesso: verde, icone check
- Erro: vermelho, icone X
- Info: azul, icone info
- Duracao: 3-5 segundos
- Posicao: top-right (desktop), top (mobile)

INLINE FEEDBACK:
- Validacao de formularios em tempo real
- Icone de status ao lado do campo
- Mensagem de erro abaixo do campo
```

### 6.4 Confirmacoes

```
ACOES DESTRUTIVAS:
- Sempre pedir confirmacao
- Modal com descricao clara
- Botao de cancelar destacado
- Botao de confirmar em vermelho

ACOES IMPORTANTES:
- Toast de sucesso
- Animacao de feedback
- Redirect automatico quando apropriado
```

---

## 7. Responsividade

### 7.1 Breakpoints

```css
--breakpoint-sm: 640px;   /* Mobile landscape */
--breakpoint-md: 768px;   /* Tablet */
--breakpoint-lg: 1024px;  /* Desktop */
--breakpoint-xl: 1280px;  /* Large desktop */
--breakpoint-2xl: 1536px; /* Extra large */
```

### 7.2 Comportamentos por Breakpoint

```
MOBILE (< 768px):
- Sidebar vira bottom navigation
- Tabelas viram cards
- Modais ocupam tela inteira
- Menus viram drawers

TABLET (768px - 1024px):
- Sidebar colapsavel
- Grid de 2 colunas
- Modais centralizados

DESKTOP (> 1024px):
- Sidebar fixa expandida
- Grid de 3-4 colunas
- Modais com max-width
```

---

## 8. Animacoes

### 8.1 Principios

- Duracao curta (150-300ms)
- Easing natural (ease-out para entrada, ease-in para saida)
- Proposito claro (feedback, orientacao, deleite)
- Respeitar preferencia do usuario (prefers-reduced-motion)

### 8.2 Animacoes Padrao

```css
/* Fade */
.fade-enter { opacity: 0; }
.fade-enter-active { opacity: 1; transition: opacity 150ms ease-out; }

/* Slide up */
.slide-up-enter { opacity: 0; transform: translateY(10px); }
.slide-up-enter-active { opacity: 1; transform: translateY(0); transition: all 200ms ease-out; }

/* Scale */
.scale-enter { opacity: 0; transform: scale(0.95); }
.scale-enter-active { opacity: 1; transform: scale(1); transition: all 150ms ease-out; }
```

### 8.3 Animacoes de Gamificacao

```
PONTOS GANHOS:
- Numero aparece com bounce
- Particulas ao redor
- Som opcional

BADGE DESBLOQUEADO:
- Modal especial com confetti
- Badge gira e brilha
- Som de conquista

LEVEL UP:
- Tela inteira com animacao
- Progresso preenchendo
- Novo nivel revelado
```

---

## 9. Acessibilidade

### 9.1 Requisitos

- Contraste minimo 4.5:1 para texto
- Todos os elementos interativos focaveis
- Labels para todos os inputs
- Alt text para imagens
- Navegacao por teclado completa
- Suporte a screen readers

### 9.2 Implementacao

```html
<!-- Botoes -->
<button aria-label="Adicionar aluno">
  <PlusIcon aria-hidden="true" />
</button>

<!-- Inputs -->
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-error" />
<span id="email-error" role="alert">Email invalido</span>

<!-- Modais -->
<div role="dialog" aria-labelledby="modal-title" aria-modal="true">
  <h2 id="modal-title">Confirmar exclusao</h2>
</div>
```

---

## 10. Performance

### 10.1 Metricas Alvo

| Metrica | Alvo |
|---------|------|
| LCP (Largest Contentful Paint) | < 2.5s |
| FID (First Input Delay) | < 100ms |
| CLS (Cumulative Layout Shift) | < 0.1 |
| TTI (Time to Interactive) | < 3.5s |

### 10.2 Otimizacoes

- Code splitting por rota
- Lazy loading de imagens
- Preload de fontes criticas
- Cache de assets estaticos
- Compressao de imagens (WebP)
- Minificacao de JS/CSS

---

*Documento gerado em 06/01/2026*
*Metodologia: BMad Framework*
