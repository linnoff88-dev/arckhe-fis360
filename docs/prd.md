# Product Requirements Document (PRD)

## FIS360 - Plataforma Inteligente de Gestao Fitness

**Versao:** 1.0
**Data:** 06/01/2026
**Status:** Aprovado
**Autor:** Product Manager

---

## 1. Introducao

### 1.1 Proposito

Este documento define os requisitos completos do produto FIS360, uma plataforma SaaS para gestao de negocios fitness que unifica academias, personal trainers e fisioterapeutas.

### 1.2 Escopo

O PRD cobre todas as funcionalidades planejadas para as Fases 1 e 2 do projeto (MVP + Studios), com visao das fases futuras.

### 1.3 Definicoes

| Termo | Definicao |
|-------|-----------|
| Business | Entidade principal (academia, studio, clinica) |
| Professional | Personal trainer, instrutor, fisioterapeuta |
| Student | Aluno ou paciente |
| Workout | Treino prescrito |
| Exercise | Exercicio individual da biblioteca |
| Assessment | Avaliacao fisica |
| Subscription | Assinatura/plano do aluno |

---

## 2. Visao do Produto

### 2.1 Declaracao de Visao

> Ser a plataforma de gestao fitness mais inteligente do Brasil, reduzindo o churn de academias em 50% e permitindo que profissionais escalem seu negocio atraves de tecnologia.

### 2.2 Objetivos do Produto

1. **Retencao:** Reduzir churn medio de 7% para 4% ao mes
2. **Engajamento:** Aumentar frequencia de treino em 25%
3. **Escala:** Permitir que personals atendam 3x mais alunos
4. **Experiencia:** NPS do aluno > 50

### 2.3 Personas

#### Persona 1: Marcos - Dono de Academia
- 42 anos, proprietario de academia de bairro
- 400 alunos, R$ 80k/mes faturamento
- Problema: Churn alto, sistema antigo
- Quer: Retencao inteligente, app moderno

#### Persona 2: Rafaela - Personal Trainer
- 29 anos, autonoma com 25 alunos
- R$ 15k/mes, quer escalar
- Problema: Limite de horas, ferramentas amadoras
- Quer: App proprio, modelo hibrido

#### Persona 3: Dr. Fernando - Fisioterapeuta
- 38 anos, clinica com 3 fisios
- 200 pacientes ativos
- Problema: Prontuario em papel, acompanhamento
- Quer: Prontuario digital, exercicios para casa

#### Persona 4: Lucas - Aluno
- 28 anos, treina 4x/semana
- Quer resultados visiveis
- Problema: Falta motivacao, app generico
- Quer: Progresso visual, gamificacao

---

## 3. Requisitos Funcionais

### 3.1 Epicos e Priorizacao

| ID | Epico | Prioridade | Fase | Complexidade |
|----|-------|------------|------|--------------|
| E1 | Autenticacao e Multi-tenancy | Must Have | 1 | Alta |
| E2 | Gestao de Alunos | Must Have | 1 | Media |
| E3 | Biblioteca de Exercicios | Must Have | 1 | Media |
| E4 | Prescricao de Treinos | Must Have | 1 | Alta |
| E5 | App do Aluno | Must Have | 1 | Alta |
| E6 | Agenda e Agendamentos | Must Have | 1 | Media |
| E7 | Integracao WhatsApp | Must Have | 1 | Media |
| E8 | Gamificacao Basica | Should Have | 1 | Media |
| E9 | Dashboard e Metricas | Should Have | 1 | Media |
| E10 | Aulas Coletivas | Must Have | 2 | Media |
| E11 | Avaliacoes Fisicas | Must Have | 2 | Media |
| E12 | Gamificacao Avancada | Should Have | 2 | Alta |
| E13 | Comunidade e Feed | Could Have | 2 | Media |
| E14 | Financeiro Basico | Should Have | 2 | Alta |

---

## 4. Epico 1: Autenticacao e Multi-tenancy

### 4.1 Descricao

Sistema de autenticacao seguro com suporte a multiplos negocios (tenants) isolados, controle de acesso baseado em roles e gestao de sessoes.

### 4.2 User Stories

