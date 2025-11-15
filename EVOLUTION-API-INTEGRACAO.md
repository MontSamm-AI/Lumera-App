# EVOLUTION API - INTEGRAÇÃO WHATSAPP

> **Objetivo:** Enviar diagnósticos personalizados via WhatsApp usando Evolution API
> **Versão:** MVP 1.0

---

## 📱 SOBRE A EVOLUTION API

Evolution API é uma API REST completa para WhatsApp que permite:
- Enviar mensagens de texto
- Enviar documentos (PDF, DOCX, etc)
- Enviar imagens, áudios e vídeos
- Validar números de WhatsApp
- Receber webhooks de mensagens
- Gerenciar instâncias do WhatsApp

**Repositório:** https://github.com/EvolutionAPI/evolution-api
**Documentação:** https://doc.evolution-api.com

---

## 🔧 SETUP INICIAL

### 1. Variáveis de Ambiente

```env
# .env.local
EVOLUTION_API_URL=https://sua-instancia.evolution-api.com
EVOLUTION_API_KEY=sua-api-key-aqui
EVOLUTION_INSTANCE_NAME=lumera-app
```

### 2. Cliente Evolution API

```typescript
// lib/whatsapp/evolution-api.ts
const EVOLUTION_API_URL = process.env.EVOLUTION_API_URL!
const API_KEY = process.env.EVOLUTION_API_KEY!
const INSTANCE = process.env.EVOLUTION_INSTANCE_NAME!

export class EvolutionAPI {
  private headers = {
    'Content-Type': 'application/json',
    'apikey': API_KEY,
  }

  /**
   * Validar se número existe no WhatsApp
   */
  async validateNumber(number: string): Promise<boolean> {
    try {
      const cleanNumber = this.cleanPhoneNumber(number)

      const response = await fetch(
        `${EVOLUTION_API_URL}/chat/whatsappNumbers/${INSTANCE}`,
        {
          method: 'POST',
          headers: this.headers,
          body: JSON.stringify({
            numbers: [cleanNumber],
          }),
        }
      )

      const data = await response.json()
      return data?.[0]?.exists === true
    } catch (error) {
      console.error('Error validating WhatsApp number:', error)
      return false
    }
  }

  /**
   * Enviar mensagem de texto
   */
  async sendText(params: {
    number: string
    text: string
  }): Promise<{ success: boolean; messageId?: string }> {
    try {
      const cleanNumber = this.cleanPhoneNumber(params.number)

      const response = await fetch(
        `${EVOLUTION_API_URL}/message/sendText/${INSTANCE}`,
        {
          method: 'POST',
          headers: this.headers,
          body: JSON.stringify({
            number: cleanNumber,
            text: params.text,
            delay: 1200, // delay de 1.2s para parecer mais humano
          }),
        }
      )

      const data = await response.json()

      return {
        success: response.ok,
        messageId: data.key?.id,
      }
    } catch (error) {
      console.error('Error sending text:', error)
      return { success: false }
    }
  }

  /**
   * Enviar documento (PDF)
   */
  async sendDocument(params: {
    number: string
    media: string // base64 ou URL
    filename: string
    caption?: string
  }): Promise<{ success: boolean; messageId?: string }> {
    try {
      const cleanNumber = this.cleanPhoneNumber(params.number)

      const response = await fetch(
        `${EVOLUTION_API_URL}/message/sendMedia/${INSTANCE}`,
        {
          method: 'POST',
          headers: this.headers,
          body: JSON.stringify({
            number: cleanNumber,
            mediatype: 'document',
            mimetype: 'application/pdf',
            caption: params.caption || '',
            fileName: params.filename,
            media: params.media,
          }),
        }
      )

      const data = await response.json()

      return {
        success: response.ok,
        messageId: data.key?.id,
      }
    } catch (error) {
      console.error('Error sending document:', error)
      return { success: false }
    }
  }

  /**
   * Enviar imagem
   */
  async sendImage(params: {
    number: string
    media: string
    caption?: string
  }): Promise<{ success: boolean }> {
    try {
      const cleanNumber = this.cleanPhoneNumber(params.number)

      const response = await fetch(
        `${EVOLUTION_API_URL}/message/sendMedia/${INSTANCE}`,
        {
          method: 'POST',
          headers: this.headers,
          body: JSON.stringify({
            number: cleanNumber,
            mediatype: 'image',
            caption: params.caption,
            media: params.media,
          }),
        }
      )

      return { success: response.ok }
    } catch (error) {
      console.error('Error sending image:', error)
      return { success: false }
    }
  }

  /**
   * Limpar número de telefone (remover caracteres especiais)
   */
  private cleanPhoneNumber(number: string): string {
    // Remove tudo exceto números
    let clean = number.replace(/\D/g, '')

    // Adiciona código do país se não tiver (Brasil = 55)
    if (!clean.startsWith('55')) {
      clean = '55' + clean
    }

    // Adiciona @s.whatsapp.net no final
    return clean + '@s.whatsapp.net'
  }

  /**
   * Formatar número para exibição
   */
  formatPhoneNumber(number: string): string {
    const clean = number.replace(/\D/g, '')
    const match = clean.match(/^(\d{2})(\d{2})(\d{5})(\d{4})$/)

    if (match) {
      return `+${match[1]} (${match[2]}) ${match[3]}-${match[4]}`
    }

    return number
  }
}

// Instância singleton
export const evolutionAPI = new EvolutionAPI()
```

