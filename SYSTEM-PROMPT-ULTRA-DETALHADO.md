# SYSTEM PROMPT ULTRA DETALHADO - LUMERA APP MVP

> **Para:** Google AI Studio / Lovable / Desenvolvedor IA
> **Versão:** 2.0 - MVP Focado
> **Nível de Detalhe:** MÁXIMO (códigos completos, textos exatos, posicionamento pixel-perfect)

---

## 🎯 CONTEXTO E OBJETIVO

Você vai construir o **Lumera App MVP** - uma landing page premium + quiz estratégico para Nathalia Mazetto.

**Nathalia Mazetto** é mentora de propósito e consultora estratégica que criou o **Método LUMERA** para transformar empreendedoras estagnadas em líderes estratégicas.

**LUMERA** = do latim *lumen* (luz) + *era* (novo tempo)
**Posicionamento:** "Da Estagnação à Estratégia"

---

## 🎨 PALETA DE CORES (CÓDIGOS EXATOS)

```typescript
// tailwind.config.ts
export default {
  theme: {
    extend: {
      colors: {
        lumera: {
          // Emerald Green - AUTORIDADE (uso em CTAs, headers, ícones principais)
          emerald: {
            DEFAULT: '#284138',
            50: '#E8F0ED',
            100: '#D1E1DB',
            500: '#284138',
            600: '#1F332D',
            900: '#0F1916',
          },
          // Wasabi - SERENIDADE (backgrounds, cards, borders suaves)
          wasabi: {
            DEFAULT: '#80907B',
            50: '#F2F4F1',
            100: '#E5E9E3',
            500: '#80907B',
            600: '#6A7966',
          },
          // Creased Khari - LUZ (destaques, progresso, acentos)
          gold: {
            DEFAULT: '#F8D794',
            50: '#FEFBF5',
            100: '#FDF7EB',
            500: '#F8D794',
            600: '#F5CA75',
          },
          // Egyptian Earth - AÇÃO (CTAs secundários, links importantes)
          earth: {
            DEFAULT: '#BB6830',
            50: '#F9EDE5',
            100: '#F3DBCB',
            500: '#BB6830',
            600: '#A35726',
          },
          // Noir de Vigne - PREMIUM (textos, títulos, contraste)
          noir: {
            DEFAULT: '#111410',
            50: '#F5F5F5',
            500: '#111410',
            600: '#0D0F0C',
          },
        },
      },
      fontFamily: {
        display: ['Cormorant Garamond', 'serif'],
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
}
```

---

## 📏 TIPOGRAFIA E ESPAÇAMENTO

```css
/* globals.css */
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;600;700&family=Inter:wght@300;400;500;600;700&display=swap');

:root {
  --font-display: 'Cormorant Garamond', serif;
  --font-sans: 'Inter', sans-serif;
}

/* Heading Styles */
.heading-1 {
  font-family: var(--font-display);
  font-size: 3.75rem; /* 60px */
  line-height: 1.1;
  font-weight: 600;
  letter-spacing: -0.02em;
  color: #111410;
}

.heading-2 {
  font-family: var(--font-display);
  font-size: 3rem; /* 48px */
  line-height: 1.2;
  font-weight: 600;
  color: #111410;
}

.heading-3 {
  font-family: var(--font-display);
  font-size: 2.25rem; /* 36px */
  line-height: 1.3;
  font-weight: 600;
  color: #111410;
}

/* Body Styles */
.body-large {
  font-family: var(--font-sans);
  font-size: 1.25rem; /* 20px */
  line-height: 1.75;
  color: #284138;
}

.body-regular {
  font-family: var(--font-sans);
  font-size: 1rem; /* 16px */
  line-height: 1.75;
  color: #111410;
}

/* Labels */
.label {
  font-family: var(--font-sans);
  font-size: 0.875rem; /* 14px */
  line-height: 1.5;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #80907B;
}
```

---

## 🏗️ ESTRUTURA DE COMPONENTES BASE

### Button Component (EXATO)

```tsx
// components/ui/Button.tsx
import { ButtonHTMLAttributes, forwardRef } from 'react'
import { motion } from 'framer-motion'
import { cn } from '@/lib/utils'

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'md' | 'lg'
  children: React.ReactNode
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ variant = 'primary', size = 'md', className, children, ...props }, ref) => {
    const baseStyles = 'inline-flex items-center justify-center rounded-lg font-sans font-medium transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-offset-2'

    const variants = {
      primary: 'bg-lumera-emerald text-white hover:bg-lumera-emerald-600 focus:ring-lumera-emerald shadow-lg hover:shadow-xl hover:-translate-y-0.5',
      secondary: 'bg-lumera-earth text-white hover:bg-lumera-earth-600 focus:ring-lumera-earth shadow-md hover:shadow-lg',
      outline: 'border-2 border-lumera-emerald text-lumera-emerald hover:bg-lumera-emerald hover:text-white focus:ring-lumera-emerald',
    }

    const sizes = {
      sm: 'px-4 py-2 text-sm',
      md: 'px-6 py-3 text-base',
      lg: 'px-8 py-4 text-lg',
    }

    return (
      <motion.button
        ref={ref}
        whileHover={{ scale: 1.02 }}
        whileTap={{ scale: 0.98 }}
        className={cn(baseStyles, variants[variant], sizes[size], className)}
        {...props}
      >
        {children}
      </motion.button>
    )
  }
)
```

