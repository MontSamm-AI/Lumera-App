# MVP LUMERA APP - ESCOPO SIMPLIFICADO E FOCADO

> **Versão:** 2.0 - MVP Pragmático
> **Data:** 14/11/2025
> **Filosofia:** 80/20 - Máximo valor, mínima complexidade

---

## 🎯 OBJETIVO CENTRAL

Criar uma **Landing Page Premium** + **Quiz Estratégico** + **Diagnóstico IA via WhatsApp** que:
- Capture leads qualificados
- Entregue valor real imediato (diagnóstico personalizado)
- Posicione Nathalia como autoridade
- Avance o lead no funil de forma natural
- Seja disruptivo e inovador mantendo funcionalidade

---

## 📊 ESCOPO DO MVP (O QUE VAI SER FEITO)

### ✅ FASE 1: ESSENCIAL (MVP Mínimo)

#### 1. **Landing Page Premium**
**Seções (simplificado):**
- **Hero** - Manifesto + CTA principal "Fazer Diagnóstico Gratuito"
- **Sobre Nathalia** - Foto + autoridade + método LUMERA resumido
- **Como Funciona** - 3 passos simples (Quiz → Diagnóstico → Sessão)
- **Para Quem é** - Persona clara (empreendedora estagnada)
- **Método LUMERA** - 6 pilares explicados (cards elegantes)
- **CTA Final** - Forte e claro
- **Footer** - Minimalista (links, Instagram, WhatsApp)

**NÃO TEM (por enquanto):**
- ❌ Depoimentos (ainda não há provas sociais)
- ❌ Blog integrado
- ❌ Múltiplas páginas de serviços
- ❌ FAQ complexo

#### 2. **Quiz Diagnóstico Estratégico**

**Características:**
- **Multi-step elegante** (1 pergunta por vez)
- **Barra de progresso** visual e motivadora
- **Perguntas estratégicas** (máximo 8-10, reduzido de 11)
- **Campos intuitivos:**
  - Nome (text)
  - WhatsApp (validação BR automática, aceita diversos formatos)
  - Email (coleta para futuro, validação simples)
  - **Seleções múltipla escolha** (maioria das perguntas)
  - Apenas 2-3 campos abertos essenciais
- **Salvamento automático** (localStorage)
- **Design Lumera** (paleta aplicada estrategicamente)

**Perguntas Otimizadas (8 perguntas):**
1. Nome completo
2. WhatsApp (validação flexível)
3. Email
4. Tipo de negócio (select: 3 opções)
5. Faturamento mensal atual (select: 5 faixas)
6. Principal desafio hoje (select: 5 opções + "outro")
7. O que te impede de crescer? (textarea: 2-3 frases)
8. Onde quer chegar nos próximos 6 meses? (textarea: 2-3 frases)

**Página de confirmação:**
- Mensagem de sucesso
- "Seu diagnóstico está sendo preparado..."
- "Você receberá via WhatsApp em até 5 minutos"

#### 3. **Motor de IA - Diagnóstico Personalizado**

**Tecnologia:**
- **Google AI (Gemini 2.5 Flash)** - rápido e eficiente
- **Prompt estruturado** com contexto completo do funil
- **Personalização profunda** baseada nas respostas

**Estrutura do Diagnóstico (Markdown → PDF):**
- Cabeçalho branded Lumera
- Saudação personalizada
- Diagnóstico da situação atual (Ponto A)
- Análise dos bloqueios específicos
- Método LUMERA aplicado ao caso
- Visão do resultado possível (Ponto B)
- Próximos passos claros
- **CTA forte:** Agendar Sessão Estratégica Gratuita

**Entrega:**
- Via **WhatsApp** (Evolution API)
- Mensagem de texto personalizada
- PDF anexado (diagnóstico completo)
- Link para agendar sessão

#### 4. **Integração Evolution API (WhatsApp)**

**Funcionalidades:**
- Enviar mensagens de texto
- Enviar documentos (PDF do diagnóstico)
- Validar número de WhatsApp
- Receber confirmação de entrega

