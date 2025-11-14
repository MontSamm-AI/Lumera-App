# DIVISÃO ESTRATÉGICA EM CHATS - PROJETO LUMERA APP

> **Estratégia:** Dividir o desenvolvimento em 5 chats sequenciais, cada um focando em um aspecto específico do projeto, mas sempre mantendo o contexto completo do branding, DNA e objetivos da Lumera.

---

## 📋 CONTEXTO COMPARTILHADO (TODOS OS CHATS)

**Antes de iniciar QUALQUER chat, sempre inclua este contexto base:**

```markdown
# CONTEXTO LUMERA - PROJETO COMPLETO

## Marca e Posicionamento
- **Marca:** LUMERA (latim: lumen = luz + era = novo tempo)
- **Tagline:** "Da Estagnação à Estratégia"
- **Missão:** Guiar empreendedoras a transformarem estagnação em estratégia
- **Cliente:** Nathalia Mazetto - Mentora de Propósito & Consultora Estratégica

## Paleta de Cores
- **Emerald Green** #284138 (autoridade, crescimento)
- **Wasabi** #80907B (serenidade, sofisticação)
- **Creased Khari** #F8D794 (luz, clareza)
- **Egyptian Earth** #BB6830 (calor, ação)
- **Noir de Vigne** #111410 (elegância, premium)

## Stack Técnico
- Next.js 14+ (App Router) + TypeScript
- Tailwind CSS (customizado com paleta Lumera)
- Google AI (Gemini Pro) para diagnósticos
- Supabase (Database + Auth) ou Firebase
- Vercel (deploy - já configurado)
- Resend (emails transacionais)

## Objetivo do Projeto
Criar ecossistema digital premium que:
1. Automatize funil de captação (quiz diagnóstico)
2. Gere diagnósticos personalizados com IA
3. Escale método LUMERA sem perder essência
4. Posicione Nathalia como autoridade digital inovadora

## Princípios de Design
- Clareza > Complexidade
- Elegância Minimalista
- Calor Humano + Autoridade
- Espaços em branco generosos
- Animações sutis (nunca chamativas)
- Mobile-first e acessível (WCAG AA)

## Documentos de Referência
- `SYSTEM-PROMPT-PRINCIPAL.md` (especificações técnicas completas)
- `DOCUMENTACAO-COMPLETA-DNA-BRANDING.md` (essência da marca)
- `ENGENHARIA-REVERSA-QUIZ.md` (estrutura do funil)
- `RELATORIO-ANALISE-COMPLETA.md` (visão estratégica)
```

---

## 🎯 CHAT 1: FUNDAÇÃO E DESIGN SYSTEM

### Objetivo
Criar a estrutura base do projeto Next.js, implementar o Design System Lumera completo e componentes UI fundamentais.

### Escopo

#### 1.1 Setup do Projeto
```bash
# Criar projeto Next.js com configurações
npx create-next-app@latest lumera-app --typescript --tailwind --app --src-dir=false

# Estrutura de pastas completa
# Configuração do TypeScript (strict)
# Configuração do Tailwind com paleta Lumera
# Setup do ESLint e Prettier
```

#### 1.2 Design System Lumera

**Arquivos a criar:**

`tailwind.config.ts`
```typescript
// Implementar TODA a paleta de cores Lumera
// Configurar tipografia (Cormorant Garamond + Inter)
// Espaçamentos customizados
// Border radius e shadows
// Animações e transições
```

`styles/globals.css`
```css
// Imports de fontes (Google Fonts)
// Reset CSS customizado
// Classes utilitárias Lumera
// Scrollbar customizada
// Seleção de texto (::selection)
```

#### 1.3 Componentes UI Base

Criar em `components/ui/`:

**Button.tsx**
- Variantes: primary, secondary, outline, ghost
- Tamanhos: sm, md, lg
- Estados: default, hover, active, disabled, loading
- Cores baseadas na paleta Lumera

**Input.tsx**
- Text, email, phone, textarea
- Validação visual
- Estados de erro e sucesso
- Label e helper text
- Acessibilidade completa

**Card.tsx**
- Container padrão com bordas suaves
- Variantes de background (branco, wasabi, emerald)
- Padding consistente
- Sombras elegantes

**Typography.tsx**
- Heading (h1 - h6)
- Paragraph
- Label
- Caption
- Aplicação correta das fontes

**Container.tsx**
- Max-width responsivo
- Padding lateral
- Centralização

**Badge.tsx**
- Status badges
- Tags de categoria
- Cores da paleta

#### 1.4 Layout Base

**`app/layout.tsx`**
- HTML lang="pt-BR"
- Metadata (SEO base)
- Fontes carregadas
- Analytics setup (placeholder)
- Theme provider se necessário

**`components/layout/Header.tsx`**
- Logo Lumera
- Navegação principal
- Mobile menu (hamburguer)
- CTA "Fazer Quiz"
- Sticky header com blur background

**`components/layout/Footer.tsx`**
- Links úteis
- Redes sociais
- Copyright
- Política de privacidade

### Prompt para Chat 1

