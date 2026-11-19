# Coding Standards

## FIS360 - Padroes de Codigo

---

## 1. TypeScript

### 1.1 Configuracao Base

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

### 1.2 Convencoes de Nomenclatura

```typescript
// Arquivos: kebab-case
user.service.ts
auth.controller.ts
create-student.schema.ts

// Classes: PascalCase
class UserService {}
class AuthController {}

// Interfaces/Types: PascalCase (sem prefixo I)
interface User {}
type CreateStudentInput = {}

// Funcoes e variaveis: camelCase
const getUserById = () => {}
const isActive = true

// Constantes: UPPER_SNAKE_CASE
const MAX_RETRIES = 3
const API_BASE_URL = '/api'

// Enums: PascalCase com valores PascalCase
enum UserRole {
  Owner = 'OWNER',
  Manager = 'MANAGER',
  Professional = 'PROFESSIONAL',
}
```

### 1.3 Imports

```typescript
// Ordem de imports:
// 1. Node modules
// 2. Externos
// 3. Internos absolutos
// 4. Internos relativos
// 5. Types

import { Router } from 'express';
import { z } from 'zod';

import { prisma } from '@/config/database';
import { logger } from '@/utils/logger';

import { UserService } from './user.service';
import { createUserSchema } from './user.schema';

import type { User, CreateUserInput } from './user.types';
```

---

## 2. Backend (Express/Node)

### 2.1 Estrutura de Modulo

```
modules/
└── users/
    ├── users.controller.ts  # Handlers HTTP
    ├── users.service.ts     # Logica de negocio
    ├── users.routes.ts      # Definicao de rotas
    ├── users.schema.ts      # Validacao Zod
    ├── users.types.ts       # Types/Interfaces
    └── users.test.ts        # Testes
```

### 2.2 Controller Pattern

```typescript
// users.controller.ts
export const usersController = {
  async list(req: Request, res: Response, next: NextFunction) {
    try {
      const { page, limit, search } = req.query;
      const result = await usersService.list({
        page: Number(page) || 1,
        limit: Number(limit) || 20,
        search: String(search || ''),
        businessId: req.businessId,
      });

      res.json({
        success: true,
        data: result.users,
        meta: {
          page: result.page,
          limit: result.limit,
          total: result.total,
          totalPages: result.totalPages,
        },
      });
    } catch (error) {
      next(error);
    }
  },

  async create(req: Request, res: Response, next: NextFunction) {
    try {
      const user = await usersService.create({
        ...req.body,
        businessId: req.businessId,
      });

      res.status(201).json({
        success: true,
        data: user,
      });
    } catch (error) {
      next(error);
    }
  },
};
```

### 2.3 Service Pattern

```typescript
// users.service.ts
export const usersService = {
  async list(params: ListUsersParams): Promise<ListUsersResult> {
    const { page, limit, search, businessId } = params;
    const skip = (page - 1) * limit;

    const where = {
      businessId,
      ...(search && {
        OR: [
          { name: { contains: search, mode: 'insensitive' } },
          { email: { contains: search, mode: 'insensitive' } },
        ],
      }),
    };

    const [users, total] = await Promise.all([
      prisma.user.findMany({ where, skip, take: limit }),
      prisma.user.count({ where }),
    ]);

    return {
      users,
      page,
      limit,
      total,
      totalPages: Math.ceil(total / limit),
    };
  },

  async create(data: CreateUserInput): Promise<User> {
    const hashedPassword = await hashPassword(data.password);

    return prisma.user.create({
      data: {
        ...data,
        passwordHash: hashedPassword,
      },
    });
  },
};
```

### 2.4 Error Handling

```typescript
// Erros customizados
export class AppError extends Error {
  constructor(
    public code: string,
    message: string,
    public statusCode: number = 400,
    public details?: any
  ) {
    super(message);
    this.name = 'AppError';
  }
}

// Uso
throw new AppError('USER_NOT_FOUND', 'Usuario nao encontrado', 404);
throw new AppError('VALIDATION_ERROR', 'Dados invalidos', 400, errors);

// Middleware de erro
export const errorMiddleware = (
  error: Error,
  req: Request,
  res: Response,
  next: NextFunction
) => {
  if (error instanceof AppError) {
    return res.status(error.statusCode).json({
      success: false,
      error: {
        code: error.code,
        message: error.message,
        details: error.details,
      },
    });
  }

  logger.error(error);
  res.status(500).json({
    success: false,
    error: {
      code: 'INTERNAL_ERROR',
      message: 'Erro interno do servidor',
    },
  });
};
```

---

## 3. Frontend (Next.js/React)

### 3.1 Estrutura de Componentes

