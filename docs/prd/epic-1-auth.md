# Epico 1: Autenticacao e Multi-tenancy

**Prioridade:** Must Have
**Fase:** 1
**Complexidade:** Alta

---

## Descricao

Sistema de autenticacao seguro com suporte a multiplos negocios (tenants) isolados, controle de acesso baseado em roles e gestao de sessoes.

---

## User Stories

### US-1.1: Registro de Negocio

**Como** um profissional fitness
**Quero** criar uma conta para meu negocio
**Para** comecar a usar a plataforma

**Criterios de Aceite:**
- [ ] Formulario com: nome, email, telefone, tipo de negocio
- [ ] Validacao de email unico
- [ ] Criacao automatica de slug unico (ex: rafaela-personal)
- [ ] Envio de email de confirmacao
- [ ] Redirect para onboarding apos confirmacao

**Regras de Negocio:**
- Tipos de negocio: GYM, PERSONAL_STUDIO, PHYSIO_CLINIC, CROSSFIT_BOX, PILATES_STUDIO, ONLINE_ONLY, HYBRID
- Slug gerado a partir do nome, com sufixo numerico se duplicado
- Trial de 14 dias automatico

---

### US-1.2: Login de Usuario

**Como** um usuario cadastrado
**Quero** fazer login na plataforma
**Para** acessar minha conta

**Criterios de Aceite:**
- [ ] Login com email e senha
- [ ] Opcao "Lembrar de mim"
- [ ] Link "Esqueci minha senha"
- [ ] Redirect para dashboard apos login
- [ ] Mensagem de erro para credenciais invalidas

**Regras de Negocio:**
- JWT com expiracao de 7 dias (lembrar) ou 24h (nao lembrar)
- Refresh token com expiracao de 30 dias
- Maximo de 5 tentativas antes de bloqueio temporario (15 min)

---

### US-1.3: Recuperacao de Senha

**Como** um usuario que esqueceu a senha
**Quero** recuperar acesso a minha conta
**Para** continuar usando a plataforma

**Criterios de Aceite:**
- [ ] Formulario com campo de email
- [ ] Envio de email com link de reset (expira em 1h)
- [ ] Pagina de definicao de nova senha
- [ ] Confirmacao de senha alterada
- [ ] Invalidacao de tokens anteriores

**Regras de Negocio:**
- Token de reset expira em 1 hora
- Apenas 3 solicitacoes por hora por email
- Nova senha deve ter minimo 8 caracteres

---

### US-1.4: Gestao de Usuarios do Negocio

**Como** um dono de negocio
**Quero** gerenciar usuarios da minha equipe
**Para** controlar acesso ao sistema

**Criterios de Aceite:**
- [ ] Listar usuarios do negocio
- [ ] Convidar novo usuario por email
- [ ] Definir role do usuario
- [ ] Ativar/desativar usuario
- [ ] Remover usuario

**Roles disponiveis:**
- BUSINESS_OWNER: Acesso total
- MANAGER: Acesso administrativo (sem billing)
- PROFESSIONAL: Acesso aos proprios alunos
- RECEPTIONIST: Acesso limitado (checkin, agenda)

---

### US-1.5: Perfil do Negocio

**Como** um dono de negocio
**Quero** configurar o perfil da minha empresa
**Para** personalizar a experiencia

**Criterios de Aceite:**
- [ ] Editar nome, endereco, telefone
- [ ] Upload de logo
- [ ] Definir cor primaria (branding)
- [ ] Configurar horario de funcionamento
- [ ] Definir timezone

---

## Requisitos Tecnicos

- JWT para autenticacao stateless
- Refresh tokens armazenados em Redis
- Bcrypt para hash de senhas (cost factor 12)
- Rate limiting por IP e por usuario
- Middleware de tenant isolation em todas as rotas

---

## Dependencias

- Nenhuma (epico fundacional)

---

## Arquivos Relacionados

```
apps/api/src/modules/auth/
├── auth.controller.ts
├── auth.service.ts
├── auth.routes.ts
├── auth.schema.ts
└── auth.types.ts

apps/api/src/modules/users/
├── users.controller.ts
├── users.service.ts
└── users.routes.ts

apps/api/src/modules/businesses/
├── businesses.controller.ts
├── businesses.service.ts
└── businesses.routes.ts

apps/web/src/app/(auth)/
├── login/page.tsx
├── register/page.tsx
└── forgot-password/page.tsx
```

---

*Referencia: docs/prd.md - Secao 4*
