# Layout — Hospital 24h (VetPiera)

> Especificação exaustiva das 10 seções da página Hospital, na ordem do Petderma. Hero + Stats já implementados como demo aprovada. Compartilha tokens da home — ver `home/layout.md` para tabela completa.

---

## Design Tokens

Mesmos da home — DM Serif Display + DM Sans, paleta verde escuro #1B4D3E + dourado #C9A84C, mesh gradient backgrounds. Ver `home/layout.md` para detalhes.

**Proposta diferencial do hospital:** urgência + plantão. Sinalização visual com:
- Dot **vermelho** pulsante no eyebrow (vs. dourado da home)
- Live indicator **verde** pulsante "Aberto agora"
- Stamp dourado **"24h"** com ring branco

---

## Seção 1: HERO

### Arquétipo e Constraints
- **Arquétipo:** Split com Overlap (60/40)
- **Constraints:** Gradient Mesh (Cor) · Image Gradient (Mídia) · Pulse Loop vermelho+verde (Movimento) · Headline com Gradiente (Tipo) · Card Bleed "24h" (Layout)
- **Justificativa:** Mantém consistência com home, mas adiciona elementos de urgência (pulses vermelho e verde) específicos do hospital.

### Conteúdo
- **Eyebrow pill (dot vermelho `#d94343` pulse):** `Plantão Veterinário · Cidade Líder, SP`
- **Headline:** `Emergência veterinária [24 horas.] Aqui, seu pet nunca fica sem atendimento.` — "24 horas." em gradient italic
- **Sub:** `Hospital completo com UTI, centro cirúrgico, internação e 13 especialistas — prontos a qualquer hora do dia ou da noite.`
- **CTA primário:** `Falar agora no WhatsApp` + `ph-fill ph-whatsapp-logo` → `wa.me/5511963326376`
- **CTA secundário (telefone com ícone circular):**
  - Label: `Plantão direto`
  - Número: `(11) 2746-7292`
  - Link: `tel:+551127467292`
- **Trust strip:** UTI veterinária · Centro cirúrgico · Diagnóstico por imagem
- **Card "24h" dourado** (bottom-right da foto, rotacionado +4deg, ring branco)
- **Badge "Aberto agora"** (top-left da foto, dot verde `#1fae6a` pulsante):
  - Title: `Aberto agora`
  - Sub: `Plantão · 7 dias`

### Layout
- Container 1320px, padding `clamp(120px, 14vw, 160px) var(--pad-x) clamp(80px, 10vw, 120px)`
- Grid `60fr 40fr`, gap `clamp(40px, 6vw, 80px)`, align center
- min-height 100svh
- Photo-wrap rotate -1.5deg → 0 hover
- Stamp 24h: position absolute `bottom: -28px; right: -24px`, padding `20px 28px 18px`, radius 18px (card retangular)
- Badge "Aberto agora": `top: 24px; left: -32px`, glass pill radius 999px

### Tipografia
- Headline: DM Serif Display 400 · `clamp(2.5rem, 5.5vw, 4.5rem)` · line-height 1.04 · letter-spacing -0.025em
- Em: gradient verde→dourado italic (igual home)
- Phone label: DM Sans 500 · 0.75rem · uppercase · 0.08em · muted
- Phone num: DM Sans 700 · 1.0625rem
- Stamp num: DM Serif Display · `clamp(2.75rem, 5vw, 4rem)` · white
- Stamp unit: italic, `clamp(1.5rem, 2.5vw, 2.25rem)` · white · padding-bottom 4px

### Cores
- Mesh idêntico à home, com Orb 1 mais escuro: radial verde dark 28% top-left (vs 22% na home)
- Dot eyebrow vermelho `#d94343`, pulse 1.8s (mais rápido = sensação de plantão ativo)
- Stamp bg: `linear-gradient(135deg, #d4ab3a 0%, #C9A84C 50%, #b8922e 100%)` · text white !important
- Stamp box-shadow: `0 24px 56px -12px rgba(201,168,76,.7), 0 0 0 4px white, 0 0 0 5px rgba(201,168,76,.4)` (ring duplo)
- Badge dot verde `#1fae6a`, pulse 1.6s

