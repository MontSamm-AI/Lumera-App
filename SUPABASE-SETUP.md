# SUPABASE - CONFIGURAÇÃO DO BANCO DE DADOS

> **Stack:** Supabase (PostgreSQL + Auth + Storage)
> **Responsável:** Backend setup (feito por você)

---

## 🔧 SETUP INICIAL

### 1. Criar Projeto no Supabase

1. Acesse https://supabase.com
2. Criar novo projeto
3. Nome: `lumera-app-production`
4. Região: South America (São Paulo)
5. Database Password: [gerar senha forte]

### 2. Variáveis de Ambiente

```env
# .env.local
NEXT_PUBLIC_SUPABASE_URL=https://seu-projeto.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=sua-anon-key-aqui
SUPABASE_SERVICE_ROLE_KEY=sua-service-role-key-aqui
```

---

## 📊 SCHEMA DO BANCO DE DADOS

### Tabela: `quiz_responses`

```sql
-- Criar tabela de respostas do quiz
CREATE TABLE quiz_responses (
  -- Identificação
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),

  -- Dados Pessoais
  nome TEXT NOT NULL,
  whatsapp TEXT NOT NULL,
  email TEXT,

  -- Dados do Negócio
  tipo_negocio TEXT NOT NULL CHECK (tipo_negocio IN ('Serviços', 'Produtos Físicos', 'Infoprodutos')),
  faturamento TEXT NOT NULL,
  principal_desafio TEXT NOT NULL,
  bloqueios TEXT NOT NULL,
  objetivo_6_meses TEXT NOT NULL,

  -- Diagnóstico
  diagnosis TEXT,
  diagnosis_generated_at TIMESTAMP WITH TIME ZONE,

  -- WhatsApp Tracking
  whatsapp_validated BOOLEAN DEFAULT FALSE,
  whatsapp_message_ids JSONB DEFAULT '[]'::jsonb,
  whatsapp_sent_at TIMESTAMP WITH TIME ZONE,
  whatsapp_delivered BOOLEAN DEFAULT FALSE,
  whatsapp_error TEXT,

  -- Status do Lead
  status TEXT DEFAULT 'pending' CHECK (status IN ('pending', 'diagnosed', 'contacted', 'scheduled', 'client')),

  -- UTM Tracking
  utm_source TEXT,
  utm_medium TEXT,
  utm_campaign TEXT,
  utm_term TEXT,
  utm_content TEXT,

  -- Indexes para busca rápida
  CONSTRAINT whatsapp_unique UNIQUE (whatsapp)
);

-- Índices para performance
CREATE INDEX idx_quiz_responses_whatsapp ON quiz_responses(whatsapp);
CREATE INDEX idx_quiz_responses_status ON quiz_responses(status);
CREATE INDEX idx_quiz_responses_created_at ON quiz_responses(created_at DESC);
CREATE INDEX idx_quiz_responses_diagnosis_sent ON quiz_responses(whatsapp_sent_at DESC) WHERE whatsapp_sent_at IS NOT NULL;

-- Trigger para atualizar updated_at
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_quiz_responses_updated_at
BEFORE UPDATE ON quiz_responses
FOR EACH ROW
EXECUTE FUNCTION update_updated_at_column();

-- RLS (Row Level Security) - para acesso seguro
ALTER TABLE quiz_responses ENABLE ROW LEVEL SECURITY;

-- Policy: Permitir INSERT público (para o quiz)
CREATE POLICY "Allow public insert" ON quiz_responses
FOR INSERT TO anon
WITH CHECK (true);

-- Policy: Permitir SELECT/UPDATE apenas com service role
CREATE POLICY "Allow authenticated read" ON quiz_responses
FOR SELECT TO authenticated
USING (true);

CREATE POLICY "Allow service role all" ON quiz_responses
FOR ALL TO service_role
USING (true);
```

---

## 💻 CLIENTE SUPABASE

### Configuração

```typescript
// lib/db/supabase.ts
import { createClient } from '@supabase/supabase-js'
import type { Database } from './database.types'

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!

// Cliente público (para quiz submission)
export const supabase = createClient<Database>(supabaseUrl, supabaseAnonKey)

// Cliente com service role (para API routes)
const supabaseServiceKey = process.env.SUPABASE_SERVICE_ROLE_KEY!

export const supabaseAdmin = createClient<Database>(
  supabaseUrl,
  supabaseServiceKey,
  {
    auth: {
      autoRefreshToken: false,
      persistSession: false,
    },
  }
)
```

---

## 📝 QUERIES

### Arquivo de Queries