### Input Component (EXATO)

```tsx
// components/ui/Input.tsx
import { InputHTMLAttributes, forwardRef } from 'react'
import { cn } from '@/lib/utils'

interface InputProps extends InputHTMLAttributes<HTMLInputElement> {
  label?: string
  error?: string
  helperText?: string
}

export const Input = forwardRef<HTMLInputElement, InputProps>(
  ({ label, error, helperText, className, ...props }, ref) => {
    return (
      <div className="w-full">
        {label && (
          <label className="label block mb-2">
            {label}
          </label>
        )}
        <input
          ref={ref}
          className={cn(
            'w-full px-4 py-3 rounded-lg border-2 font-sans',
            'transition-all duration-200',
            'focus:outline-none focus:ring-2 focus:ring-offset-1',
            error
              ? 'border-red-400 focus:border-red-500 focus:ring-red-200'
              : 'border-lumera-wasabi-100 focus:border-lumera-emerald focus:ring-lumera-emerald/20',
            'placeholder:text-lumera-wasabi',
            className
          )}
          {...props}
        />
        {error && (
          <p className="mt-1 text-sm text-red-600">{error}</p>
        )}
        {helperText && !error && (
          <p className="mt-1 text-sm text-lumera-wasabi">{helperText}</p>
        )}
      </div>
    )
  }
)
```

---

## 📄 LANDING PAGE - ESTRUTURA COMPLETA

### 1. HERO SECTION (CÓDIGO COMPLETO)

```tsx
// app/(marketing)/_components/Hero.tsx
'use client'

import { motion } from 'framer-motion'
import { Button } from '@/components/ui/Button'
import { ArrowRight, Sparkles } from 'lucide-react'
import Link from 'next/link'

export function Hero() {
  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      {/* Background Gradient */}
      <div className="absolute inset-0 bg-gradient-to-br from-white via-lumera-wasabi-50 to-lumera-gold-50 opacity-60" />

      {/* Decorative Elements */}
      <div className="absolute top-20 right-10 w-72 h-72 bg-lumera-gold/10 rounded-full blur-3xl" />
      <div className="absolute bottom-20 left-10 w-96 h-96 bg-lumera-emerald/5 rounded-full blur-3xl" />

      {/* Content Container */}
      <div className="relative z-10 container mx-auto px-6 lg:px-12 max-w-7xl">
        <div className="grid lg:grid-cols-2 gap-12 items-center">
          {/* Left Column - Text */}
          <motion.div
            initial={{ opacity: 0, y: 30 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.8, ease: 'easeOut' }}
            className="space-y-8"
          >
            {/* Badge */}
            <motion.div
              initial={{ opacity: 0, scale: 0.8 }}
              animate={{ opacity: 1, scale: 1 }}
              transition={{ delay: 0.2, duration: 0.5 }}
              className="inline-flex items-center gap-2 px-4 py-2 bg-lumera-gold/20 border border-lumera-gold rounded-full"
            >
              <Sparkles className="w-4 h-4 text-lumera-earth" />
              <span className="text-sm font-medium text-lumera-noir">
                Método LUMERA
              </span>
            </motion.div>

            {/* Main Heading */}
            <div>
              <motion.h1
                initial={{ opacity: 0, y: 20 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ delay: 0.3, duration: 0.8 }}
                className="heading-1 mb-4"
              >
                Da Estagnação
                <br />
                <span className="text-lumera-emerald">à Estratégia</span>
              </motion.h1>

              <motion.p
                initial={{ opacity: 0, y: 20 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ delay: 0.4, duration: 0.8 }}
                className="body-large text-lumera-noir/80 max-w-xl"
              >
                Guio empreendedoras inconformadas com seu resultado atual a
                transformarem clareza em direção, propósito em estratégia,
                e esforço em resultado sustentável.
              </motion.p>
            </div>

            {/* CTA Buttons */}
            <motion.div
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: 0.5, duration: 0.8 }}
              className="flex flex-col sm:flex-row gap-4"
            >
              <Link href="/quiz">
                <Button size="lg" className="group">
                  Fazer Diagnóstico Gratuito
                  <ArrowRight className="ml-2 w-5 h-5 group-hover:translate-x-1 transition-transform" />
                </Button>
              </Link>

              <Button variant="outline" size="lg">
                Conhecer o Método
              </Button>
            </motion.div>

            {/* Social Proof Mini */}
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ delay: 0.6, duration: 0.8 }}
              className="flex items-center gap-6 pt-8 border-t border-lumera-wasabi-100"
            >
              <div>
                <p className="text-2xl font-bold text-lumera-emerald">6</p>
                <p className="text-sm text-lumera-wasabi">Pilares LUMERA</p>
              </div>
              <div className="w-px h-12 bg-lumera-wasabi-100" />
              <div>
                <p className="text-2xl font-bold text-lumera-emerald">100%</p>
                <p className="text-sm text-lumera-wasabi">Personalizado</p>
              </div>
              <div className="w-px h-12 bg-lumera-wasabi-100" />
              <div>
                <p className="text-2xl font-bold text-lumera-emerald">Gratuito</p>
                <p className="text-sm text-lumera-wasabi">Diagnóstico</p>
              </div>
            </motion.div>
          </motion.div>

          {/* Right Column - Image/Illustration */}
          <motion.div
            initial={{ opacity: 0, scale: 0.9 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ delay: 0.4, duration: 1 }}
            className="relative hidden lg:block"
          >
            {/* Placeholder para imagem da Nathalia ou ilustração */}
            <div className="relative aspect-square rounded-3xl overflow-hidden">
              <div className="absolute inset-0 bg-gradient-to-br from-lumera-emerald/20 via-lumera-wasabi/20 to-lumera-gold/30" />

              {/* Círculos decorativos */}
              <motion.div
                animate={{ rotate: 360 }}
                transition={{ duration: 20, repeat: Infinity, ease: 'linear' }}
                className="absolute top-10 right-10 w-32 h-32 border-2 border-lumera-gold rounded-full"
              />
              <motion.div
                animate={{ rotate: -360 }}
                transition={{ duration: 25, repeat: Infinity, ease: 'linear' }}
                className="absolute bottom-20 left-20 w-24 h-24 border-2 border-lumera-emerald rounded-full"
              />

              {/* Aqui vai a imagem real */}
              {/* <Image src="/nathalia-hero.jpg" alt="Nathalia Mazetto" fill className="object-cover" /> */}
            </div>

            {/* Card flutuante */}
            <motion.div
              initial={{ y: 20, opacity: 0 }}
              animate={{ y: 0, opacity: 1 }}
              transition={{ delay: 1, duration: 0.8 }}
              className="absolute -bottom-6 -left-6 bg-white p-6 rounded-2xl shadow-2xl max-w-xs"
            >
              <p className="text-sm font-medium text-lumera-emerald mb-2">
                Transformação Real
              </p>
              <p className="text-xs text-lumera-noir/70">
                "Clareza de propósito traduzida em resultados sustentáveis"
              </p>
            </motion.div>
          </motion.div>
        </div>
      </div>

      {/* Scroll Indicator */}
      <motion.div
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ delay: 1, duration: 1 }}
        className="absolute bottom-10 left-1/2 -translate-x-1/2"
      >
        <motion.div
          animate={{ y: [0, 10, 0] }}
          transition={{ duration: 2, repeat: Infinity }}
          className="w-6 h-10 border-2 border-lumera-emerald rounded-full flex items-start justify-center p-2"
        >
          <motion.div className="w-1.5 h-2 bg-lumera-emerald rounded-full" />
        </motion.div>
      </motion.div>
    </section>
  )
}
```