```markdown
# CHAT 1: FUNDAÇÃO E DESIGN SYSTEM LUMERA

[INCLUIR TODO O CONTEXTO COMPARTILHADO ACIMA]

## Tarefa
Criar a fundação completa do projeto Lumera App com Design System implementado.

## Entregáveis
1. Projeto Next.js 14+ configurado com TypeScript strict
2. Tailwind configurado com TODA a paleta de cores Lumera
3. Fontes (Cormorant Garamond + Inter) carregadas
4. Componentes UI base funcionais e documentados:
   - Button (todas as variantes)
   - Input (todos os tipos)
   - Card
   - Typography
   - Container
   - Badge
5. Layout base (Header + Footer) responsivo
6. Página inicial temporária (hello world branded)

## Critérios de Sucesso
- ✅ Projeto roda sem erros (npm run dev)
- ✅ Paleta Lumera 100% implementada
- ✅ Componentes reutilizáveis e tipados
- ✅ Mobile responsivo
- ✅ Código limpo e comentado
- ✅ README com instruções de setup

## Referências Importantes
- Paleta: ver DOCUMENTACAO-COMPLETA-DNA-BRANDING.md
- Especificações técnicas: ver SYSTEM-PROMPT-PRINCIPAL.md seção "Design System Lumera"

## Stack
- Next.js 14.2+
- TypeScript 5+
- Tailwind CSS 3.4+
- Lucide React (ícones)

Por favor, implemente tudo isso de forma meticulosa, seguindo os princípios de design Lumera: clareza, elegância minimalista e atenção aos detalhes.
```

### Tempo Estimado
6-8 horas de desenvolvimento

---

## 🎨 CHAT 2: LANDING PAGE PREMIUM

### Objetivo
Criar a landing page completa da Lumera com todas as seções, conteúdo e experiência premium.

### Escopo

#### 2.1 Estrutura da Landing Page

**`app/page.tsx`** - Seções:

1. **Hero Section**
   - Headline impactante
   - Subheadline (manifesto)
   - CTA principal (Fazer Quiz)
   - Imagem/ilustração elegante
   - Animação de entrada suave

2. **Sobre Nathalia & Lumera**
   - Foto profissional
   - História e credenciais
   - Método LUMERA explicado
   - Valores e missão

3. **Método LUMERA**
   - Card para cada letra (L-U-M-E-R-A)
   - Ícones elegantes
   - Descrição de cada pilar
   - Layout em grid responsivo

4. **Serviços**
   - Mentoria de Propósito
     - Descrição completa
     - Formato e duração
     - Investimento
     - Para quem é
     - CTA "Saber mais"
   - Consultoria Criativa
     - Descrição completa
     - Formato e duração
     - Investimento
     - Para quem é
     - CTA "Saber mais"

5. **Depoimentos / Transformações**
   - Carrossel ou grid
   - Foto + nome + resultado
   - Design branded

6. **Como Funciona**
   - Passo a passo da jornada
   - Timeline visual
   - Do quiz ao resultado

7. **FAQ**
   - Accordion elegante
   - 8-10 perguntas comuns
   - Respostas claras

8. **CTA Final**
   - Seção dedicada
   - Headline persuasiva
   - Botão de ação
   - Garantia ou social proof

#### 2.2 Componentes Específicos

Criar em `components/marketing/`:

**Hero.tsx**
- Versão desktop e mobile
- Animações Framer Motion
- Gradientes sutis

**ServiceCard.tsx**
- Card de serviço reutilizável
- Hover effects elegantes
- Estrutura clara de informação

**TestimonialCarousel.tsx**
- Carousel com autoplay suave
- Indicadores de navegação
- Touch-friendly

**MethodPillar.tsx**
- Card para cada pilar LUMERA
- Ícone + título + descrição
- Hover state revelando mais info

**FAQAccordion.tsx**
- Accordion acessível
- Animação de abertura suave
- Ícone de +/-

**CTASection.tsx**
- Seção de call-to-action reutilizável
- Variantes de design
- Botões proeminentes

#### 2.3 Conteúdo e Copywriting

**Usar como base:**
- DNA NATHALIA MAZETTO.md (descrições de serviços)
- DOCUMENTACAO-COMPLETA-DNA-BRANDING.md (tom de voz)

**Tom de voz:**
- Inspirador sem ser piegas
- Sábio sem ser pedante
- Estratégico e prático
- Premium e sofisticado

#### 2.4 Animações e Interatividade

**Framer Motion:**
```bash
npm install framer-motion
```

- Fade in ao scroll
- Stagger animations para listas
- Parallax sutil
- Hover states elegantes
- Transições de página

### Prompt para Chat 2