#### US-1.1: Registro de Negocio
```
COMO um profissional fitness
QUERO criar uma conta para meu negocio
PARA comecar a usar a plataforma

Criterios de Aceite:
- [ ] Formulario com: nome, email, telefone, tipo de negocio
- [ ] Validacao de email unico
- [ ] Criacao automatica de slug unico (ex: rafaela-personal)
- [ ] Envio de email de confirmacao
- [ ] Redirect para onboarding apos confirmacao

Regras de Negocio:
- Tipos de negocio: GYM, PERSONAL_STUDIO, PHYSIO_CLINIC, CROSSFIT_BOX, PILATES_STUDIO, ONLINE_ONLY, HYBRID
- Slug gerado a partir do nome, com sufixo numerico se duplicado
- Trial de 14 dias automatico
```

#### US-1.2: Login de Usuario
```
COMO um usuario cadastrado
QUERO fazer login na plataforma
PARA acessar minha conta

Criterios de Aceite:
- [ ] Login com email e senha
- [ ] Opcao "Lembrar de mim"
- [ ] Link "Esqueci minha senha"
- [ ] Redirect para dashboard apos login
- [ ] Mensagem de erro para credenciais invalidas

Regras de Negocio:
- JWT com expiracao de 7 dias (lembrar) ou 24h (nao lembrar)
- Refresh token com expiracao de 30 dias
- Maximo de 5 tentativas antes de bloqueio temporario (15 min)
```

#### US-1.3: Recuperacao de Senha
```
COMO um usuario que esqueceu a senha
QUERO recuperar acesso a minha conta
PARA continuar usando a plataforma

Criterios de Aceite:
- [ ] Formulario com campo de email
- [ ] Envio de email com link de reset (expira em 1h)
- [ ] Pagina de definicao de nova senha
- [ ] Confirmacao de senha alterada
- [ ] Invalidacao de tokens anteriores

Regras de Negocio:
- Token de reset expira em 1 hora
- Apenas 3 solicitacoes por hora por email
- Nova senha deve ter minimo 8 caracteres
```

#### US-1.4: Gestao de Usuarios do Negocio
```
COMO um dono de negocio
QUERO gerenciar usuarios da minha equipe
PARA controlar acesso ao sistema

Criterios de Aceite:
- [ ] Listar usuarios do negocio
- [ ] Convidar novo usuario por email
- [ ] Definir role do usuario
- [ ] Ativar/desativar usuario
- [ ] Remover usuario

Roles disponiveis:
- BUSINESS_OWNER: Acesso total
- MANAGER: Acesso administrativo (sem billing)
- PROFESSIONAL: Acesso aos proprios alunos
- RECEPTIONIST: Acesso limitado (checkin, agenda)
```

#### US-1.5: Perfil do Negocio
```
COMO um dono de negocio
QUERO configurar o perfil da minha empresa
PARA personalizar a experiencia

Criterios de Aceite:
- [ ] Editar nome, endereco, telefone
- [ ] Upload de logo
- [ ] Definir cor primaria (branding)
- [ ] Configurar horario de funcionamento
- [ ] Definir timezone
```

### 4.3 Requisitos Tecnicos

- JWT para autenticacao stateless
- Refresh tokens armazenados em Redis
- Bcrypt para hash de senhas (cost factor 12)
- Rate limiting por IP e por usuario
- Middleware de tenant isolation em todas as rotas

---

## 5. Epico 2: Gestao de Alunos

### 5.1 Descricao

CRUD completo de alunos com informacoes pessoais, objetivos, restricoes de saude e historico de atividades.

### 5.2 User Stories

#### US-2.1: Cadastro de Aluno
```
COMO um profissional
QUERO cadastrar um novo aluno
PARA comecar a atende-lo

Criterios de Aceite:
- [ ] Formulario com dados pessoais (nome, email, telefone, nascimento)
- [ ] Campos opcionais: CPF, endereco, foto
- [ ] Selecao de objetivos (multiplos)
- [ ] Campo de observacoes de saude
- [ ] Campo de lesoes/restricoes
- [ ] Contato de emergencia

Objetivos disponiveis:
- WEIGHT_LOSS, MUSCLE_GAIN, STRENGTH, ENDURANCE
- FLEXIBILITY, REHABILITATION, HEALTH, SPORT_SPECIFIC
- BODY_RECOMPOSITION
```

#### US-2.2: Listagem de Alunos
```
COMO um profissional
QUERO ver a lista de todos os meus alunos
PARA gerenciar minha carteira

Criterios de Aceite:
- [ ] Lista paginada (20 por pagina)
- [ ] Busca por nome, email ou telefone
- [ ] Filtro por status (ativo, inativo, pausado)
- [ ] Filtro por objetivo
- [ ] Ordenacao por nome, data de cadastro, ultima atividade
- [ ] Indicador visual de risco de churn
- [ ] Acesso rapido ao WhatsApp
```