---

### 2. SOBRE NATHALIA SECTION

```tsx
// app/(marketing)/_components/AboutNathalia.tsx
'use client'

import { motion } from 'framer-motion'
import { useInView } from 'framer-motion'
import { useRef } from 'react'
import Image from 'next/image'
import { Sparkles, Heart, Target } from 'lucide-react'

export function AboutNathalia() {
  const ref = useRef(null)
  const isInView = useInView(ref, { once: true, margin: '-100px' })

  return (
    <section ref={ref} className="py-24 bg-white">
      <div className="container mx-auto px-6 lg:px-12 max-w-7xl">
        <div className="grid lg:grid-cols-2 gap-16 items-center">
          {/* Left - Image */}
          <motion.div
            initial={{ opacity: 0, x: -50 }}
            animate={isInView ? { opacity: 1, x: 0 } : {}}
            transition={{ duration: 0.8 }}
            className="relative"
          >
            <div className="relative aspect-[3/4] rounded-3xl overflow-hidden">
              {/* Background decorativo */}
              <div className="absolute inset-0 bg-gradient-to-br from-lumera-emerald/10 to-lumera-wasabi/20" />

              {/* Placeholder para foto */}
              {/* <Image src="/nathalia-about.jpg" alt="Nathalia Mazetto" fill className="object-cover" /> */}

              {/* Cards de valor flutuantes */}
              <motion.div
                initial={{ scale: 0 }}
                animate={isInView ? { scale: 1 } : {}}
                transition={{ delay: 0.5, type: 'spring' }}
                className="absolute top-8 -right-4 bg-white p-4 rounded-2xl shadow-xl"
              >
                <div className="flex items-center gap-3">
                  <div className="w-10 h-10 bg-lumera-gold/20 rounded-full flex items-center justify-center">
                    <Sparkles className="w-5 h-5 text-lumera-earth" />
                  </div>
                  <div>
                    <p className="text-xs text-lumera-wasabi">Método</p>
                    <p className="text-sm font-bold text-lumera-noir">LUMERA</p>
                  </div>
                </div>
              </motion.div>
            </div>
          </motion.div>

          {/* Right - Content */}
          <motion.div
            initial={{ opacity: 0, x: 50 }}
            animate={isInView ? { opacity: 1, x: 0 } : {}}
            transition={{ duration: 0.8, delay: 0.2 }}
            className="space-y-6"
          >
            <div>
              <p className="label text-lumera-emerald mb-2">Quem sou</p>
              <h2 className="heading-2 mb-4">
                Nathalia Mazetto
              </h2>
              <p className="body-regular text-lumera-noir/80 mb-4">
                Mentora de Propósito e Consultora Estratégica
              </p>
            </div>

            <div className="space-y-4">
              <p className="body-regular">
                Ajudo empreendedoras a reconectarem-se com seu propósito e
                expressarem sua essência com clareza, beleza e autenticidade.
              </p>

              <p className="body-regular">
                Acredito que quando corpo, mente e propósito se alinham, nasce
                uma comunicação autêntica e uma energia magnética. Minha missão
                é transformar estagnação em estratégia, através do{' '}
                <span className="font-semibold text-lumera-emerald">
                  Método LUMERA
                </span>
                .
              </p>
            </div>

            {/* Valores */}
            <div className="grid grid-cols-1 gap-4 pt-6">
              {[
                {
                  icon: Heart,
                  title: 'Autenticidade',
                  description: 'Ser verdadeiro acima de aparências',
                },
                {
                  icon: Sparkles,
                  title: 'Clareza',
                  description: 'Luz sobre confusão e dispersão',
                },
                {
                  icon: Target,
                  title: 'Propósito',
                  description: 'Conexão com essência e missão',
                },
              ].map((value, index) => (
                <motion.div
                  key={value.title}
                  initial={{ opacity: 0, y: 20 }}
                  animate={isInView ? { opacity: 1, y: 0 } : {}}
                  transition={{ delay: 0.4 + index * 0.1 }}
                  className="flex items-start gap-4 p-4 rounded-xl bg-lumera-wasabi-50 border border-lumera-wasabi-100"
                >
                  <div className="w-10 h-10 bg-lumera-emerald rounded-lg flex items-center justify-center flex-shrink-0">
                    <value.icon className="w-5 h-5 text-white" />
                  </div>
                  <div>
                    <h4 className="font-semibold text-lumera-noir mb-1">
                      {value.title}
                    </h4>
                    <p className="text-sm text-lumera-noir/70">
                      {value.description}
                    </p>
                  </div>
                </motion.div>
              ))}
            </div>
          </motion.div>
        </div>
      </div>
    </section>
  )
}
```