```markdown
# CHAT 2: LANDING PAGE PREMIUM LUMERA

[INCLUIR TODO O CONTEXTO COMPARTILHADO]

## Situação Atual
O Chat 1 entregou a fundação do projeto com Design System completo e componentes UI base funcionando.

## Tarefa
Criar a landing page completa da Lumera com todas as seções, conteúdo premium e experiência impecável.

## Entregáveis
1. Página inicial (`app/page.tsx`) com todas as 8 seções:
   - Hero premium com CTA claro
   - Sobre Nathalia e método LUMERA
   - Método LUMERA detalhado (6 pilares)
   - Serviços (Mentoria + Consultoria)
   - Depoimentos/transformações
   - Como funciona (jornada)
   - FAQ (8-10 perguntas)
   - CTA final forte

2. Componentes de marketing reutilizáveis:
   - Hero.tsx
   - ServiceCard.tsx
   - TestimonialCarousel.tsx
   - MethodPillar.tsx
   - FAQAccordion.tsx
   - CTASection.tsx

3. Animações sutis (Framer Motion)
4. Mobile 100% responsivo
5. Performance otimizada (lazy loading, code splitting)

## Critérios de Sucesso
- ✅ Design 100% alinhado com paleta e branding Lumera
- ✅ Conteúdo completo e persuasivo
- ✅ Animações sutis e elegantes
- ✅ Mobile perfeito
- ✅ Lighthouse Performance 90+
- ✅ Acessibilidade WCAG AA
- ✅ Todos os CTAs apontam para /quiz (ainda não criado)

## Conteúdo de Referência
Use os textos de:
- DNA NATHALIA MAZETTO.md (serviços, valores, missão)
- DOCUMENTACAO-COMPLETA-DNA-BRANDING.md (tom de voz, posicionamento)

## Stack Adicional
- Framer Motion para animações
- Lucide React para ícones
- next/image para imagens otimizadas

Por favor, crie uma landing page que transmita sofisticação, clareza e autoridade. Cada seção deve respirar o branding Lumera.
```

### Tempo Estimado
10-12 horas de desenvolvimento

---

## 📝 CHAT 3: QUIZ DIAGNÓSTICO INTELIGENTE

### Objetivo
Criar o quiz multi-step completo, integrado com banco de dados e sistema de validação.

### Escopo

#### 3.1 Estrutura do Quiz

**`app/quiz/page.tsx`**
- Container principal do quiz
- Gerenciamento de estado (useState ou Zustand)
- Navegação entre perguntas
- Validação e salvamento

**`app/quiz/obrigado/page.tsx`**
- Página de confirmação
- Mensagem de sucesso
- Expectativa de recebimento do diagnóstico
- Social proof

#### 3.2 Componentes do Quiz

Criar em `components/quiz/`:

**QuizContainer.tsx**
- Wrapper principal
- Controle de fluxo
- Persistência (localStorage)

**QuizProgress.tsx**
- Barra de progresso visual
- Indicador de etapa (1/12)
- Design elegante

**QuestionCard.tsx**
- Card para cada pergunta
- Transição suave entre perguntas
- Animação de entrada/saída

