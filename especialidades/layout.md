# Layout — Especialidades (VetPiera)

> Especificação exaustiva das 10 seções da página Especialidades, na ordem Petderma. Hero + Stats já implementados como demo aprovada. Compartilha tokens da home — ver `home/layout.md` para tabela completa.

---

## Design Tokens

Mesmos da home — DM Serif Display + DM Sans, paleta verde escuro #1B4D3E + dourado #C9A84C, mesh gradient backgrounds.

**Proposta diferencial de Especialidades:** sofisticação + cuidado eletivo. Em vez do plantão urgente do hospital:
- Dot **dourado** pulsante (calmo, sofisticado)
- Card "25 especialidades" como elemento de destaque
- Tag "Agendamento rápido" (vs "Aberto agora" do hospital)

---

## Seção 1: HERO

### Arquétipo e Constraints
- **Arquétipo:** Split com Overlap (60/40)
- **Constraints:** Gradient Mesh (Cor) · Image Gradient (Mídia) · Headline com Gradiente (Tipo) · Card Stamp "25" floating (Layout)
- **Justificativa:** Mantém consistência com home/hospital. Card stamp grande "25" substitui o stamp pequeno do hospital — é o número mais marcante da unidade.

### Conteúdo
- **Eyebrow pill (dot dourado pulse 2.4s):** `Clínica de Especialidades · Tatuapé, SP`
- **Headline:** `[25 especialidades] veterinárias para um cuidado feito sob medida.` — "25 especialidades" em gradient italic
- **Sub:** `Da neurologia à reabilitação — equipe de especialistas para diagnosticar, tratar e cuidar com excelência em cada área da medicina veterinária.`
- **CTA primário:** `Agendar uma consulta` + `ph-arrow-right` → `#contato`
- **CTA secundário:** `Ver todas as especialidades` + `ph-arrow-down` (cue scroll) → `#especialidades-lista`
- **Trust strip:** Diagnóstico preciso · Tratamento personalizado · Acompanhamento contínuo
- **Card stamp "25" (bottom-left foto, rotacionado -2deg):**
  - Num gigante: `25` em gradient verde→dourado
  - Label: `especialidades veterinárias`
- **Tag dourada (top-right foto, +2deg):** `ph-fill ph-calendar-check` + "Agendamento rápido"

### Layout
- Container 1320px, padding `clamp(120px, 14vw, 160px) var(--pad-x) clamp(80px, 10vw, 120px)`
- Grid `60fr 40fr`, gap `clamp(40px, 6vw, 80px)`
- Card stamp position absolute `bottom: -32px; left: -32px`, padding 20px 28px, radius 20px, glass branco 96%

### Tipografia
- Headline: DM Serif Display 400 · `clamp(2.5rem, 5.5vw, 4.5rem)` · line-height 1.04 · letter-spacing -0.025em
- Em: gradient idêntico ao home
- Card num: DM Serif Display · `clamp(3rem, 5vw, 4rem)` · line-height 0.9 · letter-spacing -0.04em em gradient
- Card label: DM Sans 600 · 0.75rem · uppercase · 0.08em · muted

### Cores
- Mesh gradient idêntico à home (orb 1 verde primary 22%)
- Card stamp: bg `rgba(255,255,255,.96)`, backdrop-filter blur(20px), box-shadow `0 24px 56px -12px rgba(15,45,36,.30) + inset ring branco`

### Animações
- Orbs drift idêntico
- Pulse dourado eyebrow (2.4s)
- Photo rotate -1.5deg → 0 hover
- Photo parallax desktop only

### Imagem
- `/images/especialidades-hero-final.png` (atendimento na clínica)
- Position 50% 30% (foco no centro-superior)

### Responsividade
- **≤980px:** grid 1 coluna
- **≤640px:** card stamp `left: 12px bottom: -16px`, tag `right: 12px top: 12px`

---

## Seção 2: STATS BAR

### Arquétipo / Constraints
- Type Hero Editorial idêntico à home (sufixado `.esp-stats`)