### Animações
- Orbs drift, hero rotate hover, photo parallax — igual home
- Pulse vermelho eyebrow: `hospHeroPulse 1.8s` — box-shadow 0→10px
- Pulse verde live: `hospLivePulse 1.6s` — box-shadow 0→12px

### Responsividade
- **≤980px:** grid 1 coluna
- **≤640px:** headline `clamp(2.125rem, 9vw, 2.75rem)` · stamp `bottom: -12px right: -8px` · badge `left: 12px top: 12px`

---

## Seção 2: STATS BAR

### Arquétipo e Constraints
- **Arquétipo:** Type Hero Editorial (igual home, sufixado `.hosp-stats`)
- **Constraints:** Color Blocking · Counter · Stagger — idênticos à home

### Conteúdo
- **Eyebrow:** `Hospital em números`
- **Título:** `Estrutura, equipe e tempo a favor do seu pet.`
- **Stats:**
  1. **24h** (italic) · PLANTÃO · "Hospital aberto todos os dias"
  2. **13+** · EQUIPE · "Veterinários especialistas"
  3. **12** · UTI · "Vagas de internação intensiva"
  4. **22+** · TEMPO · "Anos de experiência"

### Layout / Tipografia / Animações
Idênticos à home — ver `home/layout.md` seção 2.

---

## Seção 3: SOBRE O HOSPITAL

### Arquétipo e Constraints
- **Arquétipo:** Split Alternado 50/50 (Texto + Badge / Imagem)
- **Constraints:** Imagem com Overlay (Mídia) · Badge Overlapping (Layout) · Stagger Reveal (Movimento)

### Conteúdo
- **Pre-título:** `Nosso hospital`
- **Título:** `Tecnologia, equipe e estrutura para os momentos mais difíceis.`
- **Texto 1:** `O Hospital Veterinário Piera é referência em medicina veterinária de alta complexidade na Grande São Paulo. Estamos abertos 24 horas para acolher emergências, realizar cirurgias e cuidar de cada animal como se fosse da nossa família.`
- **Texto 2:** `Contamos com UTI veterinária equipada, centro cirúrgico de ponta, internação separada por espécie e isolamento infeccioso. Uma estrutura completa que poucos hospitais oferecem.`
- **CTA:** `Conheça nossa equipe →` → âncora para `#diferenciais` ou `/quem-somos`
- **Badge:** `22+ Anos de Experiência`
- **Imagem:** `/images/hosp-exterior.jpg`

### Layout / Tipografia
- Container 1200px, grid 2 colunas gap `clamp(48px, 6vw, 80px)`, align center
- Imagem radius 24px, aspect 4/3
- Badge sticky position absolute `top: -32px; left: -32px`
- Idêntico à home seção 3

---

## Seção 4: SERVIÇOS (Bento Box assimétrico)

### Arquétipo e Constraints
- **Arquétipo:** Bento Box Assimétrico (1 card large 2×2 + 5 cards small com 3D flip)
- **Constraints:** Live tag "Disponível agora" (Interação) · 3D Flip (Interação) · Image full-bleed no large card (Mídia) · Mixed Sizes (Layout)
- **Justificativa:** Diferente da home (que tem grid 4 iguais). Hospital tem MAIS serviços para mostrar (6 vs 4) — o assimétrico permite hierarquia.

### Conteúdo
- **Pre-título / Título / Sub:**
  - "Estrutura completa para cada momento."
  - "Do pronto-atendimento ao pós-operatório — temos tudo o que seu animal precisa em um único lugar."

- **Card LARGE (2×2): Emergência & UTI** `ph-first-aid-kit`
  - Live tag "Disponível agora" (dot verde pulsando)
  - Name: "Pronto-atendimento e cuidados intensivos veterinários."
  - Desc: "Equipe de plantão 24h, UTI com monitoramento multiparamétrico contínuo, ventilação mecânica e suporte transfusional."
  - List: Triagem imediata · UTI com 12 vagas · Oxigenoterapia · Hemoterapia
  - CTA: `Saiba mais →`
  - Photo background: `/images/hospital-uti.jpg`