**QuestionTypes/**
- `TextQuestion.tsx` (nome)
- `EmailQuestion.tsx` (validação específica)
- `PhoneQuestion.tsx` (máscara BR)
- `SelectQuestion.tsx` (dropdown elegante)
- `TextareaQuestion.tsx` (respostas longas)

**QuizNavigation.tsx**
- Botões Voltar / Próximo
- Disabled states
- Validação antes de avançar

#### 3.3 Validação com Zod

**`lib/validators.ts`**
```typescript
import { z } from 'zod'

export const quizSchema = z.object({
  nome: z.string().min(2, 'Nome muito curto'),
  instagram: z.string().regex(/^@?[a-zA-Z0-9._]+$/, 'Instagram inválido'),
  whatsapp: z.string().regex(/^\+?55?\s?\(?\d{2}\)?\s?\d{4,5}-?\d{4}$/, 'WhatsApp inválido'),
  email: z.string().email('Email inválido'),
  tipoNegocio: z.enum(['Serviços', 'Produtos Físicos', 'Infoprodutos']),
  modeloNegocio: z.string().min(20, 'Descreva melhor seu modelo'),
  faturamento: z.string(),
  metas: z.string().min(20, 'Descreva suas metas'),
  bloqueios: z.string().min(20, 'Descreva os bloqueios'),
  nivelConsciencia: z.string(),
  resultadoDesejado: z.string().min(20, 'Descreva o resultado'),
})

export type QuizData = z.infer<typeof quizSchema>
```

#### 3.4 Perguntas Exatas (da engenharia reversa)

1. Qual é o seu nome?
2. Deixe aqui o @ do seu instagram
3. Qual é o seu whatsapp?
4. Qual é o seu e-mail?
5. Com o que você trabalha? [Select: Serviços | Produtos Físicos | Infoprodutos]
6. Descreva como é o seu modelo de negócio atual, o que você vende e como:
7. Qual seu faturamento mensal, em média? [Select: 6 opções]
8. Quais são suas metas com o seu negócio hoje?
9. O que você acredita que te impede de realizar suas metas hoje?
10. Em qual situação você se identifica mais? [Select: 3 opções]
11. Qual resultado você almeja alcançar para o seu negócio?
12. Obrigado por participar! [Página de confirmação]

#### 3.5 Integração com Banco de Dados

**Setup Supabase:**
```sql
CREATE TABLE quiz_responses (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  created_at TIMESTAMP DEFAULT NOW(),
  nome TEXT NOT NULL,
  instagram TEXT,
  whatsapp TEXT,
  email TEXT UNIQUE NOT NULL,
  tipo_negocio TEXT,
  modelo_negocio TEXT,
  faturamento TEXT,
  metas TEXT,
  bloqueios TEXT,
  nivel_consciencia TEXT,
  resultado_desejado TEXT,
  status TEXT DEFAULT 'pending',
  diagnosis_generated BOOLEAN DEFAULT FALSE
)
```

**`lib/db/supabase.ts`**
```typescript
import { createClient } from '@supabase/supabase-js'

export const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
)
```

**`lib/db/queries.ts`**
```typescript
export async function saveQuizResponse(data: QuizData) {
  const { data: response, error } = await supabase
    .from('quiz_responses')
    .insert([data])
    .select()
    .single()

  if (error) throw error
  return response
}
```

#### 3.6 API Route para Submissão

**`app/api/quiz/route.ts`**
```typescript
import { NextResponse } from 'next/server'
import { quizSchema } from '@/lib/validators'
import { saveQuizResponse } from '@/lib/db/queries'

export async function POST(req: Request) {
  try {
    const body = await req.json()

    // Validar dados
    const validatedData = quizSchema.parse(body)

    // Salvar no banco
    const response = await saveQuizResponse(validatedData)

    // Trigger geração de diagnóstico (async)
    // (será implementado no Chat 4)

    return NextResponse.json({ success: true, id: response.id })
  } catch (error) {
    return NextResponse.json(
      { error: error.message },
      { status: 400 }
    )
  }
}
```

#### 3.7 UX e Animações

- Transição suave entre perguntas (Framer Motion)
- Validação em tempo real (com debounce)
- Loading state durante submissão
- Confetti ou animação de sucesso ao completar
- Salvamento automático em localStorage
- Possibilidade de voltar e editar

### Prompt para Chat 3

```markdown
# CHAT 3: QUIZ DIAGNÓSTICO INTELIGENTE

[INCLUIR TODO O CONTEXTO COMPARTILHADO]

## Situação Atual
Chats 1 e 2 entregaram:
- Design System Lumera completo
- Componentes UI base
- Landing page premium funcional

## Tarefa
Criar o quiz diagnóstico multi-step completo com as 11 perguntas, validação, persistência e integração com banco de dados.

## Entregáveis
1. Página do quiz (`app/quiz/page.tsx`) multi-step
2. Página de confirmação (`app/quiz/obrigado/page.tsx`)
3. Componentes do quiz:
   - QuizContainer
   - QuizProgress (barra elegante)
   - QuestionCard
   - QuestionTypes (text, email, phone, select, textarea)
   - QuizNavigation

4. Validação completa (Zod)
5. Integração com Supabase:
   - Schema do banco criado
   - Cliente configurado
   - Queries implementadas

6. API Route para submissão
7. UX premium:
   - Animações suaves
   - Validação em tempo real
   - Loading states
   - Salvamento automático (localStorage)
   - Possibilidade de voltar

## Perguntas Exatas do Quiz
(Ver ENGENHARIA-REVERSA-QUIZ.md para lista completa)

1. Nome (text)
2. Instagram (text com @)
3. WhatsApp (phone com máscara BR)
4. Email (email validation)
5. Tipo de negócio (select: 3 opções)
6. Modelo de negócio (textarea)
7. Faturamento mensal (select: 6 faixas)
8. Metas (textarea)
9. Bloqueios (textarea)
10. Nível de consciência (select: 3 opções)
11. Resultado desejado (textarea)
12. Confirmação (redirect para /quiz/obrigado)

## Critérios de Sucesso
- ✅ Quiz funcional em mobile e desktop
- ✅ Validação robusta (Zod)
- ✅ Dados salvos corretamente no Supabase
- ✅ UX fluida e elegante
- ✅ Design 100% Lumera
- ✅ Acessível (navegação por teclado)
- ✅ Performance otimizada

## Stack Adicional
- Zod para validação
- Supabase para banco de dados
- React Hook Form (opcional, para facilitar)
- Framer Motion para transições

Por favor, crie um quiz que seja ao mesmo tempo funcional, elegante e que transmita profissionalismo. A experiência deve ser suave e acolhedora.
```

### Tempo Estimado
12-14 horas de desenvolvimento

---

## 🤖 CHAT 4: MOTOR DE IA - GERADOR DE DIAGNÓSTICOS

### Objetivo
Implementar o sistema de IA que analisa respostas do quiz e gera diagnósticos personalizados usando Google AI (Gemini).

### Escopo

#### 4.1 Setup Google AI

```bash
npm install @google/generative-ai
```

**`.env.local`**
```
GOOGLE_AI_API_KEY=your_api_key_here
```

**`lib/ai/gemini.ts`**
```typescript
import { GoogleGenerativeAI } from '@google/generative-ai'

const genAI = new GoogleGenerativeAI(process.env.GOOGLE_AI_API_KEY!)

export const geminiModel = genAI.getGenerativeModel({
  model: 'gemini-1.5-pro',
})
```

#### 4.2 Prompt Estruturado

**`lib/ai/prompts/diagnosis.ts`**

Implementar o prompt COMPLETO conforme especificado em `SYSTEM-PROMPT-PRINCIPAL.md` seção "Motor de IA - Gerador de Diagnósticos".

```typescript
export function buildDiagnosisPrompt(quizData: QuizData): string {
  return `
# CONTEXTO
Você é Nathalia Mazetto, mentora de propósito e consultora estratégica...
[PROMPT COMPLETO DO SYSTEM-PROMPT-PRINCIPAL.md]

# DADOS DA CLIENTE
- Nome: ${quizData.nome}
- Negócio: ${quizData.tipoNegocio}
...

# ESTRUTURA OBRIGATÓRIA DO DIAGNÓSTICO
[TEMPLATE COMPLETO]
`
}
```

#### 4.3 API Route de Geração

**`app/api/generate-diagnosis/route.ts`**
```typescript
import { NextResponse } from 'next/server'
import { geminiModel } from '@/lib/ai/gemini'
import { buildDiagnosisPrompt } from '@/lib/ai/prompts/diagnosis'
import { getQuizResponse, updateDiagnosis } from '@/lib/db/queries'

export async function POST(req: Request) {
  try {
    const { quizId } = await req.json()

    // Buscar respostas do quiz
    const quizData = await getQuizResponse(quizId)

    // Construir prompt
    const prompt = buildDiagnosisPrompt(quizData)

    // Gerar diagnóstico com IA
    const result = await geminiModel.generateContent(prompt)
    const diagnosis = result.response.text()

    // Salvar diagnóstico no banco
    await updateDiagnosis(quizId, diagnosis)

    // Enviar email (trigger)
    await fetch('/api/send-email', {
      method: 'POST',
      body: JSON.stringify({ quizId, diagnosis }),
    })

    return NextResponse.json({ success: true, diagnosis })
  } catch (error) {
    console.error('Error generating diagnosis:', error)
    return NextResponse.json(
      { error: 'Failed to generate diagnosis' },
      { status: 500 }
    )
  }
}
```

#### 4.4 Atualização do Schema do Banco

```sql
ALTER TABLE quiz_responses
ADD COLUMN diagnosis TEXT,
ADD COLUMN diagnosis_generated_at TIMESTAMP;
```

**`lib/db/queries.ts`** (adicionar)
```typescript
export async function updateDiagnosis(quizId: string, diagnosis: string) {
  const { error } = await supabase
    .from('quiz_responses')
    .update({
      diagnosis,
      diagnosis_generated: true,
      diagnosis_generated_at: new Date().toISOString(),
    })
    .eq('id', quizId)

  if (error) throw error
}

export async function getQuizResponse(quizId: string) {
  const { data, error } = await supabase
    .from('quiz_responses')
    .select('*')
    .eq('id', quizId)
    .single()

  if (error) throw error
  return data
}
```

#### 4.5 Trigger Automático

**Atualizar `app/api/quiz/route.ts`**
```typescript
// Após salvar no banco
const response = await saveQuizResponse(validatedData)

// Trigger geração de diagnóstico (async - não bloquear resposta)
fetch(`${process.env.NEXT_PUBLIC_APP_URL}/api/generate-diagnosis`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ quizId: response.id }),
}).catch(console.error)
```

#### 4.6 Qualidade e Testes

**`lib/ai/test-diagnosis.ts`**
```typescript
// Script de teste para validar qualidade dos diagnósticos
import { buildDiagnosisPrompt } from './prompts/diagnosis'
import { geminiModel } from './gemini'

const testData = {
  nome: 'Maria Silva',
  tipoNegocio: 'Serviços',
  // ... dados de teste
}

async function testDiagnosis() {
  const prompt = buildDiagnosisPrompt(testData)
  const result = await geminiModel.generateContent(prompt)
  console.log(result.response.text())
}

testDiagnosis()
```

**Critérios de Qualidade:**
- Diagnóstico entre 800-1200 palavras
- Tom de voz consistente com Nathalia
- Personalização real (não genérico)
- Método LUMERA aplicado corretamente
- Formatação Markdown limpa

#### 4.7 Sistema de Validação

**`lib/ai/validate-diagnosis.ts`**
```typescript
export function validateDiagnosis(diagnosis: string): {
  valid: boolean
  issues: string[]
} {
  const issues: string[] = []

  // Verificar tamanho
  const wordCount = diagnosis.split(/\s+/).length
  if (wordCount < 800 || wordCount > 1500) {
    issues.push(`Word count: ${wordCount} (esperado: 800-1200)`)
  }

  // Verificar seções obrigatórias
  const requiredSections = [
    'DIAGNÓSTICO GERAL',
    'PONTOS DE BLOQUEIO',
    'CRENÇAS E PADRÕES',
    'MAPA DE CLAREZA LUMERA',
    'RESULTADO ESPERADO',
  ]

  requiredSections.forEach(section => {
    if (!diagnosis.includes(section)) {
      issues.push(`Seção ausente: ${section}`)
    }
  })

  // Verificar método LUMERA completo
  const lumeraLetters = ['L -', 'U -', 'M -', 'E -', 'R -', 'A -']
  lumeraLetters.forEach(letter => {
    if (!diagnosis.includes(letter)) {
      issues.push(`Falta pilar LUMERA: ${letter}`)
    }
  })

  return {
    valid: issues.length === 0,
    issues,
  }
}
```

### Prompt para Chat 4

```markdown
# CHAT 4: MOTOR DE IA - GERADOR DE DIAGNÓSTICOS

[INCLUIR TODO O CONTEXTO COMPARTILHADO]

## Situação Atual
Chats anteriores entregaram:
- Design System e componentes UI
- Landing page completa
- Quiz funcional salvando no Supabase

## Tarefa
Implementar o sistema de IA que gera diagnósticos personalizados baseados nas respostas do quiz.

## Entregáveis
1. Integração com Google AI (Gemini Pro 1.5):
   - Cliente configurado
   - API Key configurada

2. Sistema de Prompts:
   - `lib/ai/prompts/diagnosis.ts` com prompt COMPLETO
   - Personalização baseada nos dados do quiz
   - Template do diagnóstico estruturado

3. API Route de geração:
   - `/api/generate-diagnosis` funcional
   - Busca dados do quiz
   - Gera diagnóstico com IA
   - Salva no banco
   - Trigger de email (placeholder por enquanto)

4. Atualização do banco de dados:
   - Coluna `diagnosis` adicionada
   - Coluna `diagnosis_generated_at`
   - Queries atualizadas

5. Sistema de validação de qualidade:
   - Validação de tamanho (800-1200 palavras)
   - Validação de seções obrigatórias
   - Validação do método LUMERA completo

6. Trigger automático:
   - Após submissão do quiz, gera diagnóstico automaticamente

7. Script de testes:
   - Testar geração com dados fictícios
   - Validar qualidade do output

## Especificações do Prompt
Ver SYSTEM-PROMPT-PRINCIPAL.md seção "Motor de IA - Gerador de Diagnósticos" para:
- Contexto completo que a IA deve ter
- Tom de voz exato de Nathalia
- Estrutura obrigatória do diagnóstico
- Template do método LUMERA
- Instruções de geração

## Critérios de Sucesso
- ✅ Diagnósticos gerados automaticamente após quiz
- ✅ Qualidade alta (personalização real, não genérico)
- ✅ Tom de voz consistente com Nathalia
- ✅ Método LUMERA aplicado corretamente
- ✅ Validação automática de qualidade
- ✅ Erros tratados graciosamente
- ✅ Performance adequada (< 30s para gerar)

## Stack
- Google AI (Gemini Pro 1.5)
- Supabase (armazenamento)
- Markdown para formatação do diagnóstico

IMPORTANTE: O diagnóstico deve soar humano, profundo e personalizado. Não pode parecer genérico ou robótico.
```

### Tempo Estimado
10-12 horas de desenvolvimento e testes

---

## 📧 CHAT 5: SISTEMA DE EMAILS E DASHBOARD ADMIN

### Objetivo
Implementar sistema de envio de emails branded e dashboard administrativo para Nathalia gerenciar leads.

### Escopo

#### 5.1 Sistema de Emails

**Setup Resend:**
```bash
npm install resend react-email
```

**`.env.local`**
```
RESEND_API_KEY=your_api_key_here
```

**`lib/email/client.ts`**
```typescript
import { Resend } from 'resend'

export const resend = new Resend(process.env.RESEND_API_KEY)
```

**Templates de Email:**

**`lib/email/templates/diagnosis-email.tsx`**
```tsx
import {
  Html, Head, Body, Container, Heading, Text,
  Button, Hr, Section, Img
} from '@react-email/components'

interface DiagnosisEmailProps {
  nome: string
  diagnosis: string // Markdown
}

export function DiagnosisEmail({ nome, diagnosis }: DiagnosisEmailProps) {
  return (
    <Html>
      <Head />
      <Body style={styles.body}>
        <Container style={styles.container}>
          {/* Logo */}
          <Section style={styles.header}>
            <Heading style={styles.logo}>LUMERA</Heading>
            <Text style={styles.tagline}>Da Estagnação à Estratégia</Text>
          </Section>

          {/* Saudação */}
          <Text style={styles.greeting}>Olá {nome},</Text>

          <Text style={styles.intro}>
            Finalizei a análise das suas respostas e preparei um diagnóstico
            personalizado para você.
          </Text>

          {/* Diagnóstico (Markdown convertido para HTML) */}
          <Section
            style={styles.diagnosis}
            dangerouslySetInnerHTML={{ __html: markdownToHtml(diagnosis) }}
          />

          {/* CTA */}
          <Section style={styles.cta}>
            <Button style={styles.button} href="https://wa.me/...">
              Agendar Sessão Estratégica Gratuita
            </Button>
          </Section>

          {/* Footer */}
          <Hr style={styles.hr} />
          <Text style={styles.footer}>
            Com clareza e propósito,<br />
            <strong>Nathalia Mazetto</strong><br />
            Mentora de Propósito | LUMERA
          </Text>

          <Text style={styles.subfooter}>
            © 2025 Lumera | Todos os direitos reservados
          </Text>
        </Container>
      </Body>
    </Html>
  )
}