---

## 📤 FLUXO COMPLETO DE ENVIO DO DIAGNÓSTICO

### API Route: Gerar e Enviar Diagnóstico

```typescript
// app/api/send-diagnosis/route.ts
import { NextResponse } from 'next/server'
import { getQuizResponse, updateDiagnosisSent } from '@/lib/db/queries'
import { generateDiagnosis } from '@/lib/ai/generate-diagnosis'
import { generateDiagnosisPDF } from '@/lib/pdf/generate-pdf'
import { evolutionAPI } from '@/lib/whatsapp/evolution-api'

export async function POST(req: Request) {
  try {
    const { quizId } = await req.json()

    console.log(`[Diagnosis] Starting for quiz: ${quizId}`)

    // 1. Buscar dados do quiz
    const quizData = await getQuizResponse(quizId)

    if (!quizData) {
      return NextResponse.json(
        { error: 'Quiz não encontrado' },
        { status: 404 }
      )
    }

    console.log(`[Diagnosis] Quiz data loaded for: ${quizData.nome}`)

    // 2. Validar WhatsApp
    const isValidWhatsApp = await evolutionAPI.validateNumber(
      quizData.whatsapp
    )

    if (!isValidWhatsApp) {
      console.error(`[Diagnosis] Invalid WhatsApp: ${quizData.whatsapp}`)
      return NextResponse.json(
        { error: 'Número de WhatsApp inválido' },
        { status: 400 }
      )
    }

    console.log(`[Diagnosis] WhatsApp validated: ${quizData.whatsapp}`)

    // 3. Gerar diagnóstico com IA
    const diagnosis = await generateDiagnosis(quizData)

    console.log(
      `[Diagnosis] AI diagnosis generated (${diagnosis.length} chars)`
    )

    // 4. Gerar PDF
    const pdfBuffer = await generateDiagnosisPDF({
      nome: quizData.nome,
      diagnosis,
    })

    const pdfBase64 = pdfBuffer.toString('base64')

    console.log('[Diagnosis] PDF generated')

    // 5. Enviar mensagem de introdução
    await evolutionAPI.sendText({
      number: quizData.whatsapp,
      text: `Olá ${quizData.nome}! 👋\n\nSou Nathalia Mazetto, e acabei de finalizar a análise das suas respostas! 🌟\n\nPreparei um *Diagnóstico LUMERA* personalizado para você, aplicando meu método proprietário ao seu caso específico.\n\nEstou enviando o PDF completo logo abaixo. 📄`,
    })

    console.log('[Diagnosis] Introduction message sent')

    // Aguarda 2 segundos (mais humano)
    await new Promise((resolve) => setTimeout(resolve, 2000))

    // 6. Enviar PDF do diagnóstico
    const pdfResult = await evolutionAPI.sendDocument({
      number: quizData.whatsapp,
      media: pdfBase64,
      filename: `Diagnostico-LUMERA-${quizData.nome.replace(/\s/g, '-')}.pdf`,
      caption: '📊 Seu Diagnóstico LUMERA Personalizado',
    })

    if (!pdfResult.success) {
      throw new Error('Falha ao enviar PDF')
    }

    console.log('[Diagnosis] PDF sent successfully')

    // Aguarda 3 segundos
    await new Promise((resolve) => setTimeout(resolve, 3000))

    // 7. Enviar mensagem com próximo passo
    await evolutionAPI.sendText({
      number: quizData.whatsapp,
      text: `${quizData.nome}, leia o diagnóstico com atenção. Ele foi criado especialmente para você! ✨\n\nSe fizer sentido e você quiser dar o próximo passo, convido você para uma *Sessão Estratégica Gratuita* comigo.\n\n🗓️ *Agende aqui:*\nhttps://calendly.com/lumera/sessao-estrategica\n\nVamos transformar clareza em ação e estagnação em estratégia! 🚀\n\n_Com propósito,_\n*Nathalia Mazetto*\nLUMERA`,
    })

    console.log('[Diagnosis] CTA message sent')

    // 8. Atualizar banco de dados
    await updateDiagnosisSent(quizId, diagnosis)

    console.log('[Diagnosis] Database updated')

    return NextResponse.json({
      success: true,
      message: 'Diagnóstico enviado com sucesso',
    })
  } catch (error) {
    console.error('[Diagnosis] Error:', error)
    return NextResponse.json(
      {
        error: 'Erro ao enviar diagnóstico',
        details: error instanceof Error ? error.message : 'Unknown error',
      },
      { status: 500 }
    )
  }
}
```

---

## 📄 GERAÇÃO DE PDF

### Biblioteca: jsPDF

```bash
npm install jspdf
```

### Código de Geração

```typescript
// lib/pdf/generate-pdf.ts
import { jsPDF } from 'jspdf'

