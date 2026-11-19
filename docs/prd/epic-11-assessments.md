# Epico 11: Avaliacoes Fisicas

**Prioridade:** Must Have
**Fase:** 2
**Complexidade:** Media

---

## Descricao

Sistema completo de avaliacoes fisicas com antropometria, testes e acompanhamento de evolucao.

---

## User Stories

### US-11.1: Realizar Avaliacao

**Como** um profissional
**Quero** realizar avaliacao fisica completa
**Para** ter baseline do aluno

**Campos da avaliacao:**
- [ ] Peso, altura
- [ ] Circunferencias (9 medidas)
- [ ] Dobras cutaneas (7 dobras - Pollock)
- [ ] Calculo automatico: IMC, % gordura, massa magra
- [ ] Testes de flexibilidade
- [ ] Testes de forca
- [ ] Testes cardio (opcional)
- [ ] Fotos padronizadas

**Criterios de Aceite:**
- [ ] Formulario guiado passo a passo
- [ ] Calculos automaticos
- [ ] Comparacao com avaliacao anterior
- [ ] Geracao de relatorio PDF

---

### US-11.2: Fotos de Progresso

**Como** um aluno
**Quero** registrar fotos de progresso
**Para** ver minha evolucao visual

**Criterios de Aceite:**
- [ ] Captura guiada (frente, lado, costas)
- [ ] Marcacao de data
- [ ] Comparacao lado a lado
- [ ] Slider de antes/depois
- [ ] Privacidade (so aluno e profissional veem)

---

### US-11.3: Acompanhar Evolucao

**Como** um aluno
**Quero** ver minha evolucao ao longo do tempo
**Para** me motivar

**Criterios de Aceite:**
- [ ] Grafico de peso
- [ ] Grafico de % gordura
- [ ] Grafico de medidas
- [ ] Comparativo entre avaliacoes
- [ ] Timeline de fotos

---

## Modelo de Dados

```typescript
interface Assessment {
  id: string;
  studentId: string;
  professionalId: string;
  date: Date;
  type: 'FULL' | 'PARTIAL' | 'QUICK';

  // Medidas basicas
  weight: number;          // kg
  height: number;          // cm
  bmi?: number;            // calculado

  // Circunferencias (cm)
  circumferences?: {
    neck?: number;
    chest?: number;
    waist?: number;
    hip?: number;
    rightArm?: number;
    leftArm?: number;
    rightThigh?: number;
    leftThigh?: number;
    rightCalf?: number;
    leftCalf?: number;
  };

  // Dobras cutaneas (mm) - Pollock 7
  skinfolds?: {
    chest?: number;
    abdominal?: number;
    thigh?: number;
    triceps?: number;
    subscapular?: number;
    suprailiac?: number;
    midaxillary?: number;
  };

  // Calculados
  bodyFatPercentage?: number;
  fatMass?: number;
  leanMass?: number;

  // Testes
  flexibilityTests?: Record<string, number>;
  strengthTests?: Record<string, number>;
  cardioTests?: Record<string, number>;

  // Fotos
  photos?: AssessmentPhoto[];

  notes?: string;
}

interface AssessmentPhoto {
  id: string;
  assessmentId: string;
  type: 'FRONT' | 'SIDE_LEFT' | 'SIDE_RIGHT' | 'BACK';
  url: string;
  uploadedAt: Date;
}
```

---

## Formulas de Calculo

```typescript
// IMC
const bmi = weight / Math.pow(height / 100, 2);

// % Gordura - Pollock 7 Dobras (Homens)
const sumSkinfolds = chest + abdominal + thigh + triceps +
                     subscapular + suprailiac + midaxillary;
const bodyDensity = 1.112 - (0.00043499 * sumSkinfolds) +
                    (0.00000055 * Math.pow(sumSkinfolds, 2)) -
                    (0.00028826 * age);
const bodyFatPercentage = (495 / bodyDensity) - 450;

// Massa Gorda e Magra
const fatMass = weight * (bodyFatPercentage / 100);
const leanMass = weight - fatMass;
```

---

## Dependencias

- Epico 1: Autenticacao e Multi-tenancy
- Epico 2: Gestao de Alunos

---

## Arquivos Relacionados

```
apps/api/src/modules/assessments/
├── assessments.controller.ts
├── assessments.service.ts
├── assessments.routes.ts
├── calculations.ts
└── pdf-generator.ts

apps/web/src/app/(dashboard)/alunos/[id]/avaliacoes/
├── page.tsx              # Lista de avaliacoes
└── nova/page.tsx         # Nova avaliacao

apps/student-app/src/app/(app)/evolucao/
└── page.tsx              # Minha evolucao
```

---

*Referencia: docs/prd.md - Secao 14*