const styles = {
  body: { backgroundColor: '#FDFBF7', fontFamily: 'Inter, sans-serif' },
  container: { maxWidth: '600px', margin: '0 auto', padding: '40px 20px' },
  header: { textAlign: 'center', marginBottom: '32px' },
  logo: { color: '#284138', fontSize: '32px', fontWeight: 'bold', margin: '0' },
  tagline: { color: '#80907B', fontSize: '14px', margin: '8px 0 0' },
  // ... mais estilos
}
```

**`lib/email/templates/welcome-email.tsx`**
(Email de boas-vindas após completar o quiz)

**`lib/email/utils/markdown-to-html.ts`**
```typescript
import { marked } from 'marked'

export function markdownToHtml(markdown: string): string {
  return marked.parse(markdown)
}
```

**API Route de Envio:**

**`app/api/send-email/route.ts`**
```typescript
import { NextResponse } from 'next/server'
import { resend } from '@/lib/email/client'
import { DiagnosisEmail } from '@/lib/email/templates/diagnosis-email'
import { getQuizResponse } from '@/lib/db/queries'

export async function POST(req: Request) {
  try {
    const { quizId } = await req.json()

    const quizData = await getQuizResponse(quizId)

    await resend.emails.send({
      from: 'Nathalia Mazetto <nathalia@lumera.com.br>',
      to: quizData.email,
      subject: `${quizData.nome}, seu diagnóstico LUMERA está pronto ✨`,
      react: DiagnosisEmail({
        nome: quizData.nome,
        diagnosis: quizData.diagnosis,
      }),
    })

    return NextResponse.json({ success: true })
  } catch (error) {
    console.error('Error sending email:', error)
    return NextResponse.json(
      { error: 'Failed to send email' },
      { status: 500 }
    )
  }
}
```

#### 5.2 Dashboard Administrativo

**Autenticação:**

**Setup NextAuth.js:**
```bash
npm install next-auth @auth/supabase-adapter
```

**`app/api/auth/[...nextauth]/route.ts`**
```typescript
import NextAuth from 'next-auth'
import CredentialsProvider from 'next-auth/providers/credentials'

