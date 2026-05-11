# Layout — Home (Grupo Piera)

> Especificação exaustiva das 10 seções da home, na ordem do Petderma, adaptada à proposta Piera (2 unidades). Hero + Stats já implementados como demo de design aprovada.

---

## Design Tokens (Bíblia)

### Cores
```
--clr-primary:       #1B4D3E   /* verde escuro principal */
--clr-primary-mid:   #2A6B56   /* verde médio (gradients) */
--clr-primary-pale:  #E8F2ED   /* verde claríssimo (badges) */
--clr-accent:        #C9A84C   /* dourado */
--clr-accent-deep:   #b8922e   /* dourado escuro (gradients) */
--clr-accent-light:  #E6BC52   /* dourado claro (gradients) */
--clr-dark:          #0F2D24   /* verde quase preto (CTAs dark) */
--clr-bg:            #FAFAF8   /* fundo claro principal */
--clr-bg-mesh-1:     #FCFCF9   /* topo do mesh gradient */
--clr-bg-mesh-2:     #F4F7F4   /* fim do mesh gradient */
--clr-surface:       #FFFFFF   /* cards */
--clr-border:        #E2E8E5
--clr-text:          #1A1A1A
--clr-muted:         #5C6B74
```

### Fontes
- **Heading:** DM Serif Display (400 + italic) — Google Fonts
- **Body:** DM Sans (400, 500, 600, 700) — Google Fonts

### Espaçamentos
- `--sp-section: clamp(80px, 10vw, 128px)`
- Container default: 1200px max-width
- Container Hero: 1320px max-width
- `--pad-x: clamp(24px, 5vw, 64px)`
- Radius: 12px default · 18–28px cards grandes · 999px pills

### Easing global
- `cubic-bezier(0.16, 1, 0.3, 1)` (out-expo, premium)
- Durations: 280ms small interactions · 600–800ms entrance · 1400ms counter

---

## Seção 1: HERO

### Arquétipo e Constraints
- **Arquétipo:** Split com Overlap (60/40)
- **Constraints:** Gradiente Mesh (Cor) · Imagem com Gradiente (Mídia) · Mouse Parallax (Interação) · Headline com Gradiente (Tipografia)
- **Justificativa:** Mantém leveza editorial Petderma com foto generosa, evitando "split frio 50/50". Palavra-chave em gradient cria foco sem bullet visual.

### Conteúdo (literal)
- **Eyebrow pill (dot dourado pulsando):** `Grupo Piera · Desde 2002`
- **Headline:** `O cuidado [veterinário] completo que o seu pet merece.` — "veterinário" em gradient italic
- **Sub:** `Somos o Grupo Piera — 22 anos cuidando de animais com tecnologia, especialização e humanidade.`
- **CTA primário:** `Hospital 24h` + `ph-arrow-right` → `/hospital`
- **CTA secundário:** `Conhecer Especialidades` + `ph-arrow-up-right` → `/especialidades`
- **Trust strip (3 itens com `ph-fill ph-check-circle`):** Hospital 24h · 25 especialidades · 13+ veterinários
- **Badge bottom-left foto:** `22+ anos de excelência`
- **Tag dourada top-right foto (`ph-fill ph-star`):** `5.0 · Google Reviews`

### Layout
- Container max-width 1320px, padding `clamp(120px, 14vw, 160px) var(--pad-x) clamp(80px, 10vw, 120px)`
- Grid `60fr 40fr`, gap `clamp(40px, 6vw, 80px)`, align-items center
- min-height 100svh desktop
- Photo-wrap rotacionado `-1.5deg` → `0deg` em hero hover (600ms)
- Badge: position absolute, `bottom: 24px; left: -36px` (sangrando)
- Tag dourada: `top: 24px; right: -16px`, rotacionada `+2deg`

### Tipografia
- Headline: DM Serif Display 400 · `clamp(2.75rem, 6vw, 5rem)` · line-height 1.02 · letter-spacing -0.025em
- Headline-grad: `linear-gradient(105deg, #1B4D3E 0%, #2A6B56 45%, #C9A84C 100%)` + `background-clip: text` + `font-style: italic`
- Sub: DM Sans 400 · `clamp(1.05rem, 1.5vw, 1.18rem)` · line-height 1.6 · color muted · max-width 520px
- Eyebrow: DM Sans 600 · 0.8125rem · uppercase · 0.08em letter-spacing · primary
- Badge num: DM Serif Display `clamp(3rem, 5vw, 4rem)` em gradient verde→dourado
- Badge label: DM Sans 500 · 0.75rem · uppercase · 0.06em · muted