#### US-2.3: Perfil do Aluno
```
COMO um profissional
QUERO ver o perfil completo de um aluno
PARA ter visao 360 graus

Criterios de Aceite:
- [ ] Dados pessoais editaveis
- [ ] Historico de treinos
- [ ] Evolucao (graficos)
- [ ] Avaliacoes realizadas
- [ ] Fotos de progresso
- [ ] Assinaturas/pagamentos
- [ ] Timeline de atividades
- [ ] Proximos agendamentos
```

#### US-2.4: Importacao de Alunos
```
COMO um profissional
QUERO importar alunos de uma planilha
PARA migrar de outro sistema

Criterios de Aceite:
- [ ] Upload de arquivo CSV/Excel
- [ ] Mapeamento de colunas
- [ ] Preview antes de importar
- [ ] Tratamento de duplicados
- [ ] Relatorio de erros
- [ ] Importacao em background para listas grandes
```

#### US-2.5: Convite para App do Aluno
```
COMO um profissional
QUERO convidar um aluno para usar o app
PARA que ele acompanhe seus treinos

Criterios de Aceite:
- [ ] Botao "Convidar para app" no perfil
- [ ] Envio de link por WhatsApp ou email
- [ ] Link gera conta automatica para o aluno
- [ ] Aluno define senha no primeiro acesso
- [ ] Notificacao ao profissional quando aluno ativar
```

### 5.3 Requisitos Tecnicos

- Soft delete para alunos (nunca apagar dados)
- Criptografia de dados sensiveis (CPF, saude)
- Indice full-text para busca
- Cache de listagem com invalidacao

---

## 6. Epico 3: Biblioteca de Exercicios

### 6.1 Descricao

Biblioteca completa de exercicios com videos demonstrativos, instrucoes e categorizacao por grupo muscular e equipamento.

### 6.2 User Stories

#### US-3.1: Visualizar Biblioteca
```
COMO um profissional
QUERO navegar pela biblioteca de exercicios
PARA montar treinos

Criterios de Aceite:
- [ ] Grid de exercicios com thumbnail
- [ ] Filtro por categoria (peito, costas, pernas, etc)
- [ ] Filtro por equipamento
- [ ] Filtro por dificuldade
- [ ] Busca por nome
- [ ] Exercicios globais + exercicios do negocio
```

#### US-3.2: Detalhes do Exercicio
```
COMO um profissional ou aluno
QUERO ver detalhes de um exercicio
PARA entender a execucao correta

Criterios de Aceite:
- [ ] Video demonstrativo (loop)
- [ ] Nome e descricao
- [ ] Instrucoes passo a passo
- [ ] Musculos trabalhados (visual)
- [ ] Equipamento necessario
- [ ] Nivel de dificuldade
- [ ] Exercicios alternativos sugeridos
```

#### US-3.3: Criar Exercicio Personalizado
```
COMO um profissional
QUERO criar um exercicio personalizado
PARA adicionar a minha biblioteca

Criterios de Aceite:
- [ ] Formulario com nome, descricao, instrucoes
- [ ] Upload de video (ate 100MB)
- [ ] Selecao de categoria e musculos
- [ ] Selecao de equipamentos
- [ ] Definir dificuldade
- [ ] Opcao de clonar exercicio existente
```

#### US-3.4: Biblioteca Global Seed
```
COMO administrador da plataforma
QUERO disponibilizar biblioteca inicial
PARA que negocios ja tenham exercicios

Criterios de Aceite:
- [ ] Minimo 200 exercicios base
- [ ] Cobertura de todos os grupos musculares
- [ ] Videos de qualidade profissional
- [ ] Exercicios para iniciantes ate avancados
- [ ] Exercicios com e sem equipamento
```

### 6.3 Categorias de Exercicios

```
CHEST, BACK, SHOULDERS, BICEPS, TRICEPS, FOREARMS
ABS, QUADRICEPS, HAMSTRINGS, GLUTES, CALVES
FULL_BODY, CARDIO, MOBILITY, REHABILITATION
```

### 6.4 Requisitos Tecnicos

- Videos em CDN (Bunny ou CloudFront)
- Transcoding automatico (720p, 480p)
- Lazy loading de videos
- Cache agressivo de thumbnails

---

## 7. Epico 4: Prescricao de Treinos

### 7.1 Descricao