### Conteúdo
- **Eyebrow:** `Especialidades em números`
- **Título:** `Equipe completa para cada tipo de cuidado.`
- **Stats:**
  1. **25** · ATUAÇÃO · "Áreas especializadas"
  2. **13+** · EQUIPE · "Veterinários especialistas"
  3. **22+** · TEMPO · "Anos de experiência"
  4. **100%** (italic) · CUIDADO · "Atendimento personalizado"

### Layout / Animações
Idênticos à home seção 2.

---

## Seção 3: SOBRE AS ESPECIALIDADES

### Arquétipo e Constraints
- **Arquétipo:** Split Alternado 50/50 com Imagem à esquerda (inverte ordem em relação à home/hospital)
- **Constraints:** Imagem com Overlay (Mídia) · Quote/Manifesto Style (Tipografia) · Reveal Stagger (Movimento)
- **Justificativa:** Inverter ordem (foto-esquerda / texto-direita) cria variedade em relação ao hospital. Tom mais "manifesto" — paixão pela especialização.

### Conteúdo
- **Pre-título:** `Cuidado especializado`
- **Título:** `Cada animal tem uma história. Cada caso, um especialista.`
- **Texto 1:** `Da neurologia à fisioterapia, da oncologia à dermatologia — reunimos médicos veterinários com formação profunda em cada área da medicina animal. Aqui, seu pet é atendido por quem entende exatamente do que ele precisa.`
- **Texto 2:** `Mais de 25 especialidades sob o mesmo teto. Diagnóstico preciso, tratamento personalizado, acompanhamento contínuo. Cuidado completo, do primeiro exame ao último acompanhamento.`
- **CTA:** `Ver lista completa de especialidades →` → `#especialidades-lista`
- **Imagem:** `/images/diretor-ryan.jpg` ou `dra-diana.jpg` (foto da equipe diretora)
- **Badge sobreposto:** `13+ Especialistas`

### Layout
- Container 1200px, grid 2 colunas gap clamp(48px, 6vw, 80px), align center
- Imagem na esquerda (inverte ordem visual do hospital)
- Badge top-right da imagem (sangrando)

### Tipografia / Cores
- Pre-título: DM Sans 600 · 0.8125rem · uppercase · 0.18em · dourado
- Título: DM Serif Display · `clamp(2rem, 4vw, 3rem)` · line-height 1.1
- Texto: DM Sans 400 · 1rem · line-height 1.65 · muted

### Responsividade
- **≤900px:** 1 coluna, imagem em cima

---

## Seção 4: GRID DE ESPECIALIDADES (25 áreas)

### Arquétipo e Constraints
- **Arquétipo:** Modular Grid Denso (5 colunas × 5 linhas)
- **Constraints:** Hover Lift + Icon Glow (Interação) · Color Blocking sutil por categoria (Cor) · Stagger Wave on Scroll (Movimento)
- **Justificativa:** 25 especialidades exigem grid denso. Diferente do hospital (que tem strip kinetic 20 chips) — aqui cada uma é card clicável.