### Cores / Background
- Fundo: linear `#FCFCF9 0% → #F4F7F4 100%` + radial gradients verde-pale top-left e dourado 10% top-right
- 3 orbs blur 80px:
  - Orb 1: 480px verde primary 22%, top-left (-120px, -120px)
  - Orb 2: 380px dourado 18%, bottom-22% right
  - Orb 3: 320px verde-mid 18%, top-30% right-8%

### Elementos Visuais
- Photo-wrap: radius 28px · overflow hidden · box-shadow `0 40px 80px -20px rgba(15,45,36,.35) + inset 0 0 0 1px rgba(255,255,255,.4)`
- Photo-overlay: `linear-gradient(180deg, transparent 40%, rgba(15,45,36,.45) 100%) + radial top-right dourado 12%` · mix-blend-mode multiply
- Badge: glass card branco 94% · backdrop-filter blur(20px) · radius 20px · padding 20px 28px

### Animações
- **Orbs drift:** `heroOrbDrift 18s ease-in-out infinite alternate` — translate(0,0)→(40px,-30px), scale 1→1.08. Delays/durations diferentes (-3s -6s; 16s 18s 22s)
- **Eyebrow dot pulse:** `heroPulse 2.4s ease-in-out infinite` — box-shadow ring 0→8px
- **Counter badge:** 0→22 em 1400ms, easing `1 - (1-p)^2`, IO threshold 0.5
- **Photo parallax (desktop only):** mousemove ajusta `background-position` da `.hero__photo` com STRENGTH 0.015. Mouseleave volta a 50%/50% (transition 800ms).

### Interatividade
- Hero hover: photo-wrap → rotate(0deg)
- CTA primary hover: gradient invertido + translateY(-3px) + shadow intensifica + ícone translateX(+4px)
- CTA secondary hover: color→primary, gap 8→12px, border-bottom→primary
- Focus visible: outline 2px solid dourado offset 4px

### Responsividade
- **≤980px:** grid 1 coluna, ordem copy→media. Photo-wrap rotate 0deg. Min-height auto.
- **≤640px:** headline `clamp(2.25rem, 9vw, 3rem)` · media min-height 360px · badge `left: 12px bottom: 12px` · tag `right: 12px top: 12px` · trust strip gap 16px
- **≤380px:** headline 2.125rem

---

## Seção 2: STATS BAR

### Arquétipo e Constraints
- **Arquétipo:** Type Hero Editorial — números gigantes serif como protagonistas
- **Constraints:** Color Blocking sutil (Cor) · Counter Animation (Movimento) · Stagger Sequencial (Movimento)
- **Justificativa:** Quebra do hero ao introduzir seção quase 100% tipográfica. Pausa antes do bloco textual de Quem Somos.

### Conteúdo
- **Eyebrow:** `Números que pesam`
- **Título:** `Mais de duas décadas cuidando de quem você ama.`
- **Stats (4):**
  1. **22+** · TEMPO · "Anos de experiência"
  2. **25** · ATUAÇÃO · "Especialidades veterinárias"
  3. **13+** · EQUIPE · "Veterinários especialistas"
  4. **24h** (italic) · PLANTÃO · "Hospital aberto todos os dias"

### Layout
- Padding section: `clamp(80px, 10vw, 128px) 0`
- Intro centralizada, margin-bottom `clamp(56px, 7vw, 88px)`, título max-width 720px
- Grid 4 colunas, gap 0
- Cada item: flex column align-items flex-start, padding `clamp(20px, 2.5vw, 32px)`

### Tipografia
- Número: DM Serif Display · `clamp(4rem, 8.5vw, 7.5rem)` · line-height 0.85 · letter-spacing -0.05em
- Número grad: `linear-gradient(135deg, #1B4D3E 0%, #2A6B56 50%, #C9A84C 130%)` + clip
- "24h" italic
- Plus: DM Serif Display · `clamp(2rem, 4vw, 3.25rem)` · color dourado
- Label eyebrow: DM Sans 600 · 0.6875rem · uppercase · 0.2em · dourado
- Label: DM Sans 500 · `clamp(0.95rem, 1.2vw, 1.05rem)` · line-height 1.35