Sistema completo para criar, prescrever e gerenciar treinos personalizados para alunos.

### 7.2 User Stories

#### US-4.1: Criar Template de Treino
```
COMO um profissional
QUERO criar um template de treino reutilizavel
PARA agilizar a prescricao

Criterios de Aceite:
- [ ] Nome e descricao do treino
- [ ] Tipo (musculacao, cardio, HIIT, funcional, etc)
- [ ] Nivel de dificuldade
- [ ] Duracao estimada
- [ ] Adicionar exercicios com: series, reps, carga, descanso
- [ ] Ordenar exercicios (drag and drop)
- [ ] Agrupar exercicios (superset, circuito)
- [ ] Notas por exercicio
- [ ] Salvar como template
```

#### US-4.2: Prescrever Treino para Aluno
```
COMO um profissional
QUERO prescrever um treino para um aluno
PARA que ele execute

Criterios de Aceite:
- [ ] Selecionar aluno
- [ ] Criar treino do zero ou usar template
- [ ] Personalizar exercicios para o aluno
- [ ] Definir periodo de validade
- [ ] Definir dias da semana
- [ ] Definir frequencia semanal
- [ ] Notificar aluno via WhatsApp/push
```

#### US-4.3: Visualizar Treinos do Aluno
```
COMO um profissional
QUERO ver todos os treinos de um aluno
PARA acompanhar sua programacao

Criterios de Aceite:
- [ ] Lista de treinos ativos
- [ ] Historico de treinos anteriores
- [ ] Status de cada treino (ativo, expirado, pausado)
- [ ] Estatisticas de adesao
- [ ] Duplicar treino existente
```

#### US-4.4: Divisao de Treino (ABC)
```
COMO um profissional
QUERO criar divisao de treino em series
PARA organizar treinos semanais

Criterios de Aceite:
- [ ] Criar divisao (A, B, C, D, etc)
- [ ] Associar treino a cada letra
- [ ] Definir rotacao automatica
- [ ] Visualizacao em calendario
- [ ] Aluno ve proximo treino da serie
```

### 7.3 Requisitos Tecnicos

- Versionamento de treinos (historico de alteracoes)
- Clone profundo de templates
- Validacao de exercicios ao prescrever

---

## 8. Epico 5: App do Aluno

### 8.1 Descricao

Aplicativo (PWA) para o aluno acessar treinos, registrar execucao, acompanhar evolucao e interagir com o profissional.

### 8.2 User Stories

#### US-5.1: Home do Aluno
```
COMO um aluno
QUERO ver minha tela inicial personalizada
PARA saber o que fazer hoje

Criterios de Aceite:
- [ ] Saudacao personalizada
- [ ] Treino do dia destacado
- [ ] Streak atual (dias consecutivos)
- [ ] Proximos agendamentos
- [ ] Pontos e nivel atual
- [ ] Mensagem motivacional
- [ ] Acesso rapido a funcoes principais
```

#### US-5.2: Visualizar Treino
```
COMO um aluno
QUERO ver meu treino prescrito
PARA saber o que executar

Criterios de Aceite:
- [ ] Lista de exercicios com ordem
- [ ] Detalhes: series, reps, carga, descanso
- [ ] Acesso ao video de cada exercicio
- [ ] Notas do profissional
- [ ] Botao "Iniciar Treino"
- [ ] Indicador de treino ja realizado hoje
```

#### US-5.3: Executar Treino
```
COMO um aluno
QUERO executar meu treino guiado pelo app
PARA ter suporte durante o treino

Criterios de Aceite:
- [ ] Navegacao exercicio por exercicio
- [ ] Video do exercicio em loop
- [ ] Timer de descanso entre series
- [ ] Registrar carga usada por serie
- [ ] Marcar serie como concluida
- [ ] Contador de series restantes
- [ ] Botao "Pular exercicio"
- [ ] Botao "Finalizar treino"
- [ ] Tempo total de treino
```

#### US-5.4: Finalizar e Avaliar Treino
```
COMO um aluno
QUERO finalizar e avaliar meu treino
PARA registrar como foi

Criterios de Aceite:
- [ ] Resumo do treino (exercicios, volume total)
- [ ] Avaliacao de dificuldade (1-10 RPE)
- [ ] Avaliacao de humor (emojis)
- [ ] Campo de observacoes
- [ ] Opcao de tirar selfie
- [ ] Pontos ganhos exibidos
- [ ] Animacao de conquista se aplicavel
- [ ] Compartilhar no feed (opcional)
```