### Conteúdo
- **Pre-título:** `Nossas áreas`
- **Título:** `25 especialidades em um só lugar.`
- **Sub:** `Cada área conduzida por especialistas com formação focada e experiência prática.`
- **25 cards (categoria + ícone + nome + 1 frase):**
  1. `ph-brain` **Neurologia** · "Doenças do sistema nervoso central e periférico."
  2. `ph-heartbeat` **Cardiologia** · "Diagnóstico e tratamento de cardiopatias."
  3. `ph-drop` **Oncologia** · "Tratamento de neoplasias com quimioterapia e cirurgia."
  4. `ph-scissors` **Dermatologia** · "Doenças de pele, alergias e dermatopatias."
  5. `ph-eye` **Oftalmologia** · "Cuidado completo da visão animal."
  6. `ph-bone` **Ortopedia** · "Cirurgia óssea e tratamento de traumas."
  7. `ph-flask` **Endocrinologia** · "Distúrbios hormonais e metabólicos."
  8. `ph-thermometer` **Gastroenterologia** · "Doenças do trato digestivo."
  9. `ph-drop-half` **Nefrologia** · "Doenças renais e tratamento dialítico."
  10. `ph-shield-check` **Hematologia** · "Anemias, distúrbios sanguíneos e transfusão."
  11. `ph-tooth` **Odontologia** · "Limpeza, extração e cirurgias dentárias."
  12. `ph-wind` **Pneumologia** · "Doenças respiratórias e do trato pulmonar."
  13. `ph-chart-line-up` **Nutrição** · "Dietas terapêuticas personalizadas."
  14. `ph-x-ray` **Radiologia** · "Radiografia digital e laudo especializado."
  15. `ph-syringe` **Anestesia** · "Anestesia segura para todas as cirurgias."
  16. `ph-cat` **Felinos** · "Atendimento exclusivo para gatos."
  17. `ph-bird` **Silvestres e Exóticos** · "Aves, répteis e mamíferos não convencionais."
  18. `ph-sparkle` **Ozonioterapia** · "Tratamento integrativo com ozônio medicinal."
  19. `ph-person-arms-spread` **Reabilitação** · "Fisioterapia, acupuntura e laser."
  20. `ph-waves` **Ultrassonografia** · "Diagnóstico por imagem em tempo real."
  21. `ph-pulse` **Cirurgia Geral** · "Procedimentos cirúrgicos de rotina e complexidade."
  22. `ph-baby` **Reprodução** · "Reprodução assistida, monitoramento gestacional."
  23. `ph-virus` **Doenças Infecciosas** · "Diagnóstico e tratamento de infecciosas."
  24. `ph-paw-print` **Comportamento** · "Etologia clínica e modificação comportamental."
  25. `ph-hand-heart` **Geriatria** · "Cuidado especializado para pets idosos."

### Layout
- Container 1280px
- Grid `repeat(5, 1fr)`, gap 16px
- Card: padding 24px, radius 14px, bg surface, border 1px solid border, min-height 180px
- Icon: 44×44px container radius 12px, bg verde-pale, color primary, ícone 22px

### Tipografia / Cores
- Name: DM Serif Display · 1.15rem · line-height 1.2
- Desc: DM Sans 400 · 0.875rem · line-height 1.5 · muted (max 2 linhas via line-clamp opcional)

### Animações
- Hover: translateY(-4px) + box-shadow + icon container bg→primary (cor inverte)
- Stagger wave: cada card opacity 0→1 + scale 0.95→1, delay `--card-i * 40ms` ao entrar viewport, 500ms ease-out

### Responsividade
- **≤1100px:** grid 4 colunas
- **≤860px:** grid 3 colunas
- **≤600px:** grid 2 colunas
- **≤420px:** grid 1 coluna

---

## Seção 5: POR QUE ESCOLHER (Pillars)

### Arquétipo e Constraints
- **Arquétipo:** Editorial Rows numeradas (similar à home, conteúdo específico)
- **Constraints:** Type Hero numérico em outline (Tipografia) · Scroll-driven entrance (Movimento)
- **Justificativa:** Mantém ritmo da home (que tem editorial rows), mas com 4 pilares específicos da clínica de especialidades.

### Conteúdo
- **Título:** `Por que escolher a Clínica de Especialidades Piera.`
- **Pilares (4):**
  1. `01` · `ph-target` Diagnóstico · **Diagnóstico preciso** · "Equipamentos de imagem de última geração + análises laboratoriais + segundas opiniões entre especialistas. Diagnóstico sem chute."
  2. `02` · `ph-puzzle-piece` Tratamento · **Tratamento personalizado** · "Cada animal recebe protocolo individualizado. Histórico, raça, idade e perfil considerados em cada decisão."
  3. `03` · `ph-graduation-cap` Equipe · **Especialistas reais** · "13+ veterinários com residência, mestrado ou doutorado em suas áreas. Aprendizado contínuo é exigência da casa."
  4. `04` · `ph-handshake` Cuidado · **Acompanhamento contínuo** · "Atendimento que não termina no consultório. Mantemos contato com tutores entre consultas e ajustamos o tratamento conforme evolução."

### Layout / Tipografia
Idêntico à home seção 5 (Editorial Rows, número outline, animação scroll-driven).