---

### 3. MÉTODO LUMERA SECTION

```tsx
// app/(marketing)/_components/MetodoLumera.tsx
'use client'

import { motion } from 'framer-motion'
import { useInView } from 'framer-motion'
import { useRef } from 'react'
import {
  Lightbulb,
  Layers,
  Zap,
  Building2,
  Trophy,
  Target,
} from 'lucide-react'

const pillars = [
  {
    letter: 'L',
    title: 'Luz e Propósito',
    subtitle: 'Clareza',
    description: 'Definir posicionamento central, identificar missão e valores, clarear visão de negócio.',
    icon: Lightbulb,
    color: 'from-lumera-gold to-lumera-gold-600',
  },
  {
    letter: 'U',
    title: 'Unificação',
    subtitle: 'Estratégia',
    description: 'Unir serviços em jornada lógica, integrar essência e oferta, alinhar propósito e produto.',
    icon: Layers,
    color: 'from-lumera-emerald to-lumera-emerald-600',
  },
  {
    letter: 'M',
    title: 'Movimento',
    subtitle: 'Ação e Foco',
    description: 'Criar plano operacional, priorizar atividades estratégicas, eliminar dispersão.',
    icon: Zap,
    color: 'from-lumera-earth to-lumera-earth-600',
  },
  {
    letter: 'E',
    title: 'Estrutura',
    subtitle: 'Base de Crescimento',
    description: 'Desenhar modelo de negócio escalável, documentar processos, construir métricas.',
    icon: Building2,
    color: 'from-lumera-wasabi to-lumera-wasabi-600',
  },
  {
    letter: 'R',
    title: 'Reconhecimento',
    subtitle: 'Posicionamento',
    description: 'Reforçar autoridade, criar conteúdo estratégico, demonstrar diferencial.',
    icon: Trophy,
    color: 'from-lumera-emerald to-lumera-emerald-600',
  },
  {
    letter: 'A',
    title: 'Alinhamento',
    subtitle: 'Expansão',
    description: 'Manter rotina estratégica, revisar resultados, sustentar crescimento com leveza.',
    icon: Target,
    color: 'from-lumera-gold to-lumera-gold-600',
  },
]

export function MetodoLumera() {
  const ref = useRef(null)
  const isInView = useInView(ref, { once: true, margin: '-100px' })

  return (
    <section ref={ref} className="py-24 bg-gradient-to-b from-white to-lumera-wasabi-50">
      <div className="container mx-auto px-6 lg:px-12 max-w-7xl">
        {/* Header */}
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : {}}
          transition={{ duration: 0.8 }}
          className="text-center mb-16"
        >
          <p className="label text-lumera-emerald mb-2">Framework Proprietário</p>
          <h2 className="heading-2 mb-4">Método LUMERA</h2>
          <p className="body-large text-lumera-noir/80 max-w-2xl mx-auto">
            Seis pilares que transformam estagnação em estratégia,
            clareza em ação, propósito em resultado.
          </p>
        </motion.div>

        {/* Pills Grid */}
        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          {pillars.map((pillar, index) => (
            <motion.div
              key={pillar.letter}
              initial={{ opacity: 0, y: 50 }}
              animate={isInView ? { opacity: 1, y: 0 } : {}}
              transition={{ delay: 0.1 * index, duration: 0.6 }}
              whileHover={{ y: -8, transition: { duration: 0.2 } }}
              className="group relative"
            >
              <div className="bg-white rounded-2xl p-8 shadow-lg border border-lumera-wasabi-100 hover:shadow-2xl transition-all duration-300 h-full">
                {/* Letter Badge */}
                <div className={`inline-flex items-center justify-center w-14 h-14 rounded-xl bg-gradient-to-br ${pillar.color} mb-6`}>
                  <span className="text-2xl font-bold text-white">
                    {pillar.letter}
                  </span>
                </div>

                {/* Icon */}
                <pillar.icon className="w-8 h-8 text-lumera-emerald mb-4" />

                {/* Title */}
                <h3 className="heading-3 text-2xl mb-2">{pillar.title}</h3>
                <p className="label text-lumera-earth mb-4">{pillar.subtitle}</p>

                {/* Description */}
                <p className="body-regular text-sm text-lumera-noir/70">
                  {pillar.description}
                </p>

                {/* Decorative Line */}
                <div className="absolute bottom-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-lumera-gold to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300" />
              </div>
            </motion.div>
          ))}
        </div>

        {/* CTA Bottom */}
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : {}}
          transition={{ delay: 0.8, duration: 0.8 }}
          className="text-center mt-16"
        >
          <p className="body-regular text-lumera-noir/80 mb-6">
            Quer descobrir como aplicar o Método LUMERA ao seu negócio?
          </p>
          <Button size="lg">
            Fazer Diagnóstico Personalizado Gratuito
          </Button>
        </motion.div>
      </div>
    </section>
  )
}
```