#### US-5.5: Historico de Treinos
```
COMO um aluno
QUERO ver meu historico de treinos
PARA acompanhar minha consistencia

Criterios de Aceite:
- [ ] Calendario com dias treinados marcados
- [ ] Lista de treinos por mes
- [ ] Detalhes de cada treino realizado
- [ ] Estatisticas: frequencia, volume, PRs
- [ ] Comparacao com metas
```

#### US-5.6: Minha Evolucao
```
COMO um aluno
QUERO ver minha evolucao
PARA me motivar

Criterios de Aceite:
- [ ] Grafico de peso ao longo do tempo
- [ ] Grafico de medidas (se houver)
- [ ] Fotos de progresso lado a lado
- [ ] Records pessoais (PRs) por exercicio
- [ ] Badges conquistados
- [ ] Timeline de conquistas
```

### 8.3 Requisitos Tecnicos

- PWA com service worker para offline
- Sincronizacao quando voltar online
- Push notifications
- Local storage para treino em execucao
- Design responsivo (mobile-first)

---

## 9. Epico 6: Agenda e Agendamentos

### 9.1 Descricao

Sistema de agendamento de sessoes, aulas e consultas com confirmacao automatica e lembretes.

### 9.2 User Stories

#### US-6.1: Visualizar Agenda (Profissional)
```
COMO um profissional
QUERO ver minha agenda de atendimentos
PARA organizar meu dia

Criterios de Aceite:
- [ ] Visao de dia, semana e mes
- [ ] Agendamentos coloridos por status
- [ ] Horarios disponiveis vs ocupados
- [ ] Arrastar para remarcar
- [ ] Click para ver detalhes
- [ ] Filtro por tipo de servico
```

#### US-6.2: Criar Agendamento
```
COMO um profissional ou recepcionista
QUERO criar um novo agendamento
PARA reservar horario com aluno

Criterios de Aceite:
- [ ] Selecionar aluno
- [ ] Selecionar servico
- [ ] Selecionar data e hora
- [ ] Verificar conflitos automaticamente
- [ ] Definir recorrencia (opcional)
- [ ] Adicionar observacoes
- [ ] Enviar confirmacao por WhatsApp
```

#### US-6.3: Confirmar/Cancelar Agendamento
```
COMO um profissional ou aluno
QUERO confirmar ou cancelar um agendamento
PARA gerenciar minha agenda

Criterios de Aceite:
- [ ] Botao de confirmar no app/WhatsApp
- [ ] Botao de cancelar com motivo
- [ ] Politica de cancelamento configuravel
- [ ] Notificacao para ambas as partes
- [ ] Liberacao do horario automatica
```

#### US-6.4: Lembretes Automaticos
```
COMO sistema
QUERO enviar lembretes de agendamentos
PARA reduzir no-shows

Criterios de Aceite:
- [ ] Lembrete 24h antes (WhatsApp)
- [ ] Lembrete 1h antes (push notification)
- [ ] Link para confirmar/cancelar no lembrete
- [ ] Configuracao de horarios de lembrete
```

#### US-6.5: Agendamento pelo Aluno
```
COMO um aluno
QUERO agendar uma sessao pelo app
PARA ter autonomia

Criterios de Aceite:
- [ ] Ver horarios disponiveis do profissional
- [ ] Selecionar data e hora
- [ ] Confirmar agendamento
- [ ] Receber confirmacao
- [ ] Ver meus agendamentos futuros
- [ ] Cancelar com antecedencia minima
```

### 9.3 Configuracoes de Agenda

- Horario de funcionamento por dia
- Duracao padrao de sessao
- Antecedencia minima para agendar
- Antecedencia minima para cancelar
- Maximo de agendamentos por dia

---

## 10. Epico 7: Integracao WhatsApp

### 10.1 Descricao

Integracao com WhatsApp via Evolution API para comunicacao automatizada e manual com alunos.

### 10.2 User Stories

#### US-7.1: Conectar WhatsApp
```
COMO um dono de negocio
QUERO conectar meu WhatsApp ao sistema
PARA automatizar comunicacao

Criterios de Aceite:
- [ ] Gerar QR Code para conexao
- [ ] Exibir status de conexao
- [ ] Reconectar automaticamente se desconectar
- [ ] Notificar se desconectado por muito tempo
- [ ] Opcao de desconectar
```