---

## Seção 6: GALERIA — Nossa Estrutura

### Arquétipo e Constraints
- **Arquétipo:** Scroll Horizontal com Snap (mesmo padrão home)
- **Constraints:** Scroll Snap (Interação) · Hover Scale (Interação) · Custom Scrollbar dourada

### Conteúdo
- **Pre-título:** `Nosso espaço`
- **Título:** `Ambientes pensados para o cuidado especializado.`
- **Intro:** `Consultórios modernos, sala de fisioterapia equipada, recepção acolhedora — estrutura inteira pensada para o bem-estar do animal e do tutor.`
- **6-8 imagens:**
  1. Recepção · `estrutura-recepcao.jpg`
  2. Consultório 1 · `estrutura-consultorio-01.jpg`
  3. Consultório 2 · `estrutura-consultorio-02.jpg`
  4. Sala de Fisioterapia · `estrutura-fisio-01.jpg`
  5. Sala de Fisioterapia 2 · `estrutura-fisio-02.jpg`
  6. Sala Cirúrgica · `estrutura-cirurgico.jpg`
  7. Recuperação · `estrutura-recuperacao.jpg`

### Layout / Animações
Idêntico à home seção 6.

---

## Seção 7: ESPECIALISTAS EM DESTAQUE

### Arquétipo e Constraints
- **Arquétipo:** Photo Cards com Hover Reveal (Bio overlay glass)
- **Constraints:** Glassmorphism Bio Overlay (Efeitos) · Hover Reveal (Interação) · Mixed Photo/Type (Mídia)
- **Justificativa:** Equipe ganha protagonismo em uma seção dedicada — quem cuida importa tanto quanto onde se cuida. Bio escondida só revela ao interesse genuíno (hover).

### Conteúdo
- **Pre-título:** `Quem cuida`
- **Título:** `Quem vai cuidar do seu animal.`
- **Sub:** `Nossa clínica é dirigida por especialistas com décadas de experiência nas áreas mais complexas da medicina veterinária.`

- **Card 1 — Dr. Ryan:**
  - Foto: `dr-ryan.jpg`
  - Footer (sempre visível): "Diretor Clínico · Neurologia & Neurocirurgia" + "Dr. Ryan Elias Piera"
  - Overlay bio (hover): role "Neurologia & Neurocirurgia" · name · "Diretor Clínico · CRMV-SP"
  - Bio: "Formação: Graduação USP (2000), Mestrado USP (2005), Especialista Neurologia Anhembi (2009) e Argentina (2012). Neurocirurgião UNESP (2019)."
  - Experiência: "Diretor do Grupo Piera desde 2002. Especialista em doenças neuromusculares e emergências neurológicas."

- **Card 2 — Dra. Diana:**
  - Foto: `dra-diana.jpg`
  - Footer: "Diretora Clínica · Fisioterapia & Reabilitação" + "Dra. Diana Sogaiar Elias Piera"
  - Overlay bio: role "Fisioterapia & Reabilitação" · name · "Diretora Clínica · CRMV-SP"
  - Bio: "Graduação USP (2005), Residência USP, Esp. Fisioterapia e Acupuntura IBRA (2019), Ozonioterapia (2022)."
  - Experiência: "Diretora desde 2002. Especialista em reabilitação integrativa e ozonioterapia."

- **Card 3 (opcional) — Outro especialista da equipe**

### Layout
- Container 1200px
- Grid 2 colunas (ou 3 se 3 cards), gap 24px
- Card aspect 3/4 (vertical), radius 20px, overflow hidden, position relative
- Photo background-size cover
- Overlay: position absolute inset 0, bg `rgba(15,45,36,.92)` + backdrop-filter blur(8px), opacity 0 → 1 on hover, padding 32px
- Footer: position absolute bottom 0, padding 20px 24px, bg `linear-gradient(to top, rgba(0,0,0,.7), transparent)`