---

### 4. COMO FUNCIONA SECTION

```tsx
// app/(marketing)/_components/ComoFunciona.tsx
'use client'

import { motion } from 'framer-motion'
import { useInView } from 'framer-motion'
import { useRef } from 'react'
import { ClipboardList, Sparkles, Calendar } from 'lucide-react'

const steps = [
  {
    number: '01',
    icon: ClipboardList,
    title: 'Faça o Quiz Diagnóstico',
    description:
      'Responda 8 perguntas estratégicas sobre seu negócio, desafios e objetivos. Leva apenas 3 minutos.',
    color: 'bg-lumera-emerald',
  },
  {
    number: '02',
    icon: Sparkles,
    title: 'Receba seu Diagnóstico',
    description:
      'Em até 5 minutos, você recebe no WhatsApp um diagnóstico personalizado aplicando o Método LUMERA ao seu caso.',
    color: 'bg-lumera-gold',
  },
  {
    number: '03',
    icon: Calendar,
    title: 'Agende sua Sessão Gratuita',
    description:
      'Se fizer sentido, agendamos uma Sessão Estratégica onde traçamos juntas o plano de ação para sua transformação.',
    color: 'bg-lumera-earth',
  },
]

export function ComoFunciona() {
  const ref = useRef(null)
  const isInView = useInView(ref, { once: true, margin: '-100px' })

  return (
    <section ref={ref} className="py-24 bg-white">
      <div className="container mx-auto px-6 lg:px-12 max-w-7xl">
        {/* Header */}
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : {}}
          className="text-center mb-16"
        >
          <p className="label text-lumera-emerald mb-2">Processo Simples</p>
          <h2 className="heading-2 mb-4">Como Funciona</h2>
          <p className="body-large text-lumera-noir/80 max-w-2xl mx-auto">
            Três passos simples para começar sua jornada de transformação
          </p>
        </motion.div>

        {/* Steps */}
        <div className="relative">
          {/* Connecting Line (desktop) */}
          <div className="hidden lg:block absolute top-20 left-0 right-0 h-0.5 bg-gradient-to-r from-lumera-emerald via-lumera-gold to-lumera-earth opacity-20" />

          <div className="grid md:grid-cols-3 gap-12 relative">
            {steps.map((step, index) => (
              <motion.div
                key={step.number}
                initial={{ opacity: 0, y: 50 }}
                animate={isInView ? { opacity: 1, y: 0 } : {}}
                transition={{ delay: 0.2 * index, duration: 0.6 }}
                className="relative"
              >
                {/* Number Badge */}
                <motion.div
                  whileHover={{ scale: 1.1, rotate: 5 }}
                  className="absolute -top-4 -left-4 w-16 h-16 bg-white border-4 border-lumera-wasabi-100 rounded-full flex items-center justify-center shadow-lg z-10"
                >
                  <span className="text-2xl font-bold text-lumera-emerald">
                    {step.number}
                  </span>
                </motion.div>

                {/* Card */}
                <div className="bg-lumera-wasabi-50 rounded-2xl p-8 pt-12 h-full border border-lumera-wasabi-100">
                  {/* Icon */}
                  <div className={`inline-flex items-center justify-center w-14 h-14 ${step.color} rounded-xl mb-6`}>
                    <step.icon className="w-7 h-7 text-white" />
                  </div>

                  {/* Title */}
                  <h3 className="heading-3 text-xl mb-4">{step.title}</h3>

                  {/* Description */}
                  <p className="body-regular text-sm text-lumera-noir/70">
                    {step.description}
                  </p>
                </div>

                {/* Arrow (desktop) */}
                {index < steps.length - 1 && (
                  <div className="hidden lg:block absolute top-20 -right-6 text-lumera-wasabi opacity-40">
                    →
                  </div>
                )}
              </motion.div>
            ))}
          </div>
        </div>

        {/* CTA */}
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : {}}
          transition={{ delay: 0.8 }}
          className="text-center mt-16"
        >
          <Button size="lg">Começar Agora - É Gratuito</Button>
        </motion.div>
      </div>
    </section>
  )
}
```