interface GeneratePDFParams {
  nome: string
  diagnosis: string // Markdown text
}

export async function generateDiagnosisPDF(
  params: GeneratePDFParams
): Promise<Buffer> {
  const { nome, diagnosis } = params

  const doc = new jsPDF({
    orientation: 'portrait',
    unit: 'mm',
    format: 'a4',
  })

  // Cores Lumera
  const emerald = [40, 65, 56] // #284138
  const wasabi = [128, 144, 123] // #80907B
  const gold = [248, 215, 148] // #F8D794
  const noir = [17, 20, 16] // #111410

  const pageWidth = doc.internal.pageSize.getWidth()
  const pageHeight = doc.internal.pageSize.getHeight()
  const margin = 20

  // --- HEADER ---
  // Logo/Brand
  doc.setFillColor(...emerald)
  doc.rect(0, 0, pageWidth, 40, 'F')

  doc.setTextColor(255, 255, 255)
  doc.setFontSize(28)
  doc.setFont('helvetica', 'bold')
  doc.text('LUMERA', margin, 20)

  doc.setFontSize(10)
  doc.setFont('helvetica', 'normal')
  doc.text('Da Estagnação à Estratégia', margin, 28)

  // --- TÍTULO ---
  doc.setTextColor(...noir)
  doc.setFontSize(20)
  doc.setFont('helvetica', 'bold')
  doc.text('Diagnóstico Personalizado', margin, 55)

  doc.setTextColor(...wasabi)
  doc.setFontSize(12)
  doc.setFont('helvetica', 'normal')
  doc.text(`Para: ${nome}`, margin, 65)

  // --- CONTEÚDO ---
  let currentY = 80

  // Processar markdown (simplificado)
  const lines = diagnosis.split('\n')

  lines.forEach((line) => {
    // Verificar se precisa de nova página
    if (currentY > pageHeight - 30) {
      doc.addPage()
      currentY = 20
    }

    // Headers (##)
    if (line.startsWith('## ')) {
      currentY += 5
      doc.setFontSize(14)
      doc.setFont('helvetica', 'bold')
      doc.setTextColor(...emerald)
      const text = line.replace('## ', '')
      doc.text(text, margin, currentY)
      currentY += 10
      return
    }

    // Bold (**text**)
    if (line.includes('**')) {
      doc.setFontSize(10)
      doc.setFont('helvetica', 'bold')
      doc.setTextColor(...noir)
      const text = line.replace(/\*\*/g, '')
      const splitText = doc.splitTextToSize(text, pageWidth - 2 * margin)
      doc.text(splitText, margin, currentY)
      currentY += splitText.length * 5 + 3
      return
    }

    // Normal text
    if (line.trim()) {
      doc.setFontSize(10)
      doc.setFont('helvetica', 'normal')
      doc.setTextColor(...noir)
      const splitText = doc.splitTextToSize(line, pageWidth - 2 * margin)
      doc.text(splitText, margin, currentY)
      currentY += splitText.length * 5 + 3
    } else {
      currentY += 5 // Linha vazia
    }
  })

  // --- FOOTER (última página) ---
  const finalY = doc.internal.pageSize.getHeight() - 20

  doc.setDrawColor(...gold)
  doc.setLineWidth(0.5)
  doc.line(margin, finalY - 5, pageWidth - margin, finalY - 5)

  doc.setTextColor(...wasabi)
  doc.setFontSize(9)
  doc.setFont('helvetica', 'italic')
  doc.text('Com clareza e propósito,', margin, finalY)

  doc.setFont('helvetica', 'bold')
  doc.text('Nathalia Mazetto | LUMERA', margin, finalY + 5)

  // Converter para buffer
  const pdfOutput = doc.output('arraybuffer')
  return Buffer.from(pdfOutput)
}
```

---

## 🔄 WEBHOOK (Receber Mensagens) - FUTURO V2

Para quando quiser receber respostas do WhatsApp:

```typescript
// app/api/webhooks/whatsapp/route.ts
import { NextResponse } from 'next/server'