### Cores
- Fundo: `--clr-bg` (#FAFAF8) com radial verde 6% top + dourado 8% bottom-right

### Elementos Visuais
- Separadores verticais entre itens: `linear-gradient(180deg, transparent, rgba(27,77,62,.25), transparent)`, top 18% bottom 18%, width 1px

### Animações
- `statsReveal 700ms cubic-bezier(0.16, 1, 0.3, 1) forwards`: opacity 0+translateY(24px) → 1+0
- delay `calc(var(--stat-i) * 120ms + 100ms)`
- Counter: easing quadOut, 1400ms, IO threshold 0.5

### Responsividade
- **≤900px:** grid 2 colunas; itens 3-4 com border-top
- **≤520px:** grid 1 coluna, separadores horizontais

---

## Seção 3: QUEM SOMOS

### Arquétipo e Constraints
- **Arquétipo:** Split Alternado 50/50 (Texto + Badge / Imagem)
- **Constraints:** Imagem com Overlay (Mídia) · Badge Overlapping (Layout) · Reveal Stagger on Scroll (Movimento)
- **Justificativa:** Quebra do tipográfico-puro das stats com retorno a split. Diferente do hero (overlap) — aqui é alternado simétrico.

### Conteúdo
- **Pre-título:** `Nossa história`
- **Título:** `Cuidamos como se fosse parte da nossa família.`
- **Texto 1:** `O Grupo Piera é composto pelo Piera Hospital Veterinário, que realiza atendimento clínico e hospitalar 24 horas; Piera Especialidades Veterinárias, focado no atendimento de especialidades e Piera Cursos veterinários, focado no aprimoramento de médicos veterinários.`
- **Texto 2:** `Nascemos com a missão de oferecer medicina de alta complexidade com o acolhimento que seu pet merece. Hoje somos referência em neurologia, cirurgias complexas e reabilitação em toda a grande São Paulo.`
- **CTA:** `Saiba mais sobre o Grupo Piera →` (link underline dourado)
- **Badge sobreposto:** `22+ Anos de Experiência`
- **Imagem:** `/images/hosp-exterior.jpg`

### Layout
- Container max-width 1200px, padding `--sp-section --pad-x`
- Grid 2 colunas (1fr 1fr), gap `clamp(48px, 6vw, 80px)`, align-items center
- Imagem: radius 24px · aspect 4/3 · overflow hidden
- Badge sticky: position absolute, `top: -32px; left: -32px`, padding 20px 28px, bg branco, shadow elevada

### Tipografia
- Pre-título: DM Sans 600 · 0.8125rem · uppercase · 0.18em · dourado
- Título: DM Serif Display · `clamp(2rem, 4vw, 3rem)` · line-height 1.1 · color dark
- Texto: DM Sans 400 · 1rem · line-height 1.65 · muted

### Animações
- Badge: scale(0.92)→1 + opacity 0→1, delay 200ms ao entrar viewport
- Texto stagger: pre→título→t1→t2→CTA com delays 0/100/200/300/400ms

### Responsividade
- **≤900px:** 1 coluna, imagem primeiro. Badge `top: -24px; left: 12px`

---

## Seção 4: SERVICES (Grid de Procedimentos)

### Arquétipo e Constraints
- **Arquétipo:** Grid Modular (4 cards iguais)
- **Constraints:** Hover Lift (Interação) · Icon Container com bg pale (Cor) · Stagger Entry on Scroll (Movimento)
- **Justificativa:** Após dois splits (Hero, Quem Somos) e um tipográfico (Stats), precisa de grid pra variedade. 4 cards e não 3 (que é o padrão genérico).

### Conteúdo
- **Pre-título:** `O que fazemos`
- **Título:** `Atendimento veterinário completo, em um só grupo.`
- **Intro:** `Da emergência à madrugada à consulta especializada agendada — toda a estrutura, equipe e tecnologia para cuidar do seu animal.`
- **Cards (4):**
  1. `ph-first-aid` · **Emergência 24h** · "Atendimento de urgência todos os dias, a qualquer hora." → `/hospital#emergencia`
  2. `ph-scissors` · **Cirurgias** · "Centro cirúrgico equipado para procedimentos de alta complexidade." → `/hospital#cirurgia`
  3. `ph-heartbeat` · **UTI Veterinária** · "Internação intensiva com monitoramento 24h." → `/hospital#uti`
  4. `ph-magnifying-glass` · **Diagnóstico por Imagem** · "Raio-x, ultrassom, ecocardiografia e tomografia." → `/hospital#diagnostico`

### Layout
- Container max-width 1200px, padding `--sp-section`
- Header centralizado max-width 720px, margin-bottom `clamp(48px, 6vw, 72px)`
- Grid `repeat(4, 1fr)`, gap 20px
- Card: padding `clamp(24px, 2.5vw, 32px)`, radius 12px, bg surface, border 1px solid border

### Tipografia
- Title card: DM Serif Display 400 · 1.4rem · line-height 1.15
- Desc: DM Sans 400 · 0.95rem · line-height 1.55 · muted
- Link: DM Sans 600 · 0.9rem · primary · border-bottom 1.5px solid dourado

### Cores / Visuais
- Icon container: 52×52px · radius 12px · bg `--clr-primary-pale` · color primary · ícone 26px
- Hover card: translateY(-4px) · box-shadow `0 16px 40px rgba(15,45,36,.10)` · border-color primary-pale

### Animações
- Stagger reveal scroll-triggered (IO threshold 0.15): opacity 0+y20px → 1+0, 600ms ease-out, delay 100ms per card

### Responsividade
- **≤980px:** grid 2 colunas
- **≤520px:** grid 1 coluna

---

## Seção 5: PILLARS (O que nos diferencia)

### Arquétipo e Constraints
- **Arquétipo:** Editorial Rows numeradas — NÃO grid de cards
- **Constraints:** Type Hero numérico em outline (Tipografia) · Wave Stagger scroll (Movimento) · Mixed Weights serif+sans (Tipografia)
- **Justificativa:** Não pode ser cards (já tem em Services). Editorial faz a página respirar diferente. Cada pilar é uma linha larga.

### Conteúdo
- **Título:** `O que nos diferencia.`
- **Pilares (4):**
  1. `01` · `ph-cpu` Tecnologia · **Tecnologia avançada** · "Equipamentos de última geração para diagnóstico e cirurgia — do raio-x digital ao microscópio cirúrgico. Tomografia, endoscopia, ecocardiografia e cirurgia laparoscópica."
  2. `02` · `ph-stethoscope` Equipe · **Equipe especializada** · "Mais de 13 veterinários com formação específica em cada área. Fisioterapeutas, nutricionistas e anestesiologistas dedicados."
  3. `03` · `ph-heart` Cuidado · **Cuidado humanizado** · "Tratamos cada animal como único. Protocolos individualizados, comunicação clara e acolhimento em cada etapa."
  4. `04` · `ph-calendar-check` Experiência · **22 anos de experiência** · "Desde 2002 cuidando de cães, gatos, silvestres e exóticos na Grande São Paulo."

### Layout
- Container max-width 1100px
- Cada row: grid `auto 1fr`, gap 32px, padding-block `clamp(40px, 5vw, 56px)`
- Border-bottom 1px solid border (exceto último)

### Tipografia / Cores
- Número outline: DM Serif Display · 120-180px · color transparent · `-webkit-text-stroke: 1.5px rgba(27,77,62,.25)`
- Tag: DM Sans 600 · 0.8125rem · uppercase · 0.16em + ícone Phosphor
- Name (h3): DM Serif Display · `clamp(1.5rem, 2.5vw, 2rem)`
- Text: DM Sans 400 · 1.05rem · line-height 1.65 · muted · max-width 600px

### Animações
- Scroll-driven (`animation-timeline: view()`, range `entry 0% cover 30%`): opacity 0+y24 → 1+0
- Fallback IO threshold 0.15, delay `calc(--row-i * 80ms)`

### Responsividade
- **≤700px:** número shrinks 80-100px, grid 1 coluna (número acima do conteúdo)

---

## Seção 6: GALLERY (Nosso Espaço)

### Arquétipo e Constraints
- **Arquétipo:** Scroll Horizontal — free-scroll com snap
- **Constraints:** Scroll Snap (Interação) · Hover Scale + Caption Reveal (Interação) · Custom Scrollbar dourada (Mídia)
- **Justificativa:** Petderma usa scroll horizontal pra galeria. Quebra do scroll vertical e dá protagonismo às fotos.

### Conteúdo
- **Pre-título:** `Nosso espaço`
- **Título:** `Estrutura pensada para o bem-estar do pet.`
- **Intro:** `Ambientes amplos, equipamentos modernos e áreas separadas para cães, gatos e isolamento. Conheça por dentro.`
- **8 imagens com caption:**
  1. Recepção · `hosp-estrutura-recepcao.jpg`
  2. Consultório · `hosp-estrutura-consultorio-1.jpg`
  3. Centro Cirúrgico · `hosp-estrutura-cirurgico-1.jpg`
  4. Internação Felinos · `hosp-estrutura-internacao-felinos.jpg`
  5. Internação Cães · `hosp-estrutura-internacao-caes-1.jpg`
  6. Raio-X · `hosp-estrutura-raiox.jpg`
  7. Ultrassom · `hosp-estrutura-ultrassom.jpg`
  8. Fisioterapia · `estrutura-fisio-01.jpg`

### Layout
- Header centralizado max-width 720px
- Rail: flex gap 16px · overflow-x auto · scroll-snap-type x mandatory · padding-inline `--pad-x`
- Item: flex 0 0 auto · width `clamp(260px, 30vw, 380px)` · aspect 4/3 · radius 12px · overflow hidden

### Tipografia / Cores
- Caption: `linear-gradient(to top, rgba(15,45,36,.85), transparent)` · white · DM Sans 600 0.95rem
- Background section: surface (#FFFFFF) — destaca fotos contra section anterior

### Animações
- Hover img: transform scale(1.06), 600ms ease-out
- Custom scrollbar: track verde border 10%, thumb dourado

### Responsividade
- **≤640px:** item width `calc(100vw - 64px)`

---

## Seção 7: UNITS (Duas Unidades)

### Arquétipo e Constraints
- **Arquétipo:** Bento Box 2 cards com 3D Flip
- **Constraints:** 3D Flip (Interação) · Color Blocking dark/light (Cor) · Layered CTAs (Layout)
- **Justificativa:** Diferente do bento Services (cards iguais). 2 cards com cores opostas + flip 3D = momento dramático.

### Conteúdo
- **Pre-título:** `Onde seu pet precisa ir?`
- **Título:** `Duas unidades. Um só compromisso com o seu animal.`
- **Intro:** `Temos a estrutura certa para cada momento — desde a emergência à madrugada até a consulta especializada marcada com antecedência.`
- **Card 1 (DARK — Hospital):**
  - Tag: `Hospital Veterinário`
  - Name: `Emergência 24 horas.`
  - Desc: "Emergências, cirurgias, internação, diagnóstico e atendimento de rotina. Aberto todos os dias, a qualquer hora."
  - CTA: `Ir para o Hospital →` → `/hospital`
  - Back: Tel `(11) 2746-7292` · Av. Maria Luiza Americano, 803 · 24h/7d · btn "Ligar agora →"
- **Card 2 (LIGHT — Especialidades):**
  - Tag: `Clínica de Especialidades`
  - Name: `25 especialidades veterinárias.`
  - Desc: "25 especialidades veterinárias para consultas eletivas. Equipe de especialistas com foco em diagnóstico preciso e tratamento personalizado."
  - CTA: `Conhecer Especialidades →` → `/especialidades`
  - Back: Tel `(11) 2373-3144` · Rua Itapeti, 154 · Seg-Sex 9h-18h Sáb 9h-13h · btn "Agendar consulta →"

### Layout
- Container max-width 1200px
- Header centralizado, max-width 720px
- Grid `1fr 1fr`, gap 24px, min-height 480px por card
- Card padding `clamp(40px, 5vw, 64px)` · radius 24px · perspective 1200px

### Tipografia / Cores
- Card DARK: bg `linear-gradient(135deg, #0F2D24, #1B4D3E)` · text white. Name DM Serif Display `clamp(2rem, 4vw, 2.75rem)`
- Card LIGHT: bg `--clr-primary-pale` · border 1px solid primary 12% · text dark green
- Tag: DM Sans 600 · 0.75rem · uppercase · 0.12em — dourado no dark, primary no light

### Animações
- Flip: `transform: rotateY(180deg)` no `.unit__inner`, transition 700ms cubic-bezier(0.16,1,0.3,1)
- Touch/mobile: click toggle `.is-flipped`
- Keyboard: Enter/Space

### Responsividade
- **≤780px:** grid 1 coluna, min-height 420px

---

## Seção 8: TESTIMONIALS

### Arquétipo e Constraints
- **Arquétipo:** CSS-only Carousel (radio inputs)
- **Constraints:** Dark Mode (Cor) · Auto-rotate 6s + pause on hover (Movimento) · Stars stagger pop (Movimento)
- **Justificativa:** Fundo escuro destaca quote, padrão clássico em CSS puro (radio + :checked siblings).

### Conteúdo
- **Section-label:** `O que dizem quem já foi atendido.`
- **Slide 1:** ★★★★★ "Minha cadela precisou de cirurgia de emergência às 3h da manhã. A equipe do hospital foi incrível — profissional, humana e super atenciosa durante toda a recuperação." — Ana Paula M. · Tutora da Luna, Golden Retriever
- **Slide 2:** ★★★★★ "A especialidade de neurologia da VetPiera salvou a vida do meu gato. O Dr. Ryan explicou cada etapa do diagnóstico com paciência e cuidado extraordinários." — Carlos Eduardo R. · Tutor do Simba, Persa
- **Slide 3:** ★★★★★ "Faço acompanhamento com a Dra. Diana há dois anos para a fisioterapia da minha cachorra. A evolução é impressionante e o atendimento é sempre excepcional." — Mariana F. · Tutora da Mel, Labrador

### Layout
- Padding-block `--sp-section`
- Quote-mark serif gigante (12-15rem), opacity 0.06, absolute top-left, decorativo
- Track: width 300%, transition `transform 700ms`
- Cada slide width 33.33%, padding `clamp(40px, 6vw, 80px)`

### Tipografia / Cores
- Background: `linear-gradient(135deg, #0F2D24 0%, #1B4D3E 100%)`
- Section-label: DM Sans 600 · 0.8125rem · uppercase · 0.16em · dourado
- Quote: DM Serif Display · `clamp(1.4rem, 2.5vw, 2rem)` · line-height 1.4 · white italic
- Author: DM Sans 600 · 1rem · white
- Pet: DM Sans 400 · 0.875rem · rgba(255,255,255,0.6)
- Stars: dourado, 22px, keyframe pop scale 0→1.15→1

### Animações
- `@keyframes starPop`, delay `calc(--star-i * 80ms)`
- Auto-rotate JS 6000ms interval, pause on mouseenter
- Transition CSS-only `:checked ~ .testimonials__track`

### Responsividade
- **≤640px:** quote-mark static, 4rem, opacity 0.25

---

## Seção 9: INSTAGRAM (Feed)

### Arquétipo e Constraints
- **Arquétipo:** Gallery Wall (grid 6 tiles)
- **Constraints:** Hover Overlay verde + ícone instagram (Interação) · Aspect Square 1:1 (Layout) · Widget-ready (preparado para LightWidget/Elfsight)
- **Justificativa:** Padrão Petderma. Funciona com placeholders (atuais) ou substituível por widget externo (iframe). Comentário HTML indica ponto de integração.

### Conteúdo
- **Pre-título:** `@vetpiera`
- **Título:** `Acompanhe nosso dia a dia no Instagram.`
- **CTA pill:** `ph-instagram-logo` + "Seguir no Instagram" → `https://instagram.com/vetpiera`
- **Grid 6 tiles** (cada link para o perfil): cachorro-caramelo, gato-brasil-premium, dr-ryan, dra-diana, estrutura-fisio-02, hospital-uti
- **HTML comment:** `<!-- Para feed real: substituir .instagram__grid pelo iframe do widget LightWidget/Elfsight -->`

### Layout
- Header centralizado margin-bottom `clamp(36px, 5vw, 56px)`
- Grid `repeat(6, 1fr)` gap 8px
- Tile aspect 1/1, radius 8px, overflow hidden

### Tipografia / Cores
- Pre-título: DM Sans 600 · 0.95rem · dourado
- Title: DM Serif Display · fs-h2
- CTA pill: bg primary · white · padding 12px 24px · radius 999px. Hover: dark + translateY(-2px)
- Tile overlay hover: rgba(15,45,36,0.55) + `ph-instagram-logo` 28px white centered

### Animações
- Img scale 1→1.08 (500ms)
- Overlay opacity 0→1 (240ms)

### Responsividade
- **≤900px:** grid 3 colunas
- **≤480px:** grid 2 colunas

---

## Seção 10: BOOK CTA (Agendamento WhatsApp)

### Arquétipo e Constraints
- **Arquétipo:** Split com Photo + Color Block dramático
- **Constraints:** Gradient Background diagonal (Cor) · Photo Floating em card 4/3 (Layout) · Glow Decoration radial dourado (Efeitos)
- **Justificativa:** Encerra a página em alto contraste (fundo escuro pela primeira vez no fluxo). CTA final ganha peso visual diferente.

### Conteúdo
- **Pre-título:** `Agendamento`
- **Título:** `Pronto para cuidar do seu pet?`
- **Sub:** `Fale com nossa equipe pelo WhatsApp e agende uma consulta ou tire dúvidas sobre emergências, especialidades e exames.`
- **CTA primário:** pill grande "Falar pelo WhatsApp" + `ph-fill ph-whatsapp-logo` → `wa.me/5511963326376`
- **CTA secundário:** `ph-phone` + `(11) 2746-7292 — 24h` → `tel:`
- **Foto:** cachorro-caramelo, aspect 4/3, radius 20px, shadow 0 24px 60px rgba(0,0,0,.35)

### Layout
- Padding-block `--sp-section`
- Container max-width 1200px, grid `1.2fr 1fr`, gap `clamp(32px, 5vw, 64px)`, align center

### Tipografia / Cores
- Background: `linear-gradient(135deg, var(--clr-dark) 0%, var(--clr-primary) 100%)`
- Decoração: `radial-gradient(circle at 80% 20%, rgba(201,168,76,.15), transparent 50%)`
- Pre-título: DM Sans 600 · 0.8125rem · uppercase · 0.18em · dourado
- Title: DM Serif Display · `clamp(2.25rem, 4.5vw, 3.5rem)` · white
- Sub: DM Sans 400 · 1.05rem · rgba(255,255,255,.85) · max-width 480px
- WhatsApp btn: dourado (não verde) pra destacar como ação final

### Responsividade
- **≤860px:** grid 1 coluna, foto em cima (order -1), aspect 16/10

---

## Footer (mantido)

3 colunas com mapas embed.
- **Col 1 (brand):** Logo + tagline + social (Instagram, Facebook, WhatsApp)
- **Col 2 (Hospital 24h):** links serviços + tag 24h · Tel · Email · Endereço + Map iframe
- **Col 3 (Especialidades):** links serviços + horário · Tel · Email · Endereço + Map iframe
- **Bottom:** `© 2026 VetPiera · Grupo Piera. Todos os direitos reservados.`

---

## Variedade entre seções consecutivas

| # | Arquétipo | Densidade | Constraint principal |
|---|-----------|-----------|----------------------|
| 1 | Split com Overlap | Balanced | Gradient Mesh |
| 2 | Type Hero Editorial | Sparse | Color Blocking |
| 3 | Split Alternado | Balanced | Badge Overlapping |
| 4 | Grid Modular | Balanced | Hover Lift |
| 5 | Editorial Rows | Sparse | Type numérico outline |
| 6 | Scroll Horizontal | Dense | Scroll Snap |
| 7 | Bento 3D Flip | Balanced | Color Blocking dark/light |
| 8 | CSS Carousel | Sparse | Dark Mode |
| 9 | Gallery Wall | Dense | Hover Overlay |
| 10 | Split Color Block | Balanced | Gradient Background |

✓ Nenhum arquétipo repetido em seções consecutivas.
✓ Densidade alterna (Balanced → Sparse → Balanced → ...).
✓ Cor alterna fundo claro ↔ escuro nas key sections (1 claro, 7 dark card, 8 dark, 10 dark).