```typescript
// lib/db/queries.ts
import { supabaseAdmin } from './supabase'
import type { QuizData } from '@/types/quiz'

export interface QuizResponse {
  id: string
  created_at: string
  nome: string
  whatsapp: string
  email?: string
  tipo_negocio: string
  faturamento: string
  principal_desafio: string
  bloqueios: string
  objetivo_6_meses: string
  diagnosis?: string
  diagnosis_generated_at?: string
  whatsapp_sent_at?: string
  status: string
}

/**
 * Salvar resposta do quiz
 */
export async function saveQuizResponse(
  data: QuizData
): Promise<QuizResponse> {
  const { data: response, error } = await supabaseAdmin
    .from('quiz_responses')
    .insert([
      {
        nome: data.nome,
        whatsapp: data.whatsapp,
        email: data.email || null,
        tipo_negocio: data.tipoNegocio,
        faturamento: data.faturamento,
        principal_desafio: data.principal_desafio,
        bloqueios: data.bloqueios,
        objetivo_6_meses: data.objetivo_6_meses,
        utm_source: data.utm_source,
        utm_medium: data.utm_medium,
        utm_campaign: data.utm_campaign,
      },
    ])
    .select()
    .single()

  if (error) {
    console.error('[DB] Error saving quiz response:', error)
    throw error
  }

  return response
}

/**
 * Buscar resposta do quiz por ID
 */
export async function getQuizResponse(
  quizId: string
): Promise<QuizResponse | null> {
  const { data, error } = await supabaseAdmin
    .from('quiz_responses')
    .select('*')
    .eq('id', quizId)
    .single()

  if (error) {
    console.error('[DB] Error fetching quiz response:', error)
    return null
  }

  return data
}

/**
 * Atualizar com diagnóstico gerado
 */
export async function updateDiagnosis(
  quizId: string,
  diagnosis: string
): Promise<void> {
  const { error } = await supabaseAdmin
    .from('quiz_responses')
    .update({
      diagnosis,
      diagnosis_generated_at: new Date().toISOString(),
      status: 'diagnosed',
    })
    .eq('id', quizId)

  if (error) {
    console.error('[DB] Error updating diagnosis:', error)
    throw error
  }
}

/**
 * Marcar diagnóstico como enviado via WhatsApp
 */
export async function updateDiagnosisSent(
  quizId: string,
  messageIds: string[]
): Promise<void> {
  const { error } = await supabaseAdmin
    .from('quiz_responses')
    .update({
      whatsapp_sent_at: new Date().toISOString(),
      whatsapp_delivered: true,
      whatsapp_message_ids: messageIds,
    })
    .eq('id', quizId)

  if (error) {
    console.error('[DB] Error updating diagnosis sent:', error)
    throw error
  }
}

/**
 * Atualizar status do lead
 */
export async function updateLeadStatus(
  quizId: string,
  status: 'pending' | 'diagnosed' | 'contacted' | 'scheduled' | 'client'
): Promise<void> {
  const { error } = await supabaseAdmin
    .from('quiz_responses')
    .update({ status })
    .eq('id', quizId)

  if (error) {
    console.error('[DB] Error updating lead status:', error)
    throw error
  }
}

/**
 * Listar todos os leads (para painel admin futuro)
 */
export async function listLeads(filters?: {
  status?: string
  limit?: number
  offset?: number
}): Promise<QuizResponse[]> {
  let query = supabaseAdmin
    .from('quiz_responses')
    .select('*')
    .order('created_at', { ascending: false })

  if (filters?.status) {
    query = query.eq('status', filters.status)
  }

  if (filters?.limit) {
    query = query.limit(filters.limit)
  }

  if (filters?.offset) {
    query = query.range(filters.offset, filters.offset + (filters.limit || 10))
  }

  const { data, error } = await query

  if (error) {
    console.error('[DB] Error listing leads:', error)
    return []
  }

  return data || []
}

/**
 * Estatísticas gerais (para dashboard futuro)
 */
export async function getStats(): Promise<{
  total_leads: number
  diagnosed_today: number
  pending: number
  scheduled: number
}> {
  const today = new Date().toISOString().split('T')[0]

  const [totalLeads, diagnosedToday, pending, scheduled] = await Promise.all([
    supabaseAdmin.from('quiz_responses').select('*', { count: 'exact', head: true }),
    supabaseAdmin
      .from('quiz_responses')
      .select('*', { count: 'exact', head: true })
      .gte('diagnosis_generated_at', today),
    supabaseAdmin
      .from('quiz_responses')
      .select('*', { count: 'exact', head: true })
      .eq('status', 'pending'),
    supabaseAdmin
      .from('quiz_responses')
      .select('*', { count: 'exact', head: true })
      .eq('status', 'scheduled'),
  ])

  return {
    total_leads: totalLeads.count || 0,
    diagnosed_today: diagnosedToday.count || 0,
    pending: pending.count || 0,
    scheduled: scheduled.count || 0,
  }
}
```

---

## 🔐 SEGURANÇA

### Row Level Security (RLS)

Já configurado no SQL acima:
- **INSERT público:** Qualquer pessoa pode submeter o quiz
- **SELECT/UPDATE:** Apenas authenticated (futuro painel admin)
- **Service Role:** Acesso total (usado nas API routes)

### Proteção contra Duplicados

WhatsApp é `UNIQUE`, evitando leads duplicadas.

### Validação de Dados

Usar Zod no frontend + CHECK constraints no banco.

---

## 📊 MONITORAMENTO

### Logs importantes

```typescript
// Sempre logar:
console.log(`[DB] Quiz saved: ${response.id} (${response.nome})`)
console.log(`[DB] Diagnosis updated: ${quizId}`)
console.log(`[DB] WhatsApp sent: ${quizId}`)
```

### Alertas

Configurar alertas no Supabase para:
- Mais de 100 requisições/min (possível ataque)
- Erros de constraint (dados inválidos)
- Storage quase cheio

---

## ✅ CHECKLIST DE SETUP

- [ ] Projeto criado no Supabase
- [ ] Variáveis de ambiente configuradas
- [ ] Tabela `quiz_responses` criada
- [ ] Índices criados
- [ ] RLS configurado
- [ ] Cliente Supabase configurado
- [ ] Queries testadas
- [ ] Backup automático ativado no Supabase

---

**Próximo:** Ver `README.md` para documentação geral do projeto.