export async function POST(req: Request) {
  try {
    const body = await req.json()

    // Evento de nova mensagem
    if (body.event === 'messages.upsert') {
      const message = body.data

      const from = message.key.remoteJid.replace('@s.whatsapp.net', '')
      const text = message.message?.conversation || ''

      console.log(`[Webhook] Message from ${from}: ${text}`)

      // Aqui você pode:
      // 1. Buscar lead no banco pelo número
      // 2. Registrar interação
      // 3. Responder automaticamente
      // 4. Notificar Nathalia via email/SMS
    }

    return NextResponse.json({ success: true })
  } catch (error) {
    console.error('[Webhook] Error:', error)
    return NextResponse.json({ success: false }, { status: 500 })
  }
}
```

**Configurar webhook na Evolution API:**
```bash
POST /webhook/set/{instance}
{
  "url": "https://lumera.app/api/webhooks/whatsapp",
  "webhook_by_events": true,
  "webhook_base64": false,
  "events": [
    "MESSAGES_UPSERT",
    "MESSAGES_UPDATE",
    "SEND_MESSAGE"
  ]
}
```

---

## 🧪 TESTES

### Script de Teste

```typescript
// scripts/test-whatsapp.ts
import { evolutionAPI } from '@/lib/whatsapp/evolution-api'

async function testWhatsAppIntegration() {
  const testNumber = '5511999999999' // Seu número de teste

  console.log('1. Validando número...')
  const isValid = await evolutionAPI.validateNumber(testNumber)
  console.log(`   Válido: ${isValid}`)

  if (!isValid) {
    console.error('❌ Número inválido! Abortando.')
    return
  }

  console.log('\n2. Enviando mensagem de texto...')
  const textResult = await evolutionAPI.sendText({
    number: testNumber,
    text: 'Teste de integração Lumera App! 🌟',
  })
  console.log(`   Sucesso: ${textResult.success}`)
  console.log(`   Message ID: ${textResult.messageId}`)

  console.log('\n3. Enviando PDF de teste...')
  const pdfResult = await evolutionAPI.sendDocument({
    number: testNumber,
    media: 'https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf',
    filename: 'teste.pdf',
    caption: 'PDF de teste 📄',
  })
  console.log(`   Sucesso: ${pdfResult.success}`)

  console.log('\n✅ Testes concluídos!')
}

testWhatsAppIntegration()
```

Rodar:
```bash
ts-node scripts/test-whatsapp.ts
```

---

## ⚠️ TRATAMENTO DE ERROS

### Possíveis Erros e Soluções

#### 1. Número inválido
```typescript
if (!isValidWhatsApp) {
  // Salvar no banco com status "whatsapp_invalid"
  // Enviar email para o lead
  // Notificar Nathalia para contato manual
}
```

#### 2. Falha no envio
```typescript
try {
  await evolutionAPI.sendDocument(...)
} catch (error) {
  // Tentar novamente após 30 segundos
  // Limite de 3 tentativas
  // Se falhar, salvar em fila de "retry"
}
```

#### 3. Rate limiting
```typescript
// Adicionar delays entre mensagens
await sleep(2000)

// Usar fila com Bull/BullMQ para gerenciar envios
```

---

## 📊 MÉTRICAS E LOGS

### O que logar:

```typescript
// Sucesso
console.log(`[WhatsApp] Diagnosis sent to ${nome} (${whatsapp})`)

// Validação
console.log(`[WhatsApp] Number validated: ${whatsapp}`)

// Erro
console.error(`[WhatsApp] Failed to send to ${whatsapp}:`, error)

// Performance
console.log(`[WhatsApp] Total time: ${endTime - startTime}ms`)
```

### Salvar no banco:

```sql
-- Adicionar campos para tracking
ALTER TABLE quiz_responses ADD COLUMN whatsapp_validated BOOLEAN;
ALTER TABLE quiz_responses ADD COLUMN whatsapp_message_id TEXT;
ALTER TABLE quiz_responses ADD COLUMN whatsapp_sent_at TIMESTAMP;
ALTER TABLE quiz_responses ADD COLUMN whatsapp_error TEXT;
```

---

## 🚀 CHECKLIST DE IMPLEMENTAÇÃO

- [ ] Variáveis de ambiente configuradas
- [ ] Cliente Evolution API implementado
- [ ] Função de validação de número funcional
- [ ] Função de envio de texto funcional
- [ ] Função de envio de PDF funcional
- [ ] Geração de PDF com jsPDF implementada
- [ ] API route `/api/send-diagnosis` criada
- [ ] Trigger automático após quiz implementado
- [ ] Tratamento de erros robusto
- [ ] Logs completos
- [ ] Testes com número real realizados
- [ ] Delays entre mensagens configurados
- [ ] Formatação de mensagens validada
- [ ] Campos no banco atualizados

---

**Próximo:** Ver `PROMPT-IA-DIAGNOSTICO.md` para entender como a IA gera o conteúdo do diagnóstico.