#### US-7.2: Enviar Mensagem Manual
```
COMO um profissional
QUERO enviar mensagem para um aluno
PARA comunicar algo especifico

Criterios de Aceite:
- [ ] Botao de WhatsApp no perfil do aluno
- [ ] Abrir conversa no WhatsApp Web ou app
- [ ] Alternativa: enviar pelo sistema
- [ ] Historico de mensagens enviadas
```

#### US-7.3: Mensagens Automaticas
```
COMO sistema
QUERO enviar mensagens automaticas
PARA engajar alunos

Tipos de mensagem:
- [ ] Confirmacao de agendamento
- [ ] Lembrete de agendamento
- [ ] Novo treino prescrito
- [ ] Parabens por conquista
- [ ] Lembrete de inatividade
- [ ] Feliz aniversario
- [ ] Cobranca de pagamento

Criterios de Aceite:
- [ ] Templates configurave
- [ ] Variaveis dinamicas (nome, data, etc)
- [ ] Fila de envio para evitar spam
- [ ] Log de mensagens enviadas
- [ ] Metricas de entrega
```

#### US-7.4: Chatbot Basico
```
COMO sistema
QUERO responder mensagens simples automaticamente
PARA agilizar atendimento

Criterios de Aceite:
- [ ] Respostas para perguntas frequentes
- [ ] Confirmacao de agendamento por resposta
- [ ] Encaminhar para humano quando necessario
- [ ] Horario de funcionamento automatico
```

### 10.3 Requisitos Tecnicos

- Evolution API v2 self-hosted
- Webhook para receber mensagens
- Fila Redis para envio (rate limiting)
- Retry com backoff exponencial
- Fallback para SMS se WhatsApp falhar

---

## 11. Epico 8: Gamificacao Basica

### 11.1 Descricao

Sistema de pontos, streaks e badges para motivar alunos e aumentar engajamento.

### 11.2 User Stories

#### US-8.1: Sistema de Pontos
```
COMO um aluno
QUERO ganhar pontos por minhas atividades
PARA me sentir recompensado

Eventos que geram pontos:
- [ ] Check-in na academia: 10 pts
- [ ] Treino completado: 50 pts
- [ ] Treino com avaliacao: +10 pts
- [ ] PR batido: 100 pts
- [ ] Meta semanal atingida: 200 pts
- [ ] Indicacao de amigo: 500 pts

Criterios de Aceite:
- [ ] Exibir pontos totais no perfil
- [ ] Historico de pontos ganhos
- [ ] Animacao ao ganhar pontos
- [ ] Nivel baseado em pontos
```

#### US-8.2: Sistema de Streaks
```
COMO um aluno
QUERO manter minha sequencia de treinos
PARA criar habito

Criterios de Aceite:
- [ ] Contador de dias consecutivos
- [ ] Definicao de "dia treinado" (1+ treino)
- [ ] Tolerancia de 1 dia (configuravel)
- [ ] Alerta de streak em risco
- [ ] Record de maior streak
- [ ] Bonus de pontos por streak (multiplicador)
```

#### US-8.3: Badges e Conquistas
```
COMO um aluno
QUERO desbloquear badges
PARA colecionar conquistas

Badges iniciais:
- [ ] "Primeira Semana" - 7 dias seguidos
- [ ] "Madrugador" - 10 treinos antes das 7h
- [ ] "Noturno" - 10 treinos apos 21h
- [ ] "Consistente" - 30 dias sem faltar
- [ ] "Centenario" - 100 treinos
- [ ] "PR Hunter" - 10 PRs em 1 mes
- [ ] "Social" - 10 interacoes no feed

Criterios de Aceite:
- [ ] Notificacao ao desbloquear
- [ ] Animacao especial
- [ ] Exibir no perfil
- [ ] Compartilhar conquista
```

#### US-8.4: Niveis
```
COMO um aluno
QUERO subir de nivel
PARA mostrar minha dedicacao

Niveis:
- Nivel 1: Iniciante (0-1.000 pts)
- Nivel 2: Regular (1.000-5.000 pts)
- Nivel 3: Dedicado (5.000-15.000 pts)
- Nivel 4: Atleta (15.000-50.000 pts)
- Nivel 5: Elite (50.000+ pts)

Criterios de Aceite:
- [ ] Exibir nivel no perfil
- [ ] Barra de progresso para proximo nivel
- [ ] Celebracao ao subir de nivel
- [ ] Beneficios por nivel (futuro)
```

---

## 12. Epico 9: Dashboard e Metricas

### 12.1 Descricao