**Fluxo:**
1. Lead completa quiz
2. Sistema valida WhatsApp (Evolution API)
3. IA gera diagnóstico (Gemini)
4. Sistema converte Markdown → PDF
5. Evolution API envia mensagem + PDF
6. Lead recebe diagnóstico no WhatsApp

#### 5. **Banco de Dados (Supabase)**

**Tabela: quiz_responses**
```sql
CREATE TABLE quiz_responses (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  created_at TIMESTAMP DEFAULT NOW(),

  -- Dados pessoais
  nome TEXT NOT NULL,
  whatsapp TEXT NOT NULL,
  email TEXT,

  -- Dados do negócio
  tipo_negocio TEXT,
  faturamento TEXT,
  principal_desafio TEXT,
  bloqueios TEXT,
  objetivo_6_meses TEXT,

  -- Diagnóstico
  diagnosis TEXT,
  diagnosis_generated_at TIMESTAMP,
  diagnosis_sent BOOLEAN DEFAULT FALSE,
  diagnosis_sent_at TIMESTAMP,

  -- Status
  status TEXT DEFAULT 'pending', -- pending, diagnosed, contacted, client

  -- Metadata
  utm_source TEXT,
  utm_medium TEXT,
  utm_campaign TEXT
)
```

**Queries que EU vou criar:**
- Salvar resposta do quiz
- Buscar resposta por ID
- Atualizar com diagnóstico gerado
- Marcar como enviado
- Listar leads (para painel simples futuro)

---

## ❌ O QUE NÃO VAI TER NO MVP

Para focar no 80/20 e entregar rápido:

- ❌ Dashboard admin complexo (só uma view simples de leads no Supabase)
- ❌ Sistema de autenticação
- ❌ Área do cliente
- ❌ Email marketing automatizado (foco em WhatsApp)
- ❌ Blog integrado
- ❌ SEO avançado (apenas básico)
- ❌ Múltiplas landing pages
- ❌ Sistema de pagamento
- ❌ Agendamento integrado (link externo Calendly)
- ❌ Analytics avançado (apenas Google Analytics básico)
- ❌ A/B testing
- ❌ Múltiplos idiomas
- ❌ Chat ao vivo

**Tudo isso pode vir na v2, mas NÃO é essencial agora.**

---

## 🎨 DESIGN SYSTEM - APLICAÇÃO ESTRATÉGICA DAS CORES

### Paleta Lumera (aplicação prática)

#### **Emerald Green (#284138)** - Autoridade
**Uso:**
- Headers e navegação
- CTAs principais ("Fazer Diagnóstico Gratuito")
- Títulos importantes
- Ícones de destaque
- Hover states de botões primários

#### **Wasabi (#80907B)** - Serenidade
**Uso:**
- Backgrounds de seções alternadas
- Cards de informação
- Bordas suaves
- Subtítulos
- Estados desabilitados

#### **Creased Khari (#F8D794)** - Luz e Clareza
**Uso:**
- Destaques e badges
- Ícones informativos
- Barra de progresso do quiz
- Hover effects sutis
- Acentos em textos importantes

#### **Egyptian Earth (#BB6830)** - Ação e Calor
**Uso:**
- CTAs secundários
- Links importantes
- Notificações de sucesso
- Elementos de atenção
- Badges de status

#### **Noir de Vigne (#111410)** - Premium
**Uso:**
- Textos principais
- Títulos de seções
- Footer
- Elementos de contraste alto
- Bordasem destaque

### Combinações Estratégicas por Seção

**Hero:**
- Background: Gradient suave (Off-white → Wasabi 10%)
- Título: Noir de Vigne
- Subtítulo: Emerald Green
- CTA: Emerald Green (bg) + Off-white (text)
- Detalhe decorativo: Creased Khari (sutil)

**Quiz:**
- Background: Off-white limpo
- Card da pergunta: White com sombra suave
- Barra de progresso: Creased Khari (preenchido) + Wasabi (vazio)
- Botão "Próximo": Emerald Green
- Botão "Voltar": Wasabi
- Inputs: Borda Wasabi, focus Emerald Green