const handler = NextAuth({
  providers: [
    CredentialsProvider({
      name: 'Credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        // Validar credenciais de Nathalia
        if (
          credentials?.email === process.env.ADMIN_EMAIL &&
          credentials?.password === process.env.ADMIN_PASSWORD
        ) {
          return { id: '1', email: credentials.email, name: 'Nathalia' }
        }
        return null
      },
    }),
  ],
  pages: {
    signIn: '/login',
  },
})

export { handler as GET, handler as POST }
```

**Middleware de Proteção:**

**`middleware.ts`**
```typescript
export { default } from 'next-auth/middleware'

export const config = {
  matcher: ['/dashboard/:path*'],
}
```

**Layout do Dashboard:**

**`app/dashboard/layout.tsx`**
```tsx
import { Sidebar } from '@/components/dashboard/Sidebar'
import { TopBar } from '@/components/dashboard/TopBar'

export default function DashboardLayout({ children }) {
  return (
    <div className="flex h-screen bg-gray-50">
      <Sidebar />
      <div className="flex-1 flex flex-col">
        <TopBar />
        <main className="flex-1 overflow-y-auto p-8">
          {children}
        </main>
      </div>
    </div>
  )
}
```

**Páginas do Dashboard:**

**`app/dashboard/page.tsx`** - Overview
- Métricas principais (cards)
- Total de leads
- Diagnósticos gerados hoje
- Taxa de conversão
- Gráfico de evolução

**`app/dashboard/leads/page.tsx`** - Gestão de Leads
- Tabela com todos os leads
- Colunas: Nome, Email, Instagram, Faturamento, Data, Status, Ações
- Filtros: Status, Faturamento, Nível de Consciência, Data
- Busca por nome/email
- Paginação
- Ações: Ver detalhes, Regenerar diagnóstico, Marcar como contatado

**`app/dashboard/leads/[id]/page.tsx`** - Detalhes do Lead
- Informações completas
- Respostas do quiz
- Diagnóstico gerado (preview)
- Histórico de ações
- Botões de ação: Enviar follow-up, Download PDF, Editar status

**`app/dashboard/diagnosticos/page.tsx`** - Histórico de Diagnósticos
- Lista de todos os diagnósticos
- Preview rápido
- Download em lote
- Estatísticas de qualidade

**`app/dashboard/analytics/page.tsx`** - Analytics
- Gráficos detalhados
- Funil de conversão
- Análise por segmento
- Tendências temporais
- Padrões de bloqueios mais comuns

**Componentes do Dashboard:**

**`components/dashboard/Sidebar.tsx`**
- Navegação lateral
- Logo Lumera
- Menu items
- Logout

**`components/dashboard/TopBar.tsx`**
- Breadcrumbs
- Notificações
- Perfil do usuário

**`components/dashboard/LeadsTable.tsx`**
- Tabela de leads
- Ordenação
- Filtros
- Actions

**`components/dashboard/StatsCard.tsx`**
- Card de métrica
- Número + variação
- Ícone

**`components/dashboard/Charts.tsx`**
- Gráficos (Recharts)
- Line, Bar, Pie

**Queries do Dashboard:**

**`lib/db/dashboard-queries.ts`**
```typescript
export async function getDashboardStats() {
  // Total de leads
  const { count: totalLeads } = await supabase
    .from('quiz_responses')
    .select('*', { count: 'exact', head: true })

  // Diagnósticos hoje
  const today = new Date().toISOString().split('T')[0]
  const { count: diagnosisToday } = await supabase
    .from('quiz_responses')
    .select('*', { count: 'exact', head: true })
    .gte('diagnosis_generated_at', today)

  // ... mais queries

  return { totalLeads, diagnosisToday, ... }
}