Dashboard para profissionais acompanharem metricas do negocio e dos alunos.

### 12.2 User Stories

#### US-9.1: Dashboard Principal
```
COMO um profissional
QUERO ver metricas do meu negocio
PARA tomar decisoes

Metricas principais:
- [ ] Total de alunos ativos
- [ ] Novos alunos no mes
- [ ] Alunos em risco de churn
- [ ] Treinos realizados na semana
- [ ] Agendamentos de hoje
- [ ] Taxa de frequencia media
- [ ] Receita do mes (se modulo financeiro)

Criterios de Aceite:
- [ ] Graficos interativos
- [ ] Comparacao com periodo anterior
- [ ] Filtro por periodo
- [ ] Export para PDF/Excel
```

#### US-9.2: Alertas de Churn
```
COMO um profissional
QUERO ser alertado sobre alunos em risco
PARA agir proativamente

Criterios de risco:
- [ ] Nao treinou ha 7+ dias
- [ ] Frequencia caiu 50%+
- [ ] Nao abre app ha 5+ dias
- [ ] Cancelou agendamentos recentes
- [ ] Pagamento atrasado

Criterios de Aceite:
- [ ] Lista de alunos em risco
- [ ] Nivel de risco (amarelo, laranja, vermelho)
- [ ] Sugestao de acao
- [ ] Botao para contatar
- [ ] Marcar como "tratado"
```

#### US-9.3: Relatorio de Aluno
```
COMO um profissional
QUERO gerar relatorio de um aluno
PARA mostrar evolucao

Criterios de Aceite:
- [ ] Selecionar periodo
- [ ] Incluir: frequencia, treinos, evolucao
- [ ] Graficos de progresso
- [ ] Comparativo de avaliacoes
- [ ] Export para PDF
- [ ] Enviar por WhatsApp/email
```

---

## 13. Epico 10: Aulas Coletivas (Fase 2)

### 13.1 Descricao

Sistema para gerenciar aulas em grupo com reserva de vagas, check-in e waitlist.

### 13.2 User Stories

#### US-10.1: Criar Grade de Aulas
```
COMO um gerente
QUERO criar a grade semanal de aulas
PARA organizar a programacao

Criterios de Aceite:
- [ ] Criar aula com: nome, instrutor, sala, horario
- [ ] Definir capacidade maxima
- [ ] Definir dias da semana de recorrencia
- [ ] Cor para identificacao visual
- [ ] Ativar/desativar aula
```

#### US-10.2: Reservar Vaga em Aula
```
COMO um aluno
QUERO reservar vaga em uma aula
PARA garantir minha participacao

Criterios de Aceite:
- [ ] Ver aulas disponiveis
- [ ] Ver vagas restantes
- [ ] Reservar com 1 click
- [ ] Entrar em waitlist se lotado
- [ ] Cancelar reserva
- [ ] Notificacao se sair da waitlist
```

#### US-10.3: Check-in em Aula
```
COMO um instrutor ou recepcionista
QUERO fazer check-in dos alunos
PARA controlar presenca

Criterios de Aceite:
- [ ] Lista de alunos com reserva
- [ ] Marcar presenca
- [ ] Marcar no-show
- [ ] Adicionar aluno sem reserva (se houver vaga)
- [ ] Check-in por QR Code (aluno)
```

---

## 14. Epico 11: Avaliacoes Fisicas (Fase 2)

### 14.1 Descricao

Sistema completo de avaliacoes fisicas com antropometria, testes e acompanhamento de evolucao.

### 14.2 User Stories

#### US-11.1: Realizar Avaliacao
```
COMO um profissional
QUERO realizar avaliacao fisica completa
PARA ter baseline do aluno

Campos da avaliacao:
- [ ] Peso, altura
- [ ] Circunferencias (9 medidas)
- [ ] Dobras cutaneas (7 dobras - Pollock)
- [ ] Calculo automatico: IMC, % gordura, massa magra
- [ ] Testes de flexibilidade
- [ ] Testes de forca
- [ ] Testes cardio (opcional)
- [ ] Fotos padronizadas

Criterios de Aceite:
- [ ] Formulario guiado passo a passo
- [ ] Calculos automaticos
- [ ] Comparacao com avaliacao anterior
- [ ] Geracao de relatorio PDF
```

#### US-11.2: Fotos de Progresso
```
COMO um aluno
QUERO registrar fotos de progresso
PARA ver minha evolucao visual

Criterios de Aceite:
- [ ] Captura guiada (frente, lado, costas)
- [ ] Marcacao de data
- [ ] Comparacao lado a lado
- [ ] Slider de antes/depois
- [ ] Privacidade (so aluno e profissional veem)
```