---

## 📝 QUIZ - ESTRUTURA COMPLETA

### Quiz Page (Multi-Step)

```tsx
// app/quiz/page.tsx
'use client'

import { useState } from 'react'
import { motion, AnimatePresence } from 'framer-motion'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'
import { QuizProgress } from './_components/QuizProgress'
import { QuestionCard } from './_components/QuestionCard'
import { Button } from '@/components/ui/Button'
import { ArrowLeft, ArrowRight } from 'lucide-react'

// Schema de validação
const quizSchema = z.object({
  nome: z.string().min(2, 'Nome muito curto'),
  whatsapp: z.string().regex(
    /^(\+?55\s?)?(\(?\d{2}\)?\s?)?\d{4,5}-?\d{4}$/,
    'WhatsApp inválido'
  ),
  email: z.string().email('Email inválido').optional(),
  tipoNegocio: z.enum(['Serviços', 'Produtos Físicos', 'Infoprodutos']),
  faturamento: z.enum([
    'Ainda não faturo',
    'Menos de R$ 1.000',
    'R$ 1.000 a R$ 3.000',
    'R$ 3.001 a R$ 5.000',
    'R$ 5.001 a R$ 10.000',
    'Mais de R$ 10.000',
  ]),
  principal_desafio: z.string(),
  bloqueios: z.string().min(20, 'Descreva melhor (mínimo 20 caracteres)'),
  objetivo_6_meses: z.string().min(20, 'Descreva melhor (mínimo 20 caracteres)'),
})

type QuizData = z.infer<typeof quizSchema>

export default function QuizPage() {
  const [currentStep, setCurrentStep] = useState(0)
  const [isSubmitting, setIsSubmitting] = useState(false)

  const {
    register,
    handleSubmit,
    formState: { errors },
    trigger,
    watch,
  } = useForm<QuizData>({
    resolver: zodResolver(quizSchema),
    mode: 'onBlur',
  })

  const questions = [
    {
      id: 'nome',
      type: 'text',
      label: 'Qual é o seu nome completo?',
      placeholder: 'Ex: Maria Silva',
    },
    {
      id: 'whatsapp',
      type: 'tel',
      label: 'Qual é o seu WhatsApp?',
      placeholder: '(11) 99999-9999',
      helperText: 'Seu diagnóstico será enviado aqui',
    },
    {
      id: 'email',
      type: 'email',
      label: 'Qual é o seu e-mail?',
      placeholder: 'seu@email.com',
      helperText: 'Opcional',
    },
    {
      id: 'tipoNegocio',
      type: 'select',
      label: 'Com o que você trabalha?',
      options: ['Serviços', 'Produtos Físicos', 'Infoprodutos'],
    },
    {
      id: 'faturamento',
      type: 'select',
      label: 'Qual seu faturamento mensal atual?',
      options: [
        'Ainda não faturo',
        'Menos de R$ 1.000',
        'R$ 1.000 a R$ 3.000',
        'R$ 3.001 a R$ 5.000',
        'R$ 5.001 a R$ 10.000',
        'Mais de R$ 10.000',
      ],
    },
    {
      id: 'principal_desafio',
      type: 'select',
      label: 'Qual é o seu principal desafio hoje?',
      options: [
        'Falta de clareza sobre direção',
        'Dificuldade em vender',
        'Excesso de trabalho e dispersão',
        'Posicionamento e autoridade',
        'Outro',
      ],
    },
    {
      id: 'bloqueios',
      type: 'textarea',
      label: 'O que você acredita que te impede de crescer?',
      placeholder: 'Compartilhe aqui suas percepções...',
      helperText: 'Seja sincera, quanto mais detalhe, melhor será seu diagnóstico',
    },
    {
      id: 'objetivo_6_meses',
      type: 'textarea',
      label: 'Onde você quer estar em 6 meses?',
      placeholder: 'Descreva seu objetivo ideal...',
      helperText: 'Pense grande! Onde você REALMENTE quer chegar?',
    },
  ]

  const totalSteps = questions.length
  const currentQuestion = questions[currentStep]

  const handleNext = async () => {
    const isValid = await trigger(currentQuestion.id as keyof QuizData)
    if (isValid && currentStep < totalSteps - 1) {
      setCurrentStep(currentStep + 1)
    } else if (isValid && currentStep === totalSteps - 1) {
      handleSubmit(onSubmit)()
    }
  }

  const handlePrev = () => {
    if (currentStep > 0) {
      setCurrentStep(currentStep - 1)
    }
  }

  const onSubmit = async (data: QuizData) => {
    setIsSubmitting(true)
    try {
      const response = await fetch('/api/quiz/submit', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data),
      })

      if (response.ok) {
        window.location.href = '/quiz/obrigado'
      }
    } catch (error) {
      console.error(error)
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-white via-lumera-wasabi-50 to-lumera-gold-50 flex items-center justify-center p-6">
      <div className="w-full max-w-2xl">
        {/* Progress */}
        <QuizProgress current={currentStep + 1} total={totalSteps} />

        {/* Question Card */}
        <AnimatePresence mode="wait">
          <motion.div
            key={currentStep}
            initial={{ opacity: 0, x: 50 }}
            animate={{ opacity: 1, x: 0 }}
            exit={{ opacity: 0, x: -50 }}
            transition={{ duration: 0.3 }}
          >
            <QuestionCard
              question={currentQuestion}
              register={register}
              error={errors[currentQuestion.id as keyof QuizData]?.message}
            />
          </motion.div>
        </AnimatePresence>

        {/* Navigation */}
        <div className="flex justify-between mt-8">
          <Button
            variant="outline"
            onClick={handlePrev}
            disabled={currentStep === 0}
          >
            <ArrowLeft className="w-5 h-5 mr-2" />
            Voltar
          </Button>

          <Button
            onClick={handleNext}
            disabled={isSubmitting}
          >
            {currentStep === totalSteps - 1 ? (
              isSubmitting ? 'Enviando...' : 'Finalizar'
            ) : (
              <>
                Próximo
                <ArrowRight className="w-5 h-5 ml-2" />
              </>
            )}
          </Button>
        </div>
      </div>
    </div>
  )
}
```