export async function getLeads(filters?: FilterOptions) {
  let query = supabase.from('quiz_responses').select('*')

  if (filters?.status) {
    query = query.eq('status', filters.status)
  }

  // ... aplicar outros filtros

  return query
}
```

### Prompt para Chat 5

```markdown
# CHAT 5: SISTEMA DE EMAILS E DASHBOARD ADMIN

[INCLUIR TODO O CONTEXTO COMPARTILHADO]

## Situação Atual
Chats anteriores entregaram:
- Landing page premium
- Quiz funcional
- Motor de IA gerando diagnósticos

Agora falta:
- Enviar os diagnósticos por email
- Dashboard para Nathalia gerenciar tudo

## Tarefa Parte 1: Sistema de Emails

### Entregáveis
1. Integração com Resend:
   - Cliente configurado
   - API Key configurada

2. Templates de email branded (React Email):
   - DiagnosisEmail (email principal com diagnóstico)
   - WelcomeEmail (email de boas-vindas)
   - Design 100% Lumera (paleta de cores)
   - Responsivo para mobile
   - CTA claro

3. API Route de envio:
   - `/api/send-email` funcional
   - Converte Markdown para HTML
   - Envia email via Resend
   - Error handling

4. Integração completa:
   - Após gerar diagnóstico, envia email automaticamente
   - Logs de emails enviados