**Confirmação:**
- Background: Gradient (Wasabi suave → Off-white)
- Card central: White elevation
- Ícone de sucesso: Creased Khari
- Texto: Noir de Vigne
- CTA: Egyptian Earth

---

## 🔧 STACK TÉCNICO DEFINITIVO (SIMPLIFICADO)

### Frontend
- **Next.js 14+** (App Router)
- **TypeScript** (strict)
- **Tailwind CSS** (config customizado Lumera)
- **Framer Motion** (animações sutis)
- **Lucide Icons** (ícones minimalistas)
- **React Hook Form** + **Zod** (formulários e validação)

### Backend
- **Next.js API Routes**
- **Supabase** (PostgreSQL + client)
- **Google AI SDK** (Gemini 2.5 Flash)
- **Evolution API** (WhatsApp integration)
- **jsPDF** ou **Puppeteer** (geração PDF)

### Deploy
- **Vercel** (já configurado)
- **Domínio:** lumera.com.br ou app.lumera.com.br (a definir)

### Analytics
- **Google Analytics 4** (básico)
- **Vercel Analytics** (performance)

---

## 📱 EVOLUTION API - INTEGRAÇÃO WHATSAPP

### Endpoints Utilizados

#### 1. **Validar Número**
```bash
GET /validate-number/{instance}/{number}
```
Verifica se número existe no WhatsApp

#### 2. **Enviar Mensagem de Texto**
```bash
POST /message/sendText/{instance}
```
```json
{
  "number": "5511999999999",
  "text": "Olá {nome}, seu diagnóstico LUMERA está pronto! 🌟"
}
```

#### 3. **Enviar Documento (PDF)**
```bash
POST /message/sendMedia/{instance}
```
```json
{
  "number": "5511999999999",
  "mediatype": "document",
  "mimetype": "application/pdf",
  "caption": "📊 Aqui está seu Diagnóstico LUMERA Personalizado",
  "media": "base64_encoded_pdf"
}
```

#### 4. **Receber Webhooks** (futuro - v2)
Para quando o lead responder no WhatsApp

### Fluxo de Envio do Diagnóstico

```typescript
// app/api/send-diagnosis/route.ts
async function sendDiagnosisViaWhatsApp(quizId: string) {
  // 1. Buscar dados do quiz
  const quizData = await getQuizResponse(quizId)

  // 2. Validar número WhatsApp
  const isValid = await evolutionAPI.validateNumber(quizData.whatsapp)
  if (!isValid) throw new Error('WhatsApp inválido')

  // 3. Gerar diagnóstico (IA)
  const diagnosis = await generateDiagnosis(quizData)

  // 4. Converter para PDF
  const pdfBuffer = await generatePDF(diagnosis, quizData.nome)
  const pdfBase64 = pdfBuffer.toString('base64')

  // 5. Enviar mensagem de texto
  await evolutionAPI.sendText({
    number: quizData.whatsapp,
    text: `Olá ${quizData.nome}! 👋\n\nSeu *Diagnóstico LUMERA* está pronto! 🌟\n\nAnalisei suas respostas com muito cuidado e preparei um relatório personalizado para você.\n\nEstou enviando o PDF completo logo abaixo. 📄\n\n_Com clareza e propósito,_\n*Nathalia Mazetto*`
  })

  // 6. Enviar PDF
  await evolutionAPI.sendDocument({
    number: quizData.whatsapp,
    media: pdfBase64,
    filename: `Diagnostico-LUMERA-${quizData.nome.replace(/\s/g, '-')}.pdf`,
    caption: '📊 Seu Diagnóstico LUMERA Personalizado'
  })

  // 7. Enviar CTA para agendar
  await evolutionAPI.sendText({
    number: quizData.whatsapp,
    text: `Para darmos o próximo passo juntas, convido você para uma *Sessão Estratégica Gratuita* comigo.\n\n🗓️ Agende sua sessão:\nhttps://calendly.com/lumera/sessao-estrategica\n\nVamos transformar clareza em ação! 🚀`
  })

  // 8. Marcar como enviado no banco
  await updateDiagnosisSent(quizId)
}
```

---

## 🤖 PROMPT DA IA - CONTEXTO COMPLETO DO FUNIL

O Gemini 2.5 Flash precisa entender:
1. **Onde o lead está no funil** (acabou de fazer quiz)
2. **Qual o objetivo** (gerar diagnóstico que avança para sessão)
3. **Tom de voz** (Nathalia - sábia, estratégica, acolhedora)
4. **Gatilhos mentais** (escassez, autoridade, reciprocidade)
5. **Storytelling** (transformação de estagnação → estratégia)

### Estrutura do Prompt (simplificada para MVP)

```markdown
# CONTEXTO DO FUNIL
Você é Nathalia Mazetto, mentora de propósito e consultora estratégica.

