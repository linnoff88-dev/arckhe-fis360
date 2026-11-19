# Story 002: Registro de Negocio

**Epic:** E1 - Autenticacao e Multi-tenancy
**Status:** Draft
**Prioridade:** Must Have
**Estimativa:** -
**Depende de:** Story 001

---

## Descricao

**Como** um profissional fitness
**Quero** criar uma conta para meu negocio
**Para** comecar a usar a plataforma

---

## Criterios de Aceite

### 1. API - Endpoint de Registro
- [ ] POST /api/auth/register aceita: name, email, password, businessName, businessType
- [ ] Validar email formato valido
- [ ] Validar senha minimo 8 caracteres
- [ ] Validar email unico (retornar erro se ja existe)
- [ ] Criar Business com slug unico gerado automaticamente
- [ ] Criar User com role BUSINESS_OWNER
- [ ] Hash da senha com bcrypt (cost 12)
- [ ] Retornar access_token e refresh_token
- [ ] Retornar dados do usuario (sem senha)

### 2. Frontend - Pagina de Registro
- [ ] Criar pagina /register com formulario
- [ ] Campos: nome, email, senha, nome do negocio, tipo de negocio
- [ ] Validacao em tempo real dos campos
- [ ] Exibir mensagens de erro
- [ ] Loading state durante submit
- [ ] Redirect para dashboard apos sucesso
- [ ] Link para login

### 3. Validacoes
- [ ] Nome: minimo 2 caracteres
- [ ] Email: formato valido
- [ ] Senha: minimo 8 caracteres
- [ ] Nome do negocio: minimo 2 caracteres
- [ ] Tipo do negocio: valor valido do enum

### 4. Slug Generation
- [ ] Gerar slug a partir do nome do negocio
- [ ] Remover acentos e caracteres especiais
- [ ] Converter para lowercase
- [ ] Substituir espacos por hifens
- [ ] Adicionar sufixo numerico se slug ja existe

---

## Tarefas Tecnicas

### 1. Schema Prisma (atualizar)

```prisma
model Business {
  id        String   @id @default(cuid())
  name      String
  slug      String   @unique
  type      BusinessType

  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  users     User[]
}

model User {
  id           String   @id @default(cuid())
  businessId   String
  email        String
  passwordHash String
  role         UserRole
  name         String?

  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt

  business     Business @relation(fields: [businessId], references: [id])

  @@unique([businessId, email])
}

enum BusinessType {
  GYM
  PERSONAL_STUDIO
  PHYSIO_CLINIC
  CROSSFIT_BOX
  PILATES_STUDIO
  ONLINE_ONLY
  HYBRID
}

enum UserRole {
  BUSINESS_OWNER
  MANAGER
  PROFESSIONAL
  RECEPTIONIST
  STUDENT
}
```

### 2. API - Auth Module

```typescript
// src/modules/auth/auth.schema.ts
import { z } from 'zod';

export const registerSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
  password: z.string().min(8),
  businessName: z.string().min(2),
  businessType: z.nativeEnum(BusinessType),
});

// src/modules/auth/auth.service.ts
export async function register(data: RegisterInput) {
  // 1. Check if email exists
  // 2. Generate slug
  // 3. Create business
  // 4. Hash password
  // 5. Create user
  // 6. Generate tokens
  // 7. Return user + tokens
}

// src/modules/auth/auth.controller.ts
export async function registerHandler(req, res, next) {
  const data = registerSchema.parse(req.body);
  const result = await register(data);
  res.status(201).json({ success: true, data: result });
}
```

### 3. Frontend - Register Page

```typescript
// src/app/(auth)/register/page.tsx
'use client';

import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { useMutation } from '@tanstack/react-query';

export default function RegisterPage() {
  const form = useForm({
    resolver: zodResolver(registerSchema),
  });

  const mutation = useMutation({
    mutationFn: (data) => api.auth.register(data),
    onSuccess: () => router.push('/'),
  });

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(mutation.mutate)}>
        {/* Campos do formulario */}
      </form>
    </Form>
  );
}
```

---

## Arquivos a Criar/Modificar

### API
```
apps/api/src/
├── modules/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.routes.ts
│   │   ├── auth.schema.ts
│   │   └── auth.types.ts
│   └── businesses/
│       └── businesses.service.ts (generateSlug)
├── utils/
│   ├── password.ts (hashPassword)
│   └── jwt.ts (generateTokens)
└── routes.ts (adicionar auth routes)
```

### Web
```
apps/web/src/
├── app/
│   └── (auth)/
│       ├── layout.tsx
│       └── register/
│           └── page.tsx
├── lib/
│   └── api.ts (api.auth.register)
└── components/
    └── forms/
        └── register-form.tsx
```

---

## Testes

### API
- [ ] Registro com dados validos cria business e user
- [ ] Registro com email duplicado retorna erro 409
- [ ] Registro com senha fraca retorna erro 400
- [ ] Slug e gerado corretamente
- [ ] Slug com duplicata recebe sufixo numerico
- [ ] Token JWT e valido e contem dados corretos

### Frontend
- [ ] Formulario valida campos obrigatorios
- [ ] Formulario exibe erros de validacao
- [ ] Submit com sucesso redireciona para dashboard
- [ ] Submit com erro exibe mensagem

---

## API Response

### Sucesso (201)

```json
{
  "success": true,
  "data": {
    "user": {
      "id": "clx123...",
      "email": "rafaela@example.com",
      "name": "Rafaela Silva",
      "role": "BUSINESS_OWNER"
    },
    "business": {
      "id": "clx456...",
      "name": "Rafaela Personal",
      "slug": "rafaela-personal",
      "type": "PERSONAL_STUDIO"
    },
    "accessToken": "eyJ...",
    "refreshToken": "eyJ..."
  }
}
```

### Erro - Email Duplicado (409)

```json
{
  "success": false,
  "error": {
    "code": "CONFLICT",
    "message": "Email ja cadastrado"
  }
}
```

### Erro - Validacao (400)

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados invalidos",
    "details": [
      { "field": "password", "message": "Senha deve ter no minimo 8 caracteres" }
    ]
  }
}
```

---

## Referencias

- [epic-1-auth.md](../prd/epic-1-auth.md) - US-1.1
- [api-design.md](../architecture/api-design.md)
- [database.md](../architecture/database.md)

---

*Story criada em 06/01/2026*
