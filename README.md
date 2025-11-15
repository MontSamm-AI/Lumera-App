# LUMERA APP

> **"Da Estagnação à Estratégia"**
> Plataforma digital premium de mentoria e consultoria estratégica

![Status](https://img.shields.io/badge/status-em_desenvolvimento-yellow)
![Versão](https://img.shields.io/badge/versão-MVP_1.0-blue)
![License](https://img.shields.io/badge/license-Private-red)

---

## 🌟 SOBRE O PROJETO

**Lumera App** é uma aplicação web premium que automatiza o funil de captação de leads para **Nathalia Mazetto**, mentora de propósito e consultora estratégica.

### Objetivo
Transformar empreendedoras estagnadas em líderes estratégicas através de clareza, posicionamento e estrutura, utilizando o **Método LUMERA** proprietário.

### Funcionalidades Principais (MVP)
- ✅ Landing page premium com branding sofisticado
- ✅ Quiz diagnóstico inteligente (8 perguntas estratégicas)
- ✅ Geração automatizada de diagnóstico personalizado com IA (Gemini 2.5 Flash)
- ✅ Envio do diagnóstico via WhatsApp (Evolution API)
- ✅ Aplicação do Método LUMERA ao caso específico de cada lead
- ✅ CTA para agendamento de Sessão Estratégica Gratuita

---

## 👤 SOBRE NATHALIA MAZETTO

**Nathalia Mazetto** é mentora de propósito e consultora estratégica especializada em guiar mulheres empreendedoras a transformarem estagnação em estratégia.

### Missão
Ajudar empreendedoras inconformadas com seu resultado atual a reconectarem-se com seu propósito e expressarem sua essência com clareza, beleza e autenticidade.

### Método LUMERA
Framework proprietário de transformação estratégica com 6 pilares:

- **L** - Luz e Propósito (Clareza)
- **U** - Unificação (Estratégia)
- **M** - Movimento (Ação e Foco)
- **E** - Estrutura (Base de Crescimento)
- **R** - Reconhecimento (Posicionamento)
- **A** - Alinhamento (Expansão e Consistência)

### Serviços Oferecidos
- **Mentoria de Propósito:** Processo de 6 encontros para reconexão com propósito e clareza de direção
- **Consultoria Criativa:** Consultoria para alinhar propósito, estética e estratégia de marca
- **Sessão Estratégica Gratuita:** Diagnóstico inicial e plano de ação (gerado automaticamente pelo app)

### Posicionamento
*"Guio empreendedoras a transformarem estagnação em estratégia através de clareza, posicionamento e estrutura de negócio."*

### Público-Alvo
Mulheres empreendedoras (25-45 anos) que:
- Sentem-se estagnadas no negócio
- Têm faturamento de R$ 1k-10k/mês
- Buscam clareza estratégica e propósito
- Valorizam autenticidade e transformação profunda

---

## 🎨 BRANDING LUMERA

### Origem do Nome
**LUMERA** = Do latim *"lumen"* (luz) + *"era"* (novo tempo)

Evoca iluminação, clareza, liderança feminina e transição da escuridão (estagnação) para a luz (estratégia).

### Paleta de Cores

| Cor | Hex | Uso |
|-----|-----|-----|
| **Emerald Green** | `#284138` | Autoridade, CTAs principais, headers |
| **Wasabi** | `#80907B` | Serenidade, backgrounds, cards |
| **Creased Khari** | `#F8D794` | Luz/clareza, destaques, progresso |
| **Egyptian Earth** | `#BB6830` | Ação/calor, CTAs secundários |
| **Noir de Vigne** | `#111410` | Premium, textos, contraste |

### Tom de Voz
- Sábia sem ser pedante
- Estratégica sem ser fria
- Acolhedora sem ser maternal
- Premium e sofisticada
- Direta e prática

---

## 🏗️ ARQUITETURA TÉCNICA

### Stack
**Frontend:**
- Next.js 14+ (App Router)
- TypeScript (strict mode)
- Tailwind CSS (customizado com paleta Lumera)
- Framer Motion (animações sutis)
- React Hook Form + Zod (validação)

**Backend:**
- Next.js API Routes
- Supabase (PostgreSQL + Auth)
- Google AI - Gemini 2.5 Flash (geração de diagnósticos)
- Evolution API (envio via WhatsApp)
- jsPDF (geração de PDF)

**Deploy:**
- Vercel (com preview por branch)
- Domínio: [a definir]

### Fluxo Completo

```
1. Lead acessa Landing Page
   ↓
2. Clica em "Fazer Diagnóstico Gratuito"
   ↓
3. Responde Quiz (8 perguntas, ~3 minutos)
   ↓
4. Sistema valida dados e salva no Supabase
   ↓
5. Trigger automático: Gera diagnóstico com IA
   ↓
6. IA aplica Método LUMERA ao caso específico
   ↓
7. Sistema converte Markdown → PDF branded
   ↓
8. Evolution API valida WhatsApp
   ↓
9. Envia mensagem + PDF via WhatsApp
   ↓
10. Lead recebe diagnóstico em ~5 minutos
    ↓
11. CTA: Agendar Sessão Estratégica Gratuita
    ↓
12. Lead agenda → Nathalia faz oferta de Mentoria/Consultoria
```

---

## 🚀 SETUP DO PROJETO

### Pré-requisitos
- Node.js 18+
- pnpm (recomendado) ou npm
- Conta Supabase
- Conta Google AI (Gemini API)
- Evolution API configurada
- Conta Vercel

### Instalação

```bash
# Clonar repositório
git clone https://github.com/MontSamm-AI/Lumera-App.git
cd Lumera-App

# Instalar dependências
pnpm install

# Copiar .env.example para .env.local
cp .env.example .env.local

# Editar .env.local com suas credenciais
nano .env.local
```

### Variáveis de Ambiente

```env
# Next.js
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://seu-projeto.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=sua-anon-key
SUPABASE_SERVICE_ROLE_KEY=sua-service-role-key

# Google AI
GOOGLE_AI_API_KEY=sua-google-ai-key

# Evolution API (WhatsApp)
EVOLUTION_API_URL=https://sua-instancia.evolution-api.com
EVOLUTION_API_KEY=sua-evolution-api-key
EVOLUTION_INSTANCE_NAME=lumera-app

# Analytics (opcional)
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

### Desenvolvimento

```bash
# Rodar em modo desenvolvimento
pnpm dev

# Abrir no navegador
open http://localhost:3000

# Build de produção (testar localmente)
pnpm build
pnpm start
```

### Deploy

```bash
# Deploy automático via Vercel (conectado ao GitHub)
git push origin main

# Ou manual
vercel --prod
```

---

## 📁 ESTRUTURA DO PROJETO

```
lumera-app/
├── app/                          # Next.js App Router
│   ├── (marketing)/             # Rotas públicas
│   │   ├── page.tsx            # Landing page
│   │   └── _components/        # Componentes da landing
│   ├── quiz/                    # Quiz diagnóstico
│   │   ├── page.tsx
│   │   ├── obrigado/page.tsx
│   │   └── _components/
│   └── api/                     # API Routes
│       ├── quiz/submit/
│       ├── generate-diagnosis/
│       └── send-diagnosis/
├── components/
│   ├── ui/                      # Componentes base (Button, Input, etc)
│   ├── marketing/               # Componentes de marketing
│   └── quiz/                    # Componentes do quiz
├── lib/
│   ├── ai/                      # Google AI integration
│   ├── db/                      # Supabase queries
│   ├── whatsapp/                # Evolution API
│   ├── pdf/                     # Geração de PDF
│   └── utils/                   # Utilitários
├── types/                       # TypeScript types
├── public/                      # Assets estáticos
└── docs/                        # Documentação técnica
    ├── MVP-SIMPLIFICADO.md
    ├── SYSTEM-PROMPT-ULTRA-DETALHADO.md
    ├── EVOLUTION-API-INTEGRACAO.md
    ├── PROMPT-IA-DIAGNOSTICO.md
    ├── SUPABASE-SETUP.md
    └── ESTRUTURA-REPOSITORIO.md
```

---

## 📚 DOCUMENTAÇÃO TÉCNICA

### Para Desenvolvedores
- **[MVP-SIMPLIFICADO.md](MVP-SIMPLIFICADO.md)** - Escopo focado do MVP
- **[SYSTEM-PROMPT-ULTRA-DETALHADO.md](SYSTEM-PROMPT-ULTRA-DETALHADO.md)** - Códigos completos de todas as páginas
- **[SUPABASE-SETUP.md](SUPABASE-SETUP.md)** - Configuração do banco de dados
- **[EVOLUTION-API-INTEGRACAO.md](EVOLUTION-API-INTEGRACAO.md)** - Integração WhatsApp
- **[PROMPT-IA-DIAGNOSTICO.md](PROMPT-IA-DIAGNOSTICO.md)** - Prompt completo da IA

### Para Designers
- **[DOCUMENTACAO-COMPLETA-DNA-BRANDING.md](DOCUMENTACAO-COMPLETA-DNA-BRANDING.md)** - Guia completo de branding
- `Paleta-Lumera-Nathalia.jpg` - Paleta de cores visual

### Para Product Managers
- **[RELATORIO-ANALISE-COMPLETA.md](RELATORIO-ANALISE-COMPLETA.md)** - Análise de mercado e estratégia
- **[ENGENHARIA-REVERSA-QUIZ.md](ENGENHARIA-REVERSA-QUIZ.md)** - Lógica do quiz e diagnóstico

---

## 🔐 SEGURANÇA E PRIVACIDADE

### Conformidade LGPD
- ✅ Consentimento explícito no quiz
- ✅ Política de privacidade clara
- ✅ Opção de deletar dados (via contato)
- ✅ Armazenamento seguro (Supabase)
- ✅ Uso de dados apenas para fins declarados

### Segurança Técnica
- ✅ HTTPS em produção
- ✅ Variáveis de ambiente para secrets
- ✅ Validação server-side de todos inputs
- ✅ RLS (Row Level Security) no Supabase
- ✅ Rate limiting em APIs sensíveis
- ✅ Sanitização de inputs do usuário

---

## 📊 MÉTRICAS E KPIs

### Métricas de Funil
- **Visitantes únicos** da landing page
- **Taxa de início do quiz** (cliques no CTA)
- **Taxa de conclusão do quiz** (meta: >70%)
- **Taxa de entrega via WhatsApp** (meta: >95%)
- **Taxa de agendamento** de sessão estratégica (meta: >20%)
- **Taxa de conversão** para cliente pagante

### Métricas Técnicas
- **Lighthouse Performance:** 90+
- **Lighthouse Accessibility:** 100
- **Tempo de carregamento:** <2s
- **Uptime:** 99.9%

---

## 🤝 CONTRIBUINDO

### Workflow de Desenvolvimento

1. **Criar branch** a partir de `develop`
   ```bash
   git checkout develop
   git checkout -b feature/nome-da-feature
   ```

2. **Desenvolver** e commitar
   ```bash
   git add .
   git commit -m "feat: descrição da feature"
   ```

3. **Push** e abrir **Pull Request**
   ```bash
   git push origin feature/nome-da-feature
   ```

4. **Code Review** e merge

### Convenção de Commits
```
feat: nova feature
fix: correção de bug
style: formatação, espaçamento
refactor: refatoração de código
docs: atualização de documentação
chore: tarefas de build, configs
```

---

## 📞 CONTATO

**Projeto:** Lumera App
**Cliente:** Nathalia Mazetto
**Repositório:** https://github.com/MontSamm-AI/Lumera-App

---

## 📝 LICENSE

© 2025 Nathalia Mazetto | LUMERA. Todos os direitos reservados.
Projeto privado - uso não autorizado é proibido.

---

**Status:** 🚧 Em desenvolvimento - MVP
**Última atualização:** 14/11/2025