```
components/
├── ui/                    # Componentes base (shadcn)
│   ├── button.tsx
│   ├── input.tsx
│   └── card.tsx
├── forms/                 # Componentes de formulario
│   ├── student-form.tsx
│   └── workout-form.tsx
├── tables/                # Componentes de tabela
│   └── students-table.tsx
└── layout/                # Componentes de layout
    ├── sidebar.tsx
    └── header.tsx
```

### 3.2 Component Pattern

```tsx
// Componente funcional com types
interface StudentCardProps {
  student: Student;
  onEdit?: (id: string) => void;
  className?: string;
}

export function StudentCard({ student, onEdit, className }: StudentCardProps) {
  return (
    <Card className={cn('p-4', className)}>
      <div className="flex items-center gap-4">
        <Avatar>
          <AvatarImage src={student.avatarUrl} />
          <AvatarFallback>{getInitials(student.name)}</AvatarFallback>
        </Avatar>
        <div>
          <h3 className="font-medium">{student.name}</h3>
          <p className="text-sm text-muted-foreground">{student.email}</p>
        </div>
        {onEdit && (
          <Button variant="ghost" onClick={() => onEdit(student.id)}>
            Editar
          </Button>
        )}
      </div>
    </Card>
  );
}
```

### 3.3 React Query Hooks

```typescript
// hooks/use-students.ts
export function useStudents(params?: ListStudentsParams) {
  return useQuery({
    queryKey: ['students', params],
    queryFn: () => api.students.list(params),
  });
}

export function useStudent(id: string) {
  return useQuery({
    queryKey: ['students', id],
    queryFn: () => api.students.get(id),
    enabled: !!id,
  });
}

export function useCreateStudent() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: api.students.create,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['students'] });
      toast.success('Aluno criado com sucesso!');
    },
    onError: (error: AppError) => {
      toast.error(error.message);
    },
  });
}
```

### 3.4 Forms com React Hook Form

```tsx
// forms/student-form.tsx
const studentFormSchema = z.object({
  name: z.string().min(2, 'Nome deve ter pelo menos 2 caracteres'),
  email: z.string().email('Email invalido'),
  phone: z.string().regex(/^\d{10,11}$/, 'Telefone invalido'),
  goals: z.array(z.nativeEnum(GoalType)).min(1, 'Selecione pelo menos um objetivo'),
});

type StudentFormData = z.infer<typeof studentFormSchema>;

export function StudentForm({ onSubmit, defaultValues }: StudentFormProps) {
  const form = useForm<StudentFormData>({
    resolver: zodResolver(studentFormSchema),
    defaultValues,
  });

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField
          control={form.control}
          name="name"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Nome</FormLabel>
              <FormControl>
                <Input {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />
        {/* ... outros campos */}
        <Button type="submit">Salvar</Button>
      </form>
    </Form>
  );
}
```

---

## 4. Testes

### 4.1 Estrutura de Testes

```typescript
// Backend - Vitest
describe('UsersService', () => {
  beforeEach(() => {
    // Setup
  });

  afterEach(() => {
    // Cleanup
  });

  describe('create', () => {
    it('should create a user with hashed password', async () => {
      const input = {
        email: 'test@example.com',
        password: 'password123',
        name: 'Test User',
      };

      const user = await usersService.create(input);

      expect(user.email).toBe(input.email);
      expect(user.passwordHash).not.toBe(input.password);
      expect(await verifyPassword(input.password, user.passwordHash)).toBe(true);
    });

    it('should throw on duplicate email', async () => {
      // ...
    });
  });
});
```

### 4.2 Mocks

```typescript
// __mocks__/prisma.ts
import { mockDeep, DeepMockProxy } from 'vitest-mock-extended';
import { PrismaClient } from '@prisma/client';

export const prismaMock = mockDeep<PrismaClient>();

vi.mock('@/config/database', () => ({
  prisma: prismaMock,
}));
```

---

## 5. Git

### 5.1 Commits (Conventional Commits)

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:**
- `feat`: Nova feature
- `fix`: Bug fix
- `docs`: Documentacao
- `style`: Formatacao
- `refactor`: Refatoracao
- `test`: Testes
- `chore`: Manutencao

**Exemplos:**
```
feat(students): add bulk import functionality
fix(auth): resolve token refresh race condition
docs(api): update endpoint documentation
refactor(workouts): extract exercise validation logic
```

### 5.2 Branches

```
main              # Producao
develop           # Desenvolvimento
feature/xxx       # Features
fix/xxx          # Bug fixes
release/x.x.x    # Releases
```

---

## 6. Linting e Formatacao

### 6.1 ESLint Config

```javascript
// .eslintrc.js
module.exports = {
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'prettier',
  ],
  rules: {
    '@typescript-eslint/no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
    '@typescript-eslint/explicit-function-return-type': 'off',
    'react/prop-types': 'off',
    'react/react-in-jsx-scope': 'off',
  },
};
```

### 6.2 Prettier Config

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100
}
```

---

*Documento gerado em 06/01/2026*