- **Cards SMALL (5) com 3D flip:**
  1. `ph-scalpel` **Cirurgia & Anestesia** → "Cirurgia geral · Laparoscopia · Monitoração anestésica · Recuperação"
  2. `ph-scan` **Diagnóstico por Imagem** → "Tomografia · Ultrassom · Ecocardiograma · Radiologia digital"
  3. `ph-bed` **Internação Veterinária** → "Separada por espécie · Isolamento infeccioso · Monitoramento 24h · Atualização ao tutor"
  4. `ph-stethoscope` **Consultas & Prevenção** → "Consultas de rotina · Vacinas importadas · Check-up · Orientação nutricional"
  5. `ph-test-tube` **Laboratório Próprio** → "Hemograma · Testes Rápidos · Coleta de Líquor · Análises Hormonais"

### Layout
- Container max-width 1200px
- Grid: `grid-template-columns: repeat(4, 1fr); grid-auto-rows: minmax(180px, auto)`
- Large card: `grid-column: span 2; grid-row: span 2` (ocupa 2×2)
- Small cards: 1×1 cada (5 cards preenchem o resto)
- Gap 16px

### Tipografia / Cores
- Card category: DM Sans 600 · 0.8125rem · uppercase · 0.12em · dourado + ícone Phosphor
- Card name: DM Serif Display · clamp(1.25rem, 2vw, 1.6rem) · line-height 1.15
- Card desc: DM Sans 400 · 0.95rem · line-height 1.55 · muted
- Live tag: pill bg `rgba(31,174,106,.12)` · color `#1fae6a` · dot pulsando

### Animações
- Flip: rotateY 180deg, 700ms
- Live dot pulse: 1.6s ease infinite
- Card hover: translateY(-4px) + shadow

### Responsividade
- **≤980px:** grid 2 colunas. Large card `span 2 row span 1`
- **≤520px:** grid 1 coluna, sem large

---

## Seção 5: DIFERENCIAIS (Grid 3×3 Premium)

### Arquétipo e Constraints
- **Arquétipo:** Grid Simétrico 3×3 com Icon Cards
- **Constraints:** Icon Fill (Mídia) · Clip Reveal scroll-driven (Movimento) · Stagger Wave (Movimento)
- **Justificativa:** Hospital tem 9 diferenciais (vs 4 na home) — grid 3×3 acomoda esse volume. Diferente de Editorial Rows da home (que tem só 4).

### Conteúdo
- **Pre-título / Título:** `Diferenciais que salvam vidas.`
- **Cards (9), cada com ícone Phosphor fill:**
  1. `ph-car` Estacionamento Gratuito · "Comodidade e segurança no local."
  2. `ph-buildings` Internações Exclusivas · "Áreas separadas para cães, gatos e doenças infecciosas."
  3. `ph-squares-four` Tudo em um só lugar · "Atendimento, exames, cirurgias, internação e especialidades integradas."
  4. `ph-users-three` Trabalho em Equipe · "13 veterinários com diagnósticos compartilhados."
  5. `ph-medal` Competência Garantida · "Profissionais em constante atualização técnica e acadêmica."
  6. `ph-first-aid-kit` Cirurgias de Ponta · "Neurocirurgias e cirurgias cranianas de alta complexidade."
  7. `ph-test-tube` Exames Laboratoriais · "Coleta de líquor, hemogasometria e testes hormonais imediatos."
  8. `ph-scan` Imagem de Qualidade · "EEG, Ecocardiograma, Endoscopia, RX digital e Ultrassom."
  9. `ph-cpu` Tecnologia Veterinária · "Equipamentos de última geração em todas as unidades."

### Layout
- Container max-width 1200px, padding `--sp-section`
- Grid `repeat(3, 1fr)`, gap 24px
- Card: padding `clamp(28px, 3vw, 40px)`, radius 16px, bg surface, border 1px solid border

### Tipografia / Cores
- Icon: 48×48px container radius 12px bg `--clr-primary-pale`, ícone 24px primary
- Name: DM Serif Display · clamp(1.15rem, 1.8vw, 1.35rem) · line-height 1.2
- Desc: DM Sans 400 · 0.9375rem · line-height 1.5 · muted

### Animações
- Scroll-driven clip-path reveal: cada card aparece com `clip-path inset(0 100% 0 0) → 0 0 0 0`, 800ms ease-out, delay `--card-i * 60ms`
- Fallback IO threshold 0.15