## Tarefa Parte 2: Dashboard Administrativo

### Entregáveis
1. Autenticação (NextAuth.js):
   - Login page (`/login`)
   - Proteção de rotas `/dashboard/*`
   - Credenciais de admin (env vars)

2. Layout do Dashboard:
   - Sidebar com navegação
   - TopBar com breadcrumbs
   - Design clean e profissional

3. Páginas do Dashboard:
   - `/dashboard` - Overview com métricas
   - `/dashboard/leads` - Tabela de leads com filtros
   - `/dashboard/leads/[id]` - Detalhes do lead
   - `/dashboard/diagnosticos` - Histórico
   - `/dashboard/analytics` - Gráficos e insights

4. Componentes do Dashboard:
   - LeadsTable (ordenação, filtros, busca)
   - StatsCard (métricas com ícones)
   - Charts (Recharts - line, bar, pie)
   - Sidebar e TopBar

5. Funcionalidades:
   - Ver todas as respostas do quiz
   - Ver diagnóstico gerado
   - Regenerar diagnóstico
   - Marcar lead como contatado
   - Download PDF do diagnóstico
   - Filtros: status, faturamento, data
   - Busca por nome/email

## Critérios de Sucesso
- ✅ Emails enviados automaticamente após diagnóstico
- ✅ Emails com design Lumera impecável
- ✅ Dashboard funcional e intuitivo
- ✅ Autenticação segura
- ✅ Todas as métricas calculadas corretamente
- ✅ Performance otimizada (lazy loading de dados)
- ✅ Mobile responsivo (dashboard também)

## Stack Adicional
- Resend (emails)
- React Email (templates)
- NextAuth.js (autenticação)
- Recharts (gráficos)
- Marked (Markdown to HTML)

Por favor, crie um sistema de emails elegante e um dashboard profissional que permita Nathalia gerenciar todos os leads com facilidade.
```

### Tempo Estimado
12-14 horas de desenvolvimento

---

## 📊 RESUMO GERAL DOS 5 CHATS

### Chat 1: Fundação (6-8h)
✅ Projeto Next.js configurado
✅ Design System Lumera completo
✅ Componentes UI base
✅ Layout (Header + Footer)

### Chat 2: Landing Page (10-12h)
✅ Homepage com 8 seções
✅ Componentes de marketing
✅ Animações Framer Motion
✅ Mobile responsivo

### Chat 3: Quiz (12-14h)
✅ Quiz multi-step (11 perguntas)
✅ Validação (Zod)
✅ Integração Supabase
✅ UX premium

### Chat 4: IA (10-12h)
✅ Integração Google AI
✅ Prompt estruturado
✅ Geração de diagnósticos
✅ Validação de qualidade

### Chat 5: Emails + Dashboard (12-14h)
✅ Sistema de emails branded
✅ Dashboard administrativo
✅ Autenticação
✅ Analytics e métricas

---

## 🎯 TOTAL ESTIMADO
**50-60 horas de desenvolvimento**

Dividido em 5 chats sequenciais, cada um entregando um módulo funcional e testado.

---

## 📝 TEMPLATE DE INÍCIO DE CADA CHAT

```markdown
# CHAT [NÚMERO]: [TÍTULO]

## CONTEXTO LUMERA (SEMPRE INCLUIR)
[Todo o contexto compartilhado da marca, paleta, stack, objetivos]

## SITUAÇÃO ATUAL
O que foi entregue nos chats anteriores:
- Chat 1: [resumo]
- Chat 2: [resumo]
- Chat N-1: [resumo]

## TAREFA DESTE CHAT
[Descrição clara do que deve ser desenvolvido]

## ENTREGÁVEIS
[Lista específica e detalhada]

## CRITÉRIOS DE SUCESSO
[Checklist de qualidade]

## STACK ADICIONAL
[Bibliotecas/ferramentas específicas deste chat]

## REFERÊNCIAS
[Links para seções específicas dos documentos]
```

---

**Com esta estrutura, garantimos:**
- ✅ Continuidade entre chats
- ✅ Contexto sempre presente
- ✅ Entregas incrementais funcionais
- ✅ Qualidade consistente
- ✅ Foco em cada etapa
- ✅ Facilidade de revisão e ajustes

---

> **"Da Estagnação à Estratégia"**
> Divisão Estratégica de Desenvolvimento | Projeto Lumera App | v1.0