A lead {nome} acabou de preencher o quiz diagnóstico no site Lumera.
Esta é a PRIMEIRA interação dela com você.

Seu objetivo: Gerar um diagnóstico que:
1. Mostre que você REALMENTE entendeu a situação dela
2. Gere clareza sobre onde ela está (Ponto A) e onde pode chegar (Ponto B)
3. Aplique o Método LUMERA de forma prática ao caso dela
4. Crie desejo pela Sessão Estratégica Gratuita
5. Use storytelling e gatilhos mentais sutis

# TOM DE VOZ
- Sábia sem ser pedante
- Estratégica sem ser fria
- Acolhedora sem ser maternal em excesso
- Premium e sofisticada
- Direta e prática

# DADOS DA LEAD
Nome: {nome}
Tipo de negócio: {tipo_negocio}
Faturamento: {faturamento}
Principal desafio: {principal_desafio}
Bloqueios: {bloqueios}
Objetivo 6 meses: {objetivo_6_meses}

# ESTRUTURA DO DIAGNÓSTICO (800-1000 palavras)

## 🌟 Olá {nome},

[Saudação personalizada mostrando que leu as respostas]

## 📍 Onde Você Está Agora (Ponto A)

[Análise da situação atual baseada nas respostas]
[Identificar padrões de bloqueios]
[Validar a experiência dela]

## 🔍 O Que Eu Vejo Acontecendo

[Diagnóstico profundo]
[2-3 bloqueios principais identificados]
[Crenças limitantes (se aparecerem nas respostas)]

## ✨ Onde Você Pode Estar (Ponto B)

[Visão do resultado possível]
[Conectar com o objetivo dela de 6 meses]
[Criar desejo e esperança]

## 🗺️ O Caminho: Método LUMERA

[Aplicar os 6 pilares ao caso dela]
**L** - Luz e Propósito: [específico para ela]
**U** - Unificação: [específico para ela]
**M** - Movimento: [específico para ela]
**E** - Estrutura: [específico para ela]
**R** - Reconhecimento: [específico para ela]
**A** - Alinhamento: [específico para ela]

## 🚀 Próximo Passo

{nome}, este diagnóstico é o primeiro passo.

Na *Sessão Estratégica Gratuita*, vamos:
✅ Aprofundar sua situação específica
✅ Traçar um plano personalizado de ação
✅ Definir os próximos passos práticos

[CTA claro para agendar]

---

_Com clareza e propósito,_
**Nathalia Mazetto**
Mentora de Propósito | LUMERA

# GATILHOS MENTAIS A USAR (SUTILMENTE)
- Reciprocidade (estou dando valor gratuitamente)
- Autoridade (método estruturado LUMERA)
- Prova social futura (histórias de transformação, sem números ainda)
- Escassez suave (agenda limitada)
- Personalização (isso é SÓ para ela)

# O QUE EVITAR
- Promessas genéricas
- Clichês de coaching
- Ser superficial
- Parecer automático
- Vender diretamente (suavidade é chave)
```

---

## 📁 ESTRUTURA DO REPOSITÓRIO

### Branches Strategy

```
main (produção - deploy automático Vercel)
├── develop (staging - deploy preview Vercel)
    ├── feature/landing-page
    ├── feature/quiz-flow
    ├── feature/ai-diagnosis
    ├── feature/whatsapp-integration
    └── feature/database-setup