### Quiz Progress Component

```tsx
// app/quiz/_components/QuizProgress.tsx
import { motion } from 'framer-motion'

interface QuizProgressProps {
  current: number
  total: number
}

export function QuizProgress({ current, total }: QuizProgressProps) {
  const percentage = (current / total) * 100

  return (
    <div className="mb-12">
      {/* Step Counter */}
      <div className="flex justify-between items-center mb-3">
        <span className="text-sm font-medium text-lumera-emerald">
          Pergunta {current} de {total}
        </span>
        <span className="text-sm text-lumera-wasabi">
          {Math.round(percentage)}% completo
        </span>
      </div>

      {/* Progress Bar */}
      <div className="h-2 bg-lumera-wasabi-100 rounded-full overflow-hidden">
        <motion.div
          initial={{ width: 0 }}
          animate={{ width: `${percentage}%` }}
          transition={{ duration: 0.5, ease: 'easeOut' }}
          className="h-full bg-gradient-to-r from-lumera-gold via-lumera-emerald to-lumera-earth"
        />
      </div>
    </div>
  )
}
```

---

### Question Card Component (COMPLETO)

```tsx
// app/quiz/_components/QuestionCard.tsx
import { Input } from '@/components/ui/Input'
import { UseFormRegister, FieldErrors } from 'react-hook-form'
import { motion } from 'framer-motion'

interface QuestionCardProps {
  question: {
    id: string
    type: string
    label: string
    placeholder?: string
    helperText?: string
    options?: string[]
  }
  register: UseFormRegister<any>
  error?: string
}

export function QuestionCard({ question, register, error }: QuestionCardProps) {
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.95 }}
      animate={{ opacity: 1, scale: 1 }}
      className="bg-white rounded-3xl p-8 md:p-12 shadow-2xl border border-lumera-wasabi-100"
    >
      {/* Question Number Badge */}
      <div className="inline-flex items-center justify-center w-12 h-12 bg-gradient-to-br from-lumera-emerald to-lumera-emerald-600 rounded-xl mb-6">
        <span className="text-xl font-bold text-white">?</span>
      </div>

      {/* Question Label */}
      <h3 className="heading-3 text-2xl mb-6">
        {question.label}
      </h3>

      {/* Input Field */}
      {question.type === 'text' || question.type === 'email' || question.type === 'tel' ? (
        <Input
          type={question.type}
          placeholder={question.placeholder}
          error={error}
          helperText={question.helperText}
          {...register(question.id)}
          className="text-lg"
        />
      ) : question.type === 'textarea' ? (
        <div>
          <textarea
            placeholder={question.placeholder}
            rows={5}
            {...register(question.id)}
            className={`w-full px-4 py-3 rounded-lg border-2 font-sans text-lg transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-1 ${
              error
                ? 'border-red-400 focus:border-red-500 focus:ring-red-200'
                : 'border-lumera-wasabi-100 focus:border-lumera-emerald focus:ring-lumera-emerald/20'
            } placeholder:text-lumera-wasabi`}
          />
          {error && <p className="mt-2 text-sm text-red-600">{error}</p>}
          {question.helperText && !error && (
            <p className="mt-2 text-sm text-lumera-wasabi">{question.helperText}</p>
          )}
        </div>
      ) : question.type === 'select' ? (
        <div className="space-y-3">
          {question.options?.map((option, index) => (
            <motion.label
              key={option}
              initial={{ opacity: 0, x: -20 }}
              animate={{ opacity: 1, x: 0 }}
              transition={{ delay: 0.05 * index }}
              className="flex items-center p-4 rounded-xl border-2 border-lumera-wasabi-100 hover:border-lumera-emerald hover:bg-lumera-emerald/5 transition-all cursor-pointer group"
            >
              <input
                type="radio"
                value={option}
                {...register(question.id)}
                className="w-5 h-5 text-lumera-emerald focus:ring-lumera-emerald"
              />
              <span className="ml-3 text-base text-lumera-noir group-hover:text-lumera-emerald">
                {option}
              </span>
            </motion.label>
          ))}
          {error && <p className="mt-2 text-sm text-red-600">{error}</p>}
        </div>
      ) : null}
    </motion.div>
  )
}
```

