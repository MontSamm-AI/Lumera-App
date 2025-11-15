# ESTRUTURA DE REPOSITÓRIO - LUMERA APP

> **Objetivo:** Organização profissional do Git com branches, issues e milestones

---

## 🌳 ESTRATÉGIA DE BRANCHES

### Estrutura Principal

```
main (produção)
├── develop (staging/preview)
    ├── feature/landing-page
    ├── feature/quiz-flow
    ├── feature/ai-diagnosis
    ├── feature/whatsapp-integration
    ├── feature/database-setup
    ├── fix/quiz-validation
    └── docs/update-readme
```

### Descrição das Branches

**`main`**
- Branch de produção
- Deploy automático na Vercel (https://lumera.app ou app.lumera.com.br)
- Apenas código testado e aprovado
- Protected branch (requires PR + review)

**`develop`**
- Branch de staging
- Deploy preview na Vercel (https://lumera-app-develop.vercel.app)
- Integração contínua de features
- Base para todas as branches de feature

**`feature/*`**
- Branches para novas funcionalidades
- Nomenclatura: `feature/nome-descritivo`
- Exemplos:
  - `feature/landing-page`
  - `feature/quiz-multi-step`
  - `feature/ai-diagnosis-generation`

**`fix/*`**
- Branches para correções de bugs
- Nomenclatura: `fix/descricao-do-bug`
- Exemplos:
  - `fix/whatsapp-validation`
  - `fix/quiz-progress-bar`

**`docs/*`**
- Branches para documentação
- Nomenclatura: `docs/o-que-atualizar`
- Exemplo: `docs/update-api-documentation`

---

## 📝 CONVENÇÃO DE COMMITS (Semantic Commits)

### Formato

```
tipo(escopo): descrição curta

[corpo opcional com mais detalhes]

[footer opcional com breaking changes ou issues]
```

### Tipos

- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `docs`: Documentação
- `style`: Formatação (não afeta lógica)
- `refactor`: Refatoração de código
- `test`: Adicionar/atualizar testes
- `chore`: Tarefas de manutenção (configs, build)
- `perf`: Melhoria de performance

### Exemplos

```bash
# Feature
git commit -m "feat(quiz): adiciona validação de WhatsApp"

# Fix
git commit -m "fix(landing): corrige responsividade do hero"

# Docs
git commit -m "docs(readme): atualiza instruções de setup"

# Refactor
git commit -m "refactor(api): extrai lógica de diagnóstico para módulo separado"

# Chore
git commit -m "chore: configura Tailwind com paleta Lumera"
```

---

## 🎯 ISSUES E MILESTONES

### Milestones

**Milestone 1: Landing Page Premium** (Semana 1)
- Prazo: 7 dias
- Issues: #1-#6

**Milestone 2: Quiz Diagnóstico** (Semana 2)
- Prazo: 7 dias
- Issues: #7-#12

**Milestone 3: IA + WhatsApp Integration** (Semana 3)
- Prazo: 7 dias
- Issues: #13-#18

**Milestone 4: Backend + Database** (Paralelo)
- Responsável: Backend developer
- Issues: #19-#23

---

### Template de Issues

#### Issue de Feature

```markdown
## 📋 Descrição
[Descrição clara do que precisa ser implementado]

## 🎯 Objetivo
[Por que esta feature é importante]

## ✅ Critérios de Aceitação
- [ ] Critério 1
- [ ] Critério 2
- [ ] Critério 3

## 🎨 Design/Mockup
[Link para Figma ou screenshot]

## 📚 Referências
- [Link para documentação relevante]

## 🏷️ Labels
`feature`, `high-priority`, `milestone-1`
```

#### Issue de Bug

```markdown
## 🐛 Descrição do Bug
[O que está acontecendo]

## 🔄 Passos para Reproduzir
1. Passo 1
2. Passo 2
3. Observe o erro

## ✅ Comportamento Esperado
[O que deveria acontecer]

## 📸 Screenshots
[Se aplicável]

## 🌐 Ambiente
- Browser: Chrome 120
- SO: macOS
- Versão do app: develop branch

## 🏷️ Labels
`bug`, `high-priority`
```

---

### Issues Planejadas (para criar no GitHub)

**Milestone 1: Landing Page**
- [ ] #1: Criar hero section com CTA principal
- [ ] #2: Implementar seção "Sobre Nathalia"
- [ ] #3: Criar cards do Método LUMERA (6 pilares)
- [ ] #4: Implementar seção "Como Funciona" (3 passos)
- [ ] #5: Criar footer minimalista
- [ ] #6: Garantir responsividade mobile perfeita

**Milestone 2: Quiz**
- [ ] #7: Criar estrutura multi-step do quiz
- [ ] #8: Implementar 8 perguntas com validação
- [ ] #9: Adicionar barra de progresso animada
- [ ] #10: Criar página de confirmação (/quiz/obrigado)
- [ ] #11: Implementar salvamento automático (localStorage)
- [ ] #12: Adicionar animações entre perguntas

**Milestone 3: IA + WhatsApp**
- [ ] #13: Integrar Google AI (Gemini 2.5 Flash)
- [ ] #14: Implementar prompt estruturado para diagnóstico
- [ ] #15: Criar geração de PDF com jsPDF
- [ ] #16: Configurar Evolution API client
- [ ] #17: Implementar envio via WhatsApp (texto + PDF)
- [ ] #18: Adicionar logs e error handling completo

**Milestone 4: Backend**
- [ ] #19: Setup Supabase e criar tabela quiz_responses
- [ ] #20: Implementar API route /api/quiz/submit
- [ ] #21: Implementar API route /api/generate-diagnosis
- [ ] #22: Implementar API route /api/send-diagnosis
- [ ] #23: Adicionar validação de WhatsApp e tratamento de erros

---

## 🔄 WORKFLOW DE DESENVOLVIMENTO

### 1. Criar Issue
```bash
# No GitHub, criar issue com template adequado
# Atribuir milestone, labels e assignee
```

### 2. Criar Branch a Partir do Develop
```bash
git checkout develop
git pull origin develop
git checkout -b feature/landing-page
```

### 3. Desenvolver
```bash
# Fazer alterações
git add .
git commit -m "feat(landing): adiciona hero section"

# Continuar desenvolvimento
git add .
git commit -m "feat(landing): adiciona seção sobre Nathalia"
```

### 4. Push e Criar Pull Request
```bash
git push -u origin feature/landing-page

# No GitHub:
# 1. Criar Pull Request para `develop`
# 2. Adicionar descrição detalhada
# 3. Linkar com issue (#1 closes #1)
# 4. Solicitar review
```

### 5. Code Review
- Reviewer checa código
- Testa localmente ou na preview da Vercel
- Aprova ou solicita mudanças

### 6. Merge
```bash
# Após aprovação, fazer merge
# Delete branch após merge (limpar)
```

### 7. Deploy para Produção
```bash
# Quando develop estiver estável
git checkout main
git merge develop
git push origin main

# Deploy automático na Vercel
```

---

## 🚀 DEPLOYS NA VERCEL

### Configuração

**Branch `main`:**
- URL: https://lumera.app (ou app.lumera.com.br)
- Deploy automático em todo push

**Branch `develop`:**
- URL: https://lumera-app-develop.vercel.app
- Deploy preview automático

**Feature branches:**
- URL: https://lumera-app-git-feature-nome.vercel.app
- Deploy preview automático

### Ambientes

```env
# Production (main)
VERCEL_ENV=production
NEXT_PUBLIC_APP_URL=https://lumera.app

# Preview (develop e features)
VERCEL_ENV=preview
NEXT_PUBLIC_APP_URL=https://lumera-app-develop.vercel.app
```

---

## 📊 LABELS DO GITHUB

### Por Tipo
- `feature`: Nova funcionalidade
- `bug`: Correção de bug
- `docs`: Documentação
- `enhancement`: Melhoria de feature existente
- `refactor`: Refatoração de código

### Por Prioridade
- `critical`: Bloqueia produção
- `high-priority`: Importante para MVP
- `medium-priority`: Desejável mas não urgente
- `low-priority`: Nice to have

### Por Área
- `frontend`: React/Next.js
- `backend`: API routes, database
- `design`: UI/UX, branding
- `ai`: Google AI integration
- `whatsapp`: Evolution API

### Por Status
- `in-progress`: Em desenvolvimento
- `needs-review`: Aguardando code review
- `blocked`: Bloqueado por dependência
- `ready-to-deploy`: Pronto para produção

---

## 🔒 PROTEÇÃO DE BRANCHES

### Regras para `main`

```yaml
# Settings → Branches → Branch protection rules
protect: main
rules:
  - Require pull request before merging
  - Require approvals: 1
  - Dismiss stale reviews when new commits are pushed
  - Require status checks to pass (Vercel build)
  - Require branches to be up to date
  - Do not allow bypassing the above settings
```

### Regras para `develop`

```yaml
protect: develop
rules:
  - Require pull request before merging
  - Require status checks to pass
```

---

## 📈 MÉTRICAS E TRACKING

### GitHub Insights

Monitorar:
- Pulse (atividade semanal)
- Contributors (quem está contribuindo)
- Code frequency (commits ao longo do tempo)
- Network (visualização de branches)

### Velocity do Time

Acompanhar:
- Issues fechadas por semana
- PRs mergeados por semana
- Tempo médio de review
- Tempo médio de merge

---

## ✅ CHECKLIST DE ORGANIZAÇÃO

- [ ] Branch `main` criada e protegida
- [ ] Branch `develop` criada
- [ ] Milestones configurados (1, 2, 3, 4)
- [ ] Labels criados
- [ ] Template de issues criado
- [ ] Template de PRs criado
- [ ] Vercel conectado ao repositório
- [ ] Deploy automático configurado
- [ ] Variáveis de ambiente configuradas na Vercel
- [ ] Regras de proteção de branches ativas

---

**Esta estrutura garante desenvolvimento organizado, code quality e deploys seguros.**