### Tipografia / Cores
- Role overlay: DM Sans 600 · 0.75rem · uppercase · 0.16em · dourado
- Name overlay: DM Serif Display · 1.5rem · white
- Specialty: DM Sans 500 · 0.875rem · rgba(255,255,255,.7)
- Bio: DM Sans 400 · 0.9375rem · line-height 1.55 · rgba(255,255,255,.85)
- Footer role: DM Sans 500 · 0.8125rem · dourado
- Footer name: DM Serif Display · 1.25rem · white

### Animações
- Hover overlay: opacity 0→1, 400ms ease-out
- Mobile: overlay sempre visível (no hover state)
- "Ver mais" button: toggleBio JS para expandir conteúdo

### Responsividade
- **≤760px:** grid 1 coluna, card aspect 4/5
- **Mobile:** overlay default visible (não requer hover)

---

## Seção 8: COMO FUNCIONA (Processo)

### Arquétipo e Constraints
- **Arquétipo:** Timeline Horizontal numerada (4 passos)
- **Constraints:** Stepped Numbers (Tipografia) · Connecting Line gradient (Layout) · Stagger Reveal (Movimento)
- **Justificativa:** Diferente de tudo até aqui — uma jornada visual de 4 etapas. Cria expectativa de como será a experiência.

### Conteúdo
- **Pre-título:** `Como funciona`
- **Título:** `Da consulta ao acompanhamento, sem complicações.`
- **4 passos (timeline horizontal):**
  1. `01` · `ph-chat-circle-text` **Agendamento** · "Fale com nossa equipe pelo WhatsApp ou telefone. Marcamos no melhor horário pra você."
  2. `02` · `ph-clipboard-text` **Consulta especializada** · "Veterinário especialista da área avalia o caso, faz exame clínico e solicita exames se necessário."
  3. `03` · `ph-stethoscope` **Tratamento personalizado** · "Protocolo individualizado considerando histórico, raça, idade e particularidades do animal."
  4. `04` · `ph-arrows-clockwise` **Acompanhamento contínuo** · "Retornos, ajustes de tratamento e comunicação direta entre consultas."

### Layout
- Container max-width 1200px
- Padding-block `--sp-section`
- Grid `repeat(4, 1fr)`, gap 32px
- Linha conectora: position absolute top 40px (alinhada com número), height 2px, gradient `linear-gradient(to right, transparent 0%, primary 20%, accent 80%, transparent 100%)`
- Step container: text-align center, position relative

### Tipografia / Cores
- Número: DM Serif Display · 3rem · color transparent · `-webkit-text-stroke 1.5px primary` · letter-spacing -0.04em · marca acima do ícone
- Icon: 48×48px container radius 50% (circle), bg surface, border 2px solid primary, ícone 24px primary, position relative (sobreposto à linha)
- Title: DM Serif Display · 1.25rem · line-height 1.2
- Desc: DM Sans 400 · 0.9375rem · line-height 1.55 · muted

### Animações
- Stagger reveal: cada step opacity 0+scale(0.9) → 1+1, delay `--step-i * 150ms`, 600ms ease-out, IO threshold 0.3
- Linha conectora: clip-path inset(0 100% 0 0) → inset(0 0 0 0), 1200ms ease-out, trigger junto com primeiro step

### Responsividade
- **≤860px:** grid 2 colunas, linha conectora some
- **≤520px:** grid 1 coluna, layout vertical (linha conectora vertical à esquerda)

---

## Seção 9: INSTAGRAM

### Arquétipo / Constraints / Conteúdo
- Idêntico à home/hospital seção 9.
- Grid 6 tiles, hover overlay verde, CTA pill, link `https://instagram.com/vetpiera`.
- Mesmas 6 fotos (placeholder até integração do widget).

---

## Seção 10: CONTATO (Agendamento)

### Arquétipo e Constraints
- **Arquétipo:** Split Assimétrico (45/55) com Form + Info
- **Constraints:** Form Native HTML5 (Estrutura) · Dark Background (Cor) · Map Embed (Mídia)
- **Justificativa:** Diferente do hospital (que tem mapa grande + glass live). Aqui tem FORMULÁRIO de agendamento — proposta de Especialidades é consulta eletiva agendada.