---

## 15. Epico 12: Gamificacao Avancada (Fase 2)

### 15.1 Descricao

Recursos avancados de gamificacao incluindo desafios, rankings e sistema de Guilds.

### 15.2 User Stories

#### US-12.1: Desafios
```
COMO um gerente
QUERO criar desafios para os alunos
PARA aumentar engajamento

Tipos de desafio:
- [ ] Frequencia (X treinos em Y dias)
- [ ] Volume (levantar X kg total)
- [ ] Consistencia (Y dias seguidos)
- [ ] Coletivo (academia queimar X calorias)

Criterios de Aceite:
- [ ] Criar desafio com regras e periodo
- [ ] Definir premios
- [ ] Ranking em tempo real
- [ ] Notificacoes de progresso
- [ ] Celebracao dos vencedores
```

#### US-12.2: Rankings/Leaderboards
```
COMO um aluno
QUERO ver minha posicao no ranking
PARA competir com outros

Criterios de Aceite:
- [ ] Ranking semanal/mensal
- [ ] Filtro por categoria (idade, objetivo)
- [ ] Top 10 destacado
- [ ] Minha posicao sempre visivel
- [ ] Reset periodico para dar chance a todos
```

#### US-12.3: Sistema de Guilds
```
COMO um aluno
QUERO participar de uma Guild
PARA treinar em grupo

Criterios de Aceite:
- [ ] Criar Guild (5-10 membros)
- [ ] Nome, descricao, objetivo
- [ ] Convite por link
- [ ] Meta coletiva semanal
- [ ] Chat da Guild
- [ ] Ranking entre Guilds
- [ ] Recompensas coletivas
```

---

## 16. Requisitos Nao Funcionais

### 16.1 Performance

| Metrica | Requisito |
|---------|-----------|
| Tempo de carregamento inicial | < 3s |
| Tempo de resposta API | < 200ms (p95) |
| Tempo de carregamento de pagina | < 1s |
| Uptime | 99.5% |

### 16.2 Seguranca

- HTTPS obrigatorio
- JWT com expiracao
- Rate limiting por IP e usuario
- Sanitizacao de inputs
- LGPD compliance
- Criptografia de dados sensiveis
- Backup diario automatico

### 16.3 Escalabilidade

- Arquitetura stateless
- Cache distribuido (Redis)
- Banco de dados com replicas
- CDN para assets estaticos
- Filas para processos async

### 16.4 Usabilidade

- Design responsivo (mobile-first)
- Acessibilidade WCAG 2.1 AA
- Suporte a modo escuro
- Onboarding guiado
- Tooltips e ajuda contextual

### 16.5 Compatibilidade

- Browsers: Chrome, Safari, Firefox, Edge (ultimas 2 versoes)
- Mobile: iOS 14+, Android 10+
- PWA com suporte offline

---

## 17. Roadmap de Releases

### Release 1.0 - MVP (Abril 2026)

**Epicos incluidos:** E1, E2, E3, E4, E5, E6, E7

**Features principais:**
- Autenticacao e multi-tenancy
- CRUD de alunos
- Biblioteca de exercicios
- Prescricao de treinos
- App do aluno basico
- Agenda
- WhatsApp

### Release 1.5 - Gamificacao (Maio 2026)

**Epicos incluidos:** E8, E9

**Features principais:**
- Pontos e streaks
- Badges
- Dashboard de metricas
- Alertas de churn

### Release 2.0 - Studios (Agosto 2026)

**Epicos incluidos:** E10, E11, E12

**Features principais:**
- Aulas coletivas
- Avaliacoes fisicas
- Desafios e rankings
- Guilds

### Release 3.0 - Academias (2027)

- Integracao catracas
- Financeiro completo
- Multi-unidades

### Release 4.0 - Fisioterapia (2027)

- Prontuario digital
- Protocolos de tratamento
- Laudos automaticos

---

## 18. Aprovacoes

| Papel | Nome | Data | Assinatura |
|-------|------|------|------------|
| Product Owner | - | 06/01/2026 | Aprovado |
| Tech Lead | - | 06/01/2026 | Aprovado |
| UX Designer | - | 06/01/2026 | Aprovado |

---

*Documento gerado em 06/01/2026*
*Metodologia: BMad Framework*
*Versao do PRD: 1.0*