### Responsividade
- **≤900px:** grid 2 colunas
- **≤520px:** grid 1 coluna

---

## Seção 6: GALERIA — Nossa Estrutura

### Arquétipo e Constraints
- **Arquétipo:** Featured Carousel com prev/next buttons
- **Constraints:** Drag-to-Scroll (Interação) · Caption Reveal on Hover (Mídia) · Snap (Interação)
- **Justificativa:** Diferente do Scroll Horizontal puro da home (que não tem buttons). Hospital tem buttons explícitos pra navegação consciente.

### Conteúdo
- **Pre-título:** `Nossa estrutura`
- **Título:** `Ambientes preparados para salvar vidas 24 horas por dia.`
- **9 imagens com caption (já existentes):**
  1. Recepção 24h · `hosp-estrutura-recepcao.jpg`
  2. Hall de Espera · `hosp-estrutura-hall.jpg`
  3. Consultórios Modernos · `hosp-estrutura-consultorio-1.jpg`
  4. Centro Cirúrgico de Ponta · `hosp-estrutura-cirurgico-1.jpg`
  5. Sala de Emergência · `hosp-estrutura-emergencia.jpg`
  6. Radiologia Digital · `hosp-estrutura-raiox.jpg`
  7. Ultrassonografia · `hosp-estrutura-ultrassom.jpg`
  8. Internação Canina · `hosp-estrutura-internacao-caes-1.jpg`
  9. Internação Felina Exclusiva · `hosp-estrutura-internacao-felinos.jpg`

### Layout
- Header centralizado max-width 720px
- Track: flex gap 16px, transform translateX por currentPos
- Item: flex 0 0 auto, width `clamp(320px, 35vw, 480px)`, aspect 3/2, radius 16px
- Buttons prev/next: circle 48×48px, radius 50%, bg surface, shadow, hover scale 1.05

### Animações
- Track transform: 600ms ease (currentPos × itemWidth + gap)
- Caption: opacity 0→1 + translateY(16px)→0 on hover, 300ms

### Responsividade
- **≤640px:** items `100vw - 48px`, caption sempre visível

---

## Seção 7: ESPECIALIDADES DISPONÍVEIS NO HOSPITAL

### Arquétipo e Constraints
- **Arquétipo:** Kinetic Type Strip — chips infinitos com auto-scroll
- **Constraints:** Infinite Loop (Movimento) · Drag-to-Scroll (Interação) · Fade Edges (Mídia)
- **Justificativa:** 20 especialidades não cabem em grid sem ficar denso demais. Strip horizontal com loop infinito CSS-only = ritmo único.

### Conteúdo
- **Pre-título:** `20+ especialidades` (com ícone)
- **Título:** `Especialidades disponíveis.`
- **Sub:** `Nossa equipe cobre mais de 20 áreas especializadas. Se o seu pet precisar de um especialista, ele já está aqui.`
- **20 chips (cada ícone Phosphor):** Neurologia · Cardiologia · Oncologia · Dermatologia · Oftalmologia · Ortopedia · Endocrinologia · Gastroenterologia · Nefrologia · Hematologia · Odontologia · Pneumologia · Nutrição · Radiologia · Anestesia · Felinos · Silvestres · Ozonioterapia · Reabilitação · Ultrassonografia
- **CTA footer:** `Ver todas as especialidades →` → `/especialidades`

### Layout
- Padding-block `--sp-section`
- Stage container: position relative, overflow hidden
- Fade-edges: pseudo-elements `::before` e `::after` 80px, gradient bg
- Track: flex gap 12px, animation `infiniteScroll 40s linear infinite`
- Chip: min-width clamp(140px, 14vw, 180px), height 80px, padding 12px 20px, radius 16px, bg surface, border 1px

### Tipografia / Cores
- Chip name: DM Sans 600 · 0.875rem · color text
- Icon Phosphor: 24px primary

### Animações
- `@keyframes infiniteScroll`: 0% translateX(0) → 100% translateX(-50%) (chips duplicados pra continuidade)
- Hover pausa animation (animation-play-state paused)
- Drag-to-scroll JS (pageX track scrollLeft)

### Responsividade
- **≤480px:** chip min-width 110px, height 72px

---

## Seção 8: TESTIMONIALS