### Conteúdo
- **Eyebrow:** `Agende sua consulta`
- **Título:** `Vamos cuidar do seu pet juntos.`
- **Sub:** `Preencha o formulário e nossa equipe entra em contato em até 1 hora útil. Ou fale direto pelo WhatsApp.`

- **Info list (3 itens):**
  - `ph-map-pin` `Rua Itapeti, 154 — Tatuapé, São Paulo, SP`
  - `ph-clock` `Seg–Sex 9h–18h · Sáb 9h–13h`
  - `ph-phone` `(11) 2373-3144` (link tel)

- **CTA WhatsApp:** botão pill dourado "Falar pelo WhatsApp" → `wa.me/5511963326376`

- **Formulário (Netlify Forms):**
  - Hidden: form-name "contato-especialidades", bot-field honeypot
  - Nome (required, autocomplete name)
  - E-mail (required, autocomplete email)
  - Telefone/WhatsApp (required, autocomplete tel — `intl-tel-input`)
  - Especialidade desejada (select com 25 opções + "Não sei ainda")
  - Mensagem (textarea opcional)
  - Botão submit: "Agendar consulta →" gradient verde

- **Mapa:** iframe Google Maps embed da Rua Itapeti 154

### Layout
- Padding-block `--sp-section`
- Background: `linear-gradient(135deg, #0F2D24 0%, #1B4D3E 100%)` (consistência com home Book CTA + hospital contato)
- Decoração: radial dourado top-right 15%
- Grid 45fr / 55fr, gap clamp(40px, 6vw, 80px)
- Form panel (esquerda): card glass `rgba(255,255,255,.05)` backdrop blur(20px), padding clamp(32px, 4vw, 48px), radius 24px
- Info+Map panel (direita): info acima, mapa abaixo (aspect 4/3, radius 16px)

### Tipografia / Cores
- Eyebrow: DM Sans 600 · 0.8125rem · uppercase · 0.18em · dourado
- Title: DM Serif Display · clamp(2rem, 4vw, 3rem) · white
- Sub: DM Sans 400 · 1.05rem · rgba(255,255,255,.85)
- Form label: DM Sans 500 · 0.875rem · rgba(255,255,255,.8)
- Form input: bg `rgba(255,255,255,.08)`, border 1px solid `rgba(255,255,255,.18)`, padding 14px 16px, radius 10px, color white, font DM Sans 1rem
- Form input focus: border-color dourado, box-shadow `0 0 0 3px rgba(201,168,76,.18)`
- Submit btn: bg `linear-gradient(135deg, #1B4D3E, #2A6B56)`, hover gradient invertido

### Animações
- Form entrance: stagger fadeUp por field, 80ms entre cada, IO threshold 0.2
- Submit: hover translateY(-2px) + shadow + ícone translate-right

### Responsividade
- **≤860px:** grid 1 coluna (form em cima, info+mapa embaixo)

---

## Footer (compartilhado)

Mesma estrutura 3 colunas das outras páginas.

---

## Variedade entre seções consecutivas

| # | Arquétipo | Constraint principal |
|---|-----------|----------------------|
| 1 | Split com Overlap 60/40 | Gradient Mesh + Card Stamp |
| 2 | Type Hero Editorial | Color Blocking |
| 3 | Split Alternado (foto-esq) | Imagem Overlay + Badge |
| 4 | Modular Grid Denso 5×5 | Hover Lift + Stagger Wave |
| 5 | Editorial Rows | Type numérico outline |
| 6 | Scroll Horizontal | Scroll Snap |
| 7 | Photo Cards Hover Reveal | Glassmorphism overlay |
| 8 | Timeline Horizontal | Stepped Numbers + Line |
| 9 | Gallery Wall | Hover Overlay |
| 10 | Split Form/Info 45/55 | Dark Bg + Form Native |

✓ Nenhum arquétipo repetido consecutivo.
✓ Hero (Split 60/40) ≠ Sobre (Split 50/50 inverted) ≠ Contato (Split 45/55 form) — splits com proporções, densidades e propósitos diferentes.
✓ Página tem mais seções "dense" que home (Grid denso 5×5 + Timeline) por ser uma página de catálogo.