```

### Commits Semânticos

```
feat: adiciona hero section na landing page
fix: corrige validação de WhatsApp no quiz
style: ajusta espaçamento do card de pergunta
refactor: modulariza componente de progresso
docs: atualiza README com setup Evolution API
chore: configura Tailwind com paleta Lumera
```

### Issues e Milestones

**Milestone 1: Landing Page** (deadline: semana 1)
- [ ] #1 Criar hero section com CTA
- [ ] #2 Implementar seção "Sobre Nathalia"
- [ ] #3 Criar cards método LUMERA
- [ ] #4 Implementar seção "Como Funciona"
- [ ] #5 Footer minimalista
- [ ] #6 Mobile responsivo

**Milestone 2: Quiz Diagnóstico** (deadline: semana 2)
- [ ] #7 Criar estrutura multi-step
- [ ] #8 Implementar 8 perguntas
- [ ] #9 Validação de campos
- [ ] #10 Barra de progresso
- [ ] #11 Página de confirmação
- [ ] #12 Salvamento localStorage

**Milestone 3: IA + WhatsApp** (deadline: semana 3)
- [ ] #13 Integração Google AI (Gemini)
- [ ] #14 Prompt estruturado do diagnóstico
- [ ] #15 Geração de PDF
- [ ] #16 Setup Evolution API
- [ ] #17 Envio via WhatsApp
- [ ] #18 Testes end-to-end

**Milestone 4: Backend + Database** (eu faço)
- [ ] #19 Setup Supabase
- [ ] #20 Criar tabela quiz_responses
- [ ] #21 API routes (save quiz, generate diagnosis)
- [ ] #22 Validação de número WhatsApp
- [ ] #23 Logs e error handling

---

## 📏 MÉTRICAS DE SUCESSO DO MVP

### Técnicas
- ✅ Lighthouse Performance: 90+
- ✅ Lighthouse Accessibility: 100
- ✅ Mobile responsivo perfeito
- ✅ Tempo de carregamento: < 2s
- ✅ Taxa de conclusão do quiz: > 70%
- ✅ Taxa de envio WhatsApp com sucesso: > 95%

### Negócio
- 🎯 Leads capturados no primeiro mês: 50+
- 🎯 Taxa de agendamento pós-diagnóstico: > 20%
- 🎯 Qualidade percebida do diagnóstico (feedback): 4.5/5+
- 🎯 Conversão para cliente: (a medir)

---

## 🚀 TIMELINE DE DESENVOLVIMENTO

### Semana 1: Landing Page
- Dia 1-2: Setup + Design System
- Dia 3-4: Todas as seções
- Dia 5: Mobile + Animações
- Dia 6-7: Revisão e ajustes

### Semana 2: Quiz
- Dia 1-2: Estrutura multi-step
- Dia 3-4: Perguntas e validações
- Dia 5: UX e animações
- Dia 6-7: Testes e ajustes

### Semana 3: IA + WhatsApp
- Dia 1-2: Integração Gemini + Prompt
- Dia 3-4: Geração PDF + Evolution API
- Dia 5: Testes integração completa
- Dia 6-7: Ajustes finais e deploy

**Total: 3 semanas para MVP funcional**

---

## 💡 INOVAÇÕES E DIFERENCIAIS

### O que torna o Lumera App disruptivo:

1. **Diagnóstico IA Premium via WhatsApp**
   - Não é email frio
   - Chega onde a pessoa já está
   - Mais pessoal e humanizado

2. **Paleta Visual Única**
   - Não se parece com nenhum concorrente
   - Premium sem ser corporativo
   - Feminino sem ser infantil

3. **Método Proprietário Aplicado Automaticamente**
   - LUMERA não é só teoria
   - IA aplica ao caso específico
   - Valor entregue antes da venda

4. **Simplicidade Sofisticada**
   - Minimalista mas rico
   - Fácil mas profundo
   - Rápido mas personalizado

5. **Experiência Fluida**
   - Landing → Quiz → WhatsApp
   - Sem fricção
   - Sem cadastros complexos
   - Valor imediato

---

**Status:** ✅ MVP Redefinido - Focado e Pragmático
**Próximo passo:** System Prompt ULTRA detalhado