### Arquétipo / Constraints / Conteúdo
- Idêntico à home seção 8.
- Mesmo CSS carousel dark mode + auto-rotate 6s.
- Mesmos 3 slides + estrelas pop stagger.

---

## Seção 9: INSTAGRAM

### Arquétipo / Constraints / Conteúdo
- Idêntico à home seção 9.
- Grid 6 tiles + hover overlay verde + CTA pill.
- Mesmas 6 fotos + comentário HTML para widget LightWidget/Elfsight.
- Link `https://instagram.com/vetpiera`

---

## Seção 10: CONTATO + MAPA (Agendamento)

### Arquétipo e Constraints
- **Arquétipo:** Split Assimétrico 45/55 (info / mapa)
- **Constraints:** Dark Background (Cor) · Glass Card Floating com Live Indicator (Layout + Movimento) · Map embed (Mídia)
- **Justificativa:** Encerra hospital com prova de "aberto agora" + mapa real. Diferente do Book CTA da home (que tem foto), aqui o mapa é o elemento visual.

### Conteúdo
- **Eyebrow:** `Plantão 24 horas`
- **Título:** `Estamos abertos agora.`
- **Sub:** `Nosso hospital nunca fecha. Entre em contato pelo WhatsApp ou telefone — nossa equipe responde imediatamente.`
- **Info list (4 itens com ícone):**
  - `ph-map-pin` Endereço · "Av. Maria Luiza Americano, 803 — São Paulo, SP"
  - `ph-clock` Horário · "24 horas · 7 dias por semana"
  - `ph-phone` Telefone · `(11) 2746-7292`
  - `ph-envelope` E-mail · `hospital@vetpiera.com.br`
- **CTA primário:** `Chamar no WhatsApp` + ícone
- **Mapa:** iframe Google Maps embed
- **Glass card flutuante (canto inferior-esq do mapa):** dot verde pulsando + "Aberto agora · 24h · 7 dias"

### Layout
- Padding-block `--sp-section`
- Background: `linear-gradient(135deg, #0F2D24, #1B4D3E)` (mesmo do Book CTA da home pra consistência)
- Grid 45fr / 55fr, gap clamp(40px, 6vw, 80px)
- Mapa: aspect 16/11, radius 20px, overflow hidden
- Glass card: position absolute `bottom: 24px; left: 24px`, padding 12px 18px, radius 12px, backdrop-filter blur(16px), bg rgba(255,255,255,.18), text white, dot verde 10px pulse

### Tipografia / Cores
- Eyebrow: DM Sans 600 · 0.8125rem · uppercase · 0.18em · dourado
- Title: DM Serif Display · clamp(2rem, 4vw, 3rem) · white
- Sub: DM Sans 400 · 1.05rem · rgba(255,255,255,.85)
- Info label: DM Sans 500 · 0.75rem · uppercase · 0.08em · rgba(255,255,255,.6)
- Info value: DM Sans 400 · 1rem · white
- Tel link: dourado underline

### Animações
- Glass dot pulse: 1.6s box-shadow ring

### Responsividade
- **≤860px:** grid 1 coluna, mapa em cima

---

## Footer (compartilhado com home)

Mesma estrutura 3 colunas. Ver `home/layout.md`.

---

## Variedade entre seções consecutivas

| # | Arquétipo | Constraint principal |
|---|-----------|----------------------|
| 1 | Split com Overlap | Gradient Mesh + Live Pulse |
| 2 | Type Hero Editorial | Color Blocking |
| 3 | Split Alternado | Badge Overlapping |
| 4 | Bento Assimétrico | 3D Flip + Live Tag |
| 5 | Grid 3×3 Simétrico | Clip Reveal stagger |
| 6 | Featured Carousel (buttons) | Drag-to-Scroll |
| 7 | Kinetic Type Strip | Infinite Loop |
| 8 | CSS Carousel | Dark Mode |
| 9 | Gallery Wall | Hover Overlay |
| 10 | Split Assimétrico 45/55 | Dark Bg + Glass Live |

✓ Nenhum arquétipo repetido consecutivo.
✓ Hero (Split 60/40) ≠ Sobre (Split 50/50) ≠ Contato (Split 45/55) — todos splits MAS proporções e densidades diferentes.