---

### Página de Confirmação

```tsx
// app/quiz/obrigado/page.tsx
'use client'

import { motion } from 'framer-motion'
import { CheckCircle, Smartphone, Calendar } from 'lucide-react'
import { Button } from '@/components/ui/Button'
import Link from 'next/link'
import confetti from 'canvas-confetti'
import { useEffect } from 'react'

export default function ObrigadoPage() {
  useEffect(() => {
    // Confetti effect
    confetti({
      particleCount: 100,
      spread: 70,
      origin: { y: 0.6 },
      colors: ['#284138', '#80907B', '#F8D794', '#BB6830'],
    })
  }, [])

  return (
    <div className="min-h-screen bg-gradient-to-br from-white via-lumera-wasabi-50 to-lumera-gold-50 flex items-center justify-center p-6">
      <motion.div
        initial={{ opacity: 0, scale: 0.9 }}
        animate={{ opacity: 1, scale: 1 }}
        transition={{ duration: 0.5 }}
        className="max-w-2xl w-full"
      >
        <div className="bg-white rounded-3xl p-12 shadow-2xl border border-lumera-wasabi-100 text-center">
          {/* Success Icon */}
          <motion.div
            initial={{ scale: 0 }}
            animate={{ scale: 1 }}
            transition={{ delay: 0.2, type: 'spring', stiffness: 200 }}
            className="inline-flex items-center justify-center w-24 h-24 bg-gradient-to-br from-lumera-emerald to-lumera-emerald-600 rounded-full mb-8"
          >
            <CheckCircle className="w-12 h-12 text-white" />
          </motion.div>

          {/* Heading */}
          <motion.h1
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: 0.3 }}
            className="heading-2 mb-4"
          >
            Obrigada! ✨
          </motion.h1>

          <motion.p
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: 0.4 }}
            className="body-large text-lumera-noir/80 mb-8"
          >
            Suas respostas foram recebidas com sucesso.
          </motion.p>

          {/* Status Cards */}
          <motion.div
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: 0.5 }}
            className="space-y-4 mb-8"
          >
            {/* WhatsApp Card */}
            <div className="bg-lumera-emerald/5 border border-lumera-emerald/20 rounded-2xl p-6">
              <div className="flex items-start gap-4">
                <div className="w-12 h-12 bg-lumera-emerald rounded-lg flex items-center justify-center flex-shrink-0">
                  <Smartphone className="w-6 h-6 text-white" />
                </div>
                <div className="text-left">
                  <h3 className="font-bold text-lumera-noir mb-2">
                    Seu diagnóstico está sendo preparado
                  </h3>
                  <p className="text-sm text-lumera-noir/70">
                    Em até <strong>5 minutos</strong> você receberá no WhatsApp um
                    diagnóstico personalizado aplicando o Método LUMERA ao seu caso.
                  </p>
                </div>
              </div>
            </div>

            {/* Next Step Card */}
            <div className="bg-lumera-gold/10 border border-lumera-gold/30 rounded-2xl p-6">
              <div className="flex items-start gap-4">
                <div className="w-12 h-12 bg-lumera-earth rounded-lg flex items-center justify-center flex-shrink-0">
                  <Calendar className="w-6 h-6 text-white" />
                </div>
                <div className="text-left">
                  <h3 className="font-bold text-lumera-noir mb-2">
                    Próximo passo
                  </h3>
                  <p className="text-sm text-lumera-noir/70">
                    Leia seu diagnóstico com atenção e, se fizer sentido,
                    agende uma Sessão Estratégica Gratuita comigo.
                  </p>
                </div>
              </div>
            </div>
          </motion.div>

          {/* CTA */}
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 0.6 }}
            className="flex flex-col sm:flex-row gap-4 justify-center"
          >
            <Link href="/">
              <Button variant="outline" size="lg">
                Voltar ao Início
              </Button>
            </Link>

            <a
              href="https://instagram.com/nathaliamazzeto"
              target="_blank"
              rel="noopener noreferrer"
            >
              <Button variant="secondary" size="lg">
                Seguir no Instagram
              </Button>
            </a>
          </motion.div>

          {/* Footer Note */}
          <motion.p
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 0.7 }}
            className="mt-8 text-sm text-lumera-wasabi"
          >
            Com clareza e propósito, <strong>Nathalia Mazetto</strong>
          </motion.p>
        </div>
      </motion.div>
    </div>
  )
}
```

---

**Arquivo completo. Consulte também:**
- `EVOLUTION-API-INTEGRACAO.md` (integração WhatsApp)
- `PROMPT-IA-DIAGNOSTICO.md` (prompt completo da IA)
- `SUPABASE-SETUP.md` (configuração banco de dados)
- `README.md` (documentação principal do projeto)
