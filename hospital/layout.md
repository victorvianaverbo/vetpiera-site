# VetPiera — Hospital Page Layout Specification

**File:** `hospital/layout.md`
**Last updated:** 2026-03-13
**Designer:** Art Director (Claude)
**Status:** Ready for development

> This file assumes Global Tokens defined in `home/layout.md` are already applied via the shared CSS.
> All CSS tokens (colors, fonts, spacing, radius, easing) are inherited from `:root`.

---

## Page-Level Notes

- URL: `/hospital`
- Title: `Hospital Veterinário 24h | VetPiera`
- Meta description: `Emergência veterinária 24 horas em São Paulo. UTI veterinária, cirurgia e internação com equipe especializada. VetPiera Hospital.`
- Nav state: highlight "Hospital" link in navigation

---

## Section 1 — Hero

**Archetype:** Hero Dominante (100vh full-bleed)
**Constraints:** Imagem Fullbleed + Mouse Spotlight + Counter Animation ("24h" stamp) + Grain Overlay

---

### HTML Structure

```html
<section class="hosp-hero" aria-label="Hospital Veterinário 24 horas">
  <!-- Mouse spotlight layer (JS-driven) -->
  <div class="hosp-hero__spotlight" id="heroSpotlight" aria-hidden="true"></div>
  <!-- Grain overlay -->
  <div class="hosp-hero__grain" aria-hidden="true"></div>

  <!-- Giant "24h" stamp (decorative, background) -->
  <div class="hosp-hero__stamp" aria-hidden="true">24h</div>

  <!-- Centered content -->
  <div class="hosp-hero__content">
    <span class="hosp-hero__eyebrow">Hospital Veterinário · São Paulo</span>
    <h1 class="hosp-hero__headline">
      Emergência veterinária<br>
      <em class="hosp-hero__em">24 horas.</em><br>
      Aqui, seu pet nunca<br>fica sem atendimento.
    </h1>
    <p class="hosp-hero__sub">Equipe médica de plantão, UTI equipada e centro cirúrgico disponíveis ininterruptamente para cuidar do que mais importa.</p>
    <div class="hosp-hero__actions">
      <a href="https://wa.me/5511991334520" class="btn btn--accent" target="_blank" rel="noopener">
        <i class="ph ph-whatsapp-logo" aria-hidden="true"></i> WhatsApp →
      </a>
      <a href="tel:+551123733144" class="btn btn--ghost">
        <i class="ph ph-phone" aria-hidden="true"></i> (11) 2373-3144
      </a>
    </div>
  </div>

  <!-- Scroll cue -->
  <div class="hosp-hero__scroll-cue" aria-hidden="true">
    <span class="hosp-hero__scroll-line"></span>
  </div>
</section>
```

---

### Layout CSS

```css
.hosp-hero {
  position: relative;
  width: 100%;
  min-height: 100svh;
  display: flex;
  align-items: center;
  overflow: hidden;

  /* Fullbleed background */
  background-image: url('/images/hospital-hero.jpg');
  background-size: cover;
  background-position: center center;
  /* Fallback gradient if image absent */
  background-color: #0a1e16;
}

/* Dark gradient overlay on photo */
.hosp-hero::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    135deg,
    rgba(10, 30, 22, 0.88) 0%,
    rgba(15, 45, 36, 0.75) 60%,
    rgba(8, 26, 22, 0.82) 100%
  );
  z-index: 1;
}

/* ── Mouse Spotlight ── */
.hosp-hero__spotlight {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    400px circle at var(--mx, 50%) var(--my, 50%),
    rgba(27, 77, 62, 0.15),
    transparent 60%
  );
  z-index: 2;
  pointer-events: none;
  transition: background 0.05s linear;
}

/* ── Grain Overlay ── */
.hosp-hero__grain {
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 256px 256px;
  opacity: 0.04;
  mix-blend-mode: overlay;
  z-index: 3;
  pointer-events: none;
}

/* ── Giant "24h" stamp ── */
.hosp-hero__stamp {
  position: absolute;
  bottom: clamp(32px, 5vw, 64px);
  right: clamp(32px, 5vw, 64px);
  font-family: var(--font-display);
  font-size: clamp(6rem, 16vw, 14rem);
  line-height: 1;
  color: rgba(255, 255, 255, 0.05);
  letter-spacing: -0.04em;
  user-select: none;
  pointer-events: none;
  z-index: 2;

  /* Initial state for animation */
  opacity: 0;
  transform: scale(0.7);
  animation: stampReveal 1000ms var(--ease-out-expo) 800ms forwards;
}

@keyframes stampReveal {
  from {
    opacity: 0;
    transform: scale(0.7);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* ── Content ── */
.hosp-hero__content {
  position: relative;
  z-index: 4;
  max-width: var(--container);
  width: 100%;
  margin-inline: auto;
  padding-inline: var(--pad-x);
  padding-block: clamp(120px, 16vw, 180px) clamp(80px, 10vw, 120px);
  display: flex;
  flex-direction: column;
  gap: 0;
}

/* ── Eyebrow ── */
.hosp-hero__eyebrow {
  display: inline-block;
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
  margin-bottom: clamp(16px, 2.5vw, 24px);

  opacity: 0;
  transform: translateY(16px);
  animation: fadeUp 550ms var(--ease-out-expo) 100ms forwards;
}

/* ── Headline ── */
.hosp-hero__headline {
  font-family: var(--font-display);
  font-size: var(--fs-hero);
  line-height: 1.08;
  color: #FFFFFF;
  letter-spacing: -0.025em;
  margin: 0 0 clamp(20px, 3vw, 32px);
  max-width: 700px;

  opacity: 0;
  transform: translateY(20px);
  animation: fadeUp 700ms var(--ease-out-expo) 250ms forwards;
}

/* Gold italic emphasis */
.hosp-hero__em {
  color: var(--clr-accent);
  font-style: italic;
}

/* ── Sub ── */
.hosp-hero__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: rgba(255, 255, 255, 0.72);
  line-height: 1.65;
  max-width: 540px;
  margin: 0 0 clamp(32px, 4vw, 48px);

  opacity: 0;
  transform: translateY(16px);
  animation: fadeUp 650ms var(--ease-out-expo) 400ms forwards;
}

/* ── CTAs ── */
.hosp-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;

  opacity: 0;
  transform: translateY(16px);
  animation: fadeUp 550ms var(--ease-out-expo) 550ms forwards;
}

/* ── Shared fadeUp keyframe ── */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(var(--from-y, 16px));
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ── Scroll cue ── */
.hosp-hero__scroll-cue {
  position: absolute;
  bottom: clamp(24px, 4vw, 40px);
  left: 50%;
  transform: translateX(-50%);
  z-index: 4;
  display: flex;
  flex-direction: column;
  align-items: center;
  opacity: 0;
  animation: fadeIn 600ms ease 1200ms forwards;
}

.hosp-hero__scroll-line {
  display: block;
  width: 1px;
  height: 48px;
  background: linear-gradient(to bottom, rgba(255,255,255,0.5), transparent);
  animation: scrollPulse 2s ease infinite;
}

@keyframes scrollPulse {
  0%   { transform: scaleY(1); opacity: 1; }
  50%  { transform: scaleY(0.5); opacity: 0.3; }
  100% { transform: scaleY(1); opacity: 1; }
}

@keyframes fadeIn {
  to { opacity: 1; }
}
```

---

### Mouse Spotlight JS

```js
const hero = document.querySelector('.hosp-hero');
const spotlight = document.getElementById('heroSpotlight');

if (hero && spotlight) {
  hero.addEventListener('mousemove', e => {
    const rect = hero.getBoundingClientRect();
    const x = ((e.clientX - rect.left) / rect.width * 100).toFixed(2);
    const y = ((e.clientY - rect.top) / rect.height * 100).toFixed(2);
    spotlight.style.setProperty('--mx', `${x}%`);
    spotlight.style.setProperty('--my', `${y}%`);
  });

  hero.addEventListener('mouseleave', () => {
    spotlight.style.setProperty('--mx', '50%');
    spotlight.style.setProperty('--my', '50%');
  });
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .hosp-hero__stamp {
    font-size: clamp(5rem, 22vw, 9rem);
    bottom: 20px;
    right: 16px;
  }
  .hosp-hero__headline {
    font-size: clamp(2.25rem, 7.5vw, 3.5rem);
  }
  .hosp-hero__actions {
    flex-direction: column;
    align-items: flex-start;
  }
  /* Disable spotlight on touch */
  .hosp-hero__spotlight {
    display: none;
  }
}
```

---

## Section 2 — Serviços Bento

**Archetype:** Bento Box Assimétrico
**Constraints:** Grid Assimétrico (card grande 2×2 + 3 cards menores) + Hover Flip nos menores + Overlap Elements ("Disponível agora" flutua)

---

### HTML Structure

```html
<section class="services" aria-label="Estrutura e serviços do hospital">
  <div class="services__container">

    <header class="services__header">
      <h2 class="services__title">Estrutura completa<br>para cada momento.</h2>
      <p class="services__sub">Do pronto-atendimento ao pós-operatório — temos tudo o que seu animal precisa em um único lugar.</p>
    </header>

    <div class="services__grid">

      <!-- LARGE CARD: Emergência & UTI (col 1-2, row 1-2) -->
      <article class="services__card services__card--large" aria-label="Emergência e UTI veterinária">
        <!-- "Disponível agora" floating tag -->
        <span class="services__card-live" aria-label="Atendimento disponível agora">
          <span class="services__card-live-dot" aria-hidden="true"></span>
          Disponível agora
        </span>
        <div class="services__card-large-inner">
          <!-- Body (left) -->
          <div class="services__card-large-body">
            <div class="services__card-category">
              <i class="ph ph-first-aid-kit" aria-hidden="true"></i>
              <span>Emergência & UTI</span>
            </div>
            <h3 class="services__card-name">Pronto-atendimento e cuidados intensivos veterinários.</h3>
            <p class="services__card-desc">Equipe de plantão 24h, UTI com monitoramento multiparamétrico contínuo, ventilação mecânica e suporte transfusional.</p>
            <ul class="services__card-list">
              <li>Triagem imediata</li>
              <li>UTI com 12 vagas</li>
              <li>Oxigenoterapia</li>
              <li>Hemoterapia</li>
            </ul>
            <a href="/hospital#emergencia" class="btn btn--ghost services__card-cta">Saiba mais →</a>
          </div>
          <!-- Photo (right) -->
          <div class="services__card-large-photo" aria-hidden="true"></div>
        </div>
      </article>

      <!-- SMALL CARD 1: Cirurgia & Anestesia -->
      <article class="services__card services__card--small" tabindex="0" aria-label="Cirurgia e Anestesia — clique para ver detalhes">
        <div class="services__flip">
          <!-- Front -->
          <div class="services__flip-front">
            <i class="ph ph-scalpel" aria-hidden="true"></i>
            <h3 class="services__flip-name">Cirurgia &<br>Anestesia</h3>
            <p class="services__flip-desc">Centro cirúrgico completo com anestesista residente.</p>
          </div>
          <!-- Back -->
          <div class="services__flip-back" aria-hidden="true">
            <p class="services__flip-back-title">O que oferecemos:</p>
            <ul class="services__flip-back-list">
              <li>Cirurgia geral e especializada</li>
              <li>Laparoscopia</li>
              <li>Monitoração anestésica avançada</li>
              <li>Recuperação assistida</li>
            </ul>
          </div>
        </div>
      </article>

      <!-- SMALL CARD 2: Diagnóstico -->
      <article class="services__card services__card--small" tabindex="0" aria-label="Diagnóstico por imagem — clique para ver detalhes">
        <div class="services__flip">
          <div class="services__flip-front">
            <i class="ph ph-scan" aria-hidden="true"></i>
            <h3 class="services__flip-name">Diagnóstico<br>por Imagem</h3>
            <p class="services__flip-desc">Tomografia, ressonância, ecocardiografia e mais.</p>
          </div>
          <div class="services__flip-back" aria-hidden="true">
            <p class="services__flip-back-title">O que oferecemos:</p>
            <ul class="services__flip-back-list">
              <li>Tomografia computadorizada</li>
              <li>Ultrassonografia</li>
              <li>Ecocardiograma</li>
              <li>Radiologia digital</li>
            </ul>
          </div>
        </div>
      </article>

      <!-- SMALL CARD 3: Internação -->
      <article class="services__card services__card--small" tabindex="0" aria-label="Internação veterinária — clique para ver detalhes">
        <div class="services__flip">
          <div class="services__flip-front">
            <i class="ph ph-bed" aria-hidden="true"></i>
            <h3 class="services__flip-name">Internação<br>Veterinária</h3>
            <p class="services__flip-desc">Acompanhamento contínuo com equipe de enfermagem.</p>
          </div>
          <div class="services__flip-back" aria-hidden="true">
            <p class="services__flip-back-title">O que oferecemos:</p>
            <ul class="services__flip-back-list">
              <li>Internação separada por espécie</li>
              <li>Isolamento infeccioso</li>
              <li>Monitoramento 24h</li>
              <li>Atualização diária ao tutor</li>
            </ul>
          </div>
        </div>
      </article>

    </div>
  </div>
</section>
```

---

### Layout CSS

```css
.services {
  background: var(--clr-bg);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
}

.services__container {
  max-width: var(--container);
  margin-inline: auto;
}

/* ── Section header ── */
.services__header {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: clamp(32px, 4vw, 64px);
  align-items: end;
  margin-bottom: clamp(48px, 6vw, 72px);
}

.services__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0;
}

.services__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  margin: 0;
  max-width: 420px;
}

/* ── Bento Grid ── */
.services__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto auto;
  gap: clamp(12px, 2vw, 20px);
}

/* ── Large card (Emergência) ── */
.services__card--large {
  grid-column: 1 / 3; /* spans 2 columns */
  grid-row: 1 / 3;    /* spans 2 rows */
  background: var(--clr-dark);
  border-radius: var(--radius-lg);
  overflow: hidden;
  position: relative;
  transition: transform 400ms var(--ease-out-expo), box-shadow 400ms var(--ease-out-expo);
}

.services__card--large:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 48px rgba(15,45,36,0.18);
}

/* Floating "Disponível agora" tag */
.services__card-live {
  position: absolute;
  top: 24px;
  right: 24px;
  z-index: 3;
  display: flex;
  align-items: center;
  gap: 8px;
  background: rgba(201,168,76,0.15);
  border: 1px solid rgba(201,168,76,0.30);
  color: var(--clr-accent);
  border-radius: 100px;
  padding: 6px 14px;
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.04em;
}

/* Pulsing live dot */
.services__card-live-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--clr-accent);
  animation: livePulse 2s ease infinite;
  flex-shrink: 0;
}

@keyframes livePulse {
  0%   { box-shadow: 0 0 0 0 rgba(201,168,76,0.5); }
  70%  { box-shadow: 0 0 0 6px rgba(201,168,76,0); }
  100% { box-shadow: 0 0 0 0 rgba(201,168,76,0); }
}

/* Large card inner — split body/photo */
.services__card-large-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100%;
  min-height: 420px;
}

.services__card-large-body {
  padding: clamp(32px, 4vw, 48px);
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: 16px;
}

.services__card-large-photo {
  background-image: url('/images/hospital-uti.jpg');
  background-size: cover;
  background-position: center;
  /* Fallback gradient */
  background-color: #0a1e16;
  position: relative;
}

/* Gradient blending photo into body */
.services__card-large-photo::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to right,
    rgba(15,45,36,0.5) 0%,
    transparent 40%
  );
  pointer-events: none;
}

/* Large card typography */
.services__card-category {
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-accent);
}

.services__card-category i {
  font-size: 1rem;
}

.services__card-name {
  font-family: var(--font-display);
  font-size: clamp(1.4rem, 2.5vw, 1.9rem);
  line-height: 1.2;
  color: #FFFFFF;
  letter-spacing: -0.01em;
  margin: 0;
}

.services__card-desc {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  line-height: 1.6;
  color: rgba(255,255,255,0.60);
  margin: 0;
}

.services__card-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.services__card-list li {
  font-family: var(--font-body);
  font-size: 0.875rem;
  color: rgba(255,255,255,0.50);
  padding-left: 16px;
  position: relative;
}

.services__card-list li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--clr-accent);
  opacity: 0.7;
}

/* ── Small cards (flip) ── */
.services__card--small {
  border-radius: var(--radius-lg);
  overflow: hidden;
  position: relative;
  perspective: 800px;
  min-height: 200px;
  cursor: pointer;
  background: var(--clr-surface);
  border: 1px solid var(--clr-border);
}

.services__flip {
  width: 100%;
  height: 100%;
  position: absolute;
  inset: 0;
  transform-style: preserve-3d;
  transition: transform 600ms cubic-bezier(0.16, 1, 0.3, 1);
  will-change: transform;
}

.services__card--small:hover .services__flip,
.services__card--small:focus .services__flip {
  transform: rotateY(180deg);
}

.services__flip-front,
.services__flip-back {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  padding: clamp(24px, 3vw, 36px);
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.services__flip-front {
  background: var(--clr-surface);
}

.services__flip-back {
  background: var(--clr-primary);
  transform: rotateY(180deg);
}

/* Front face icon */
.services__flip-front > i {
  font-size: 2rem;
  color: var(--clr-primary);
  position: absolute;
  top: clamp(24px, 3vw, 36px);
  left: clamp(24px, 3vw, 36px);
}

.services__flip-name {
  font-family: var(--font-display);
  font-size: 1.3rem;
  line-height: 1.2;
  color: var(--clr-text);
  margin: 0 0 8px;
}

.services__flip-desc {
  font-family: var(--font-body);
  font-size: 0.875rem;
  color: var(--clr-muted);
  line-height: 1.55;
  margin: 0;
}

/* Back face content */
.services__flip-back-title {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-accent);
  margin: 0 0 16px;
}

.services__flip-back-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.services__flip-back-list li {
  font-family: var(--font-body);
  font-size: 0.9rem;
  color: rgba(255,255,255,0.85);
  padding-left: 18px;
  position: relative;
  line-height: 1.4;
}

.services__flip-back-list li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 7px;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--clr-accent);
}
```

---

### Mobile Flip (JS)

```js
// Mobile: flip on click/tap
if ('ontouchstart' in window) {
  document.querySelectorAll('.services__card--small').forEach(card => {
    card.addEventListener('click', () => {
      card.querySelector('.services__flip').style.transform =
        card.classList.toggle('is-flipped') ? 'rotateY(180deg)' : 'rotateY(0deg)';
    });
  });
}
```

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .services__header {
    grid-template-columns: 1fr;
  }
  .services__sub {
    max-width: 100%;
  }
  .services__grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .services__card--large {
    grid-column: 1 / 3;
    grid-row: 1;
  }
  .services__card-large-inner {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  .services__card-large-photo {
    height: 240px;
    order: -1;
  }
}
```

#### < 640px (mobile)

```css
@media (max-width: 640px) {
  .services__grid {
    grid-template-columns: 1fr;
  }
  .services__card--large {
    grid-column: 1;
    grid-row: 1;
  }
  .services__card--small {
    min-height: 180px;
  }
  /* Disable hover flip on mobile, use click JS above */
  .services__card--small:hover .services__flip {
    transform: none;
  }
  .services__card--small.is-flipped .services__flip {
    transform: rotateY(180deg);
  }
}
```

---

## Section 3 — Especialidades Disponíveis (Scroll Horizontal)

**Archetype:** Scroll Horizontal
**Constraints:** Drag Horizontal + Overflow Visible + Fade nos edges + Sticky-ish title

---

### HTML Structure

```html
<section class="hosp-specs" aria-label="Especialidades disponíveis no hospital">
  <div class="hosp-specs__head">
    <h2 class="hosp-specs__title">Especialidades disponíveis.</h2>
    <p class="hosp-specs__sub">Contamos com especialistas das principais áreas para um cuidado completo e integrado do seu animal.</p>
  </div>

  <!-- Fade edges (CSS ::before/::after) + scrollable track -->
  <div class="hosp-specs__stage" id="specsStage">
    <div class="hosp-specs__track" id="specsTrack" role="list">

      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-brain" aria-hidden="true"></i>
        <span>Neurologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-bone" aria-hidden="true"></i>
        <span>Ortopedia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-heartbeat" aria-hidden="true"></i>
        <span>Cardiologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-activity" aria-hidden="true"></i>
        <span>Fisioterapia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-eye" aria-hidden="true"></i>
        <span>Oftalmologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-tooth" aria-hidden="true"></i>
        <span>Odontologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-drop" aria-hidden="true"></i>
        <span>Oncologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-flask" aria-hidden="true"></i>
        <span>Endocrinologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-shield-check" aria-hidden="true"></i>
        <span>Imunologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-scissors" aria-hidden="true"></i>
        <span>Dermatologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-tree" aria-hidden="true"></i>
        <span>Medicina Felina</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-baby" aria-hidden="true"></i>
        <span>Neonatologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-syringe" aria-hidden="true"></i>
        <span>Anestesiologia</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-cpu" aria-hidden="true"></i>
        <span>Diagnóstico</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-person-arms-spread" aria-hidden="true"></i>
        <span>Reabilitação</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-circles-three" aria-hidden="true"></i>
        <span>Comportamento</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-chart-line-up" aria-hidden="true"></i>
        <span>Nutrição Clínica</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-stethoscope" aria-hidden="true"></i>
        <span>Clínica Geral</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-globe" aria-hidden="true"></i>
        <span>Acupuntura</span>
      </div>
      <div class="hosp-specs__chip" role="listitem">
        <i class="ph ph-sparkle" aria-hidden="true"></i>
        <span>+ outras</span>
      </div>

    </div>
  </div>

  <div class="hosp-specs__footer">
    <a href="/especialidades" class="btn btn--primary">Ver todas as especialidades →</a>
  </div>
</section>
```

---

### Layout CSS

```css
.hosp-specs {
  background: var(--clr-primary-pale);
  padding-block: var(--sp-section);
  overflow: hidden; /* Contains the stage visually */
}

/* ── Header ── */
.hosp-specs__head {
  max-width: var(--container);
  margin-inline: auto;
  padding-inline: var(--pad-x);
  text-align: center;
  margin-bottom: clamp(40px, 5vw, 64px);
}

.hosp-specs__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0 0 16px;
}

.hosp-specs__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  max-width: 560px;
  margin-inline: auto;
}

/* ── Scrollable stage ── */
.hosp-specs__stage {
  position: relative;
  /* Fade edges using pseudo-elements */
}

.hosp-specs__stage::before,
.hosp-specs__stage::after {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  width: 80px;
  z-index: 1;
  pointer-events: none;
}

.hosp-specs__stage::before {
  left: 0;
  background: linear-gradient(to right, var(--clr-primary-pale), transparent);
}

.hosp-specs__stage::after {
  right: 0;
  background: linear-gradient(to left, var(--clr-primary-pale), transparent);
}

/* ── Track (scrollable) ── */
.hosp-specs__track {
  display: flex;
  gap: 12px;
  padding: 8px var(--pad-x) 24px;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  cursor: grab;
  /* Hide scrollbar */
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.hosp-specs__track::-webkit-scrollbar {
  display: none;
}

.hosp-specs__track.is-dragging {
  cursor: grabbing;
  user-select: none;
}

/* ── Individual chip cards ── */
.hosp-specs__chip {
  flex-shrink: 0;
  min-width: 160px;
  height: 90px;
  background: var(--clr-surface);
  border: 1px solid var(--clr-border);
  border-radius: var(--radius);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  scroll-snap-align: start;
  transition:
    border-color 250ms ease,
    box-shadow 250ms ease,
    transform 250ms ease;
  padding: 16px;
}

.hosp-specs__chip:hover {
  border-color: var(--clr-primary);
  box-shadow: 0 4px 16px rgba(27,77,62,0.10);
  transform: translateY(-3px);
}

.hosp-specs__chip i {
  font-size: 1.375rem;
  color: var(--clr-primary);
}

.hosp-specs__chip span {
  font-family: var(--font-body);
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--clr-text);
  text-align: center;
  line-height: 1.3;
}

/* ── Footer CTA ── */
.hosp-specs__footer {
  display: flex;
  justify-content: center;
  padding-inline: var(--pad-x);
  padding-top: clamp(32px, 4vw, 48px);
}
```

---

### Drag-to-Scroll JS

```js
const track = document.getElementById('specsTrack');

if (track) {
  let isDragging = false;
  let startX = 0;
  let scrollLeft = 0;

  track.addEventListener('mousedown', e => {
    isDragging = true;
    startX = e.pageX - track.offsetLeft;
    scrollLeft = track.scrollLeft;
    track.classList.add('is-dragging');
  });

  track.addEventListener('mouseleave', () => {
    isDragging = false;
    track.classList.remove('is-dragging');
  });

  track.addEventListener('mouseup', () => {
    isDragging = false;
    track.classList.remove('is-dragging');
  });

  track.addEventListener('mousemove', e => {
    if (!isDragging) return;
    e.preventDefault();
    const x = e.pageX - track.offsetLeft;
    const walk = (x - startX) * 1.5; // drag speed multiplier
    track.scrollLeft = scrollLeft - walk;
  });
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .hosp-specs__chip {
    min-width: 130px;
    height: 80px;
  }
  .hosp-specs__stage::before,
  .hosp-specs__stage::after {
    width: 40px;
  }
}
```

---

## Section 4 — Diferenciais (Timeline Vertical)

**Archetype:** Timeline Vertical
**Constraints:** Clip Reveal + View Timeline CSS + Off-Grid números + Stagger

---

### HTML Structure

```html
<section class="diffs" aria-label="Diferenciais do hospital">
  <div class="diffs__container">

    <header class="diffs__header">
      <h2 class="diffs__title">O que torna nosso<br>hospital diferente.</h2>
    </header>

    <!-- Vertical line (absolute, sits in .diffs__timeline) -->
    <div class="diffs__timeline" aria-hidden="true">
      <div class="diffs__line"></div>
    </div>

    <div class="diffs__list">

      <div class="diffs__item" style="--item-i: 0">
        <div class="diffs__dot" aria-hidden="true"></div>
        <div class="diffs__body">
          <span class="diffs__num" aria-hidden="true">01</span>
          <div class="diffs__text-group">
            <div class="diffs__icon-title">
              <i class="ph ph-car" aria-hidden="true"></i>
              <h3 class="diffs__name">Estacionamento gratuito</h3>
            </div>
            <p class="diffs__desc">Nosso hospital conta com estacionamento exclusivo e gratuito para tutores durante o atendimento — sem preocupação com vagas em momentos difíceis.</p>
          </div>
        </div>
      </div>

      <div class="diffs__item" style="--item-i: 1">
        <div class="diffs__dot" aria-hidden="true"></div>
        <div class="diffs__body">
          <span class="diffs__num" aria-hidden="true">02</span>
          <div class="diffs__text-group">
            <div class="diffs__icon-title">
              <i class="ph ph-house-line" aria-hidden="true"></i>
              <h3 class="diffs__name">Internação separada por espécie</h3>
            </div>
            <p class="diffs__desc">Cães e gatos são internados em alas separadas, reduzindo o estresse e garantindo o bem-estar de todos os animais durante a recuperação.</p>
          </div>
        </div>
      </div>

      <div class="diffs__item" style="--item-i: 2">
        <div class="diffs__dot" aria-hidden="true"></div>
        <div class="diffs__body">
          <span class="diffs__num" aria-hidden="true">03</span>
          <div class="diffs__text-group">
            <div class="diffs__icon-title">
              <i class="ph ph-virus" aria-hidden="true"></i>
              <h3 class="diffs__name">Isolamento infeccioso</h3>
            </div>
            <p class="diffs__desc">Área dedicada a casos de doenças infectocontagiosas, com protocolo rigoroso de biossegurança para proteger os demais pacientes internados.</p>
          </div>
        </div>
      </div>

      <div class="diffs__item" style="--item-i: 3">
        <div class="diffs__dot" aria-hidden="true"></div>
        <div class="diffs__body">
          <span class="diffs__num" aria-hidden="true">04</span>
          <div class="diffs__text-group">
            <div class="diffs__icon-title">
              <i class="ph ph-users-three" aria-hidden="true"></i>
              <h3 class="diffs__name">Equipe multidisciplinar</h3>
            </div>
            <p class="diffs__desc">Médicos veterinários de diferentes especialidades atuam em conjunto para casos complexos, garantindo um diagnóstico mais preciso e completo.</p>
          </div>
        </div>
      </div>

      <div class="diffs__item" style="--item-i: 4">
        <div class="diffs__dot" aria-hidden="true"></div>
        <div class="diffs__body">
          <span class="diffs__num" aria-hidden="true">05</span>
          <div class="diffs__text-group">
            <div class="diffs__icon-title">
              <i class="ph ph-cpu" aria-hidden="true"></i>
              <h3 class="diffs__name">Tecnologia cirúrgica avançada</h3>
            </div>
            <p class="diffs__desc">Centro cirúrgico equipado com laparoscópico, sistema de monitoração multiparamétrica e anestesia inalatória de precisão para procedimentos de alta complexidade.</p>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

---

### Layout CSS

```css
.diffs {
  background: var(--clr-surface);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
}

.diffs__container {
  max-width: var(--container);
  margin-inline: auto;
  position: relative;
}

/* ── Header ── */
.diffs__header {
  text-align: center;
  margin-bottom: clamp(64px, 8vw, 96px);
}

.diffs__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0;
}

/* ── Timeline line wrapper ── */
.diffs__timeline {
  position: absolute;
  /* Center line at 50% on desktop */
  left: 50%;
  top: 0;
  bottom: 0;
  transform: translateX(-50%);
  width: 1px;
  pointer-events: none;
}

.diffs__line {
  width: 1px;
  height: 100%;
  background: linear-gradient(to bottom, transparent, var(--clr-border) 10%, var(--clr-border) 90%, transparent);
}

/* ── List ── */
.diffs__list {
  display: flex;
  flex-direction: column;
  gap: 0;
}

/* ── Individual item ── */
.diffs__item {
  display: grid;
  grid-template-columns: 1fr 24px 1fr; /* left content | dot | right content */
  align-items: start;
  gap: 0 clamp(32px, 4vw, 64px);
  padding-block: clamp(40px, 5vw, 64px);
  position: relative;

  /* CSS View Timeline animation */
  animation: clipReveal 600ms ease-out both;
  animation-timeline: view();
  animation-range: entry 0% entry 35%;
  animation-delay: calc(var(--item-i, 0) * 100ms);
}

/* Odd items: content on right side of line */
.diffs__item:nth-child(odd) .diffs__body {
  grid-column: 3;
  grid-row: 1;
}
.diffs__item:nth-child(odd) .diffs__dot {
  grid-column: 2;
  grid-row: 1;
}
/* Invisible spacer for odd — left column is empty */
.diffs__item:nth-child(odd)::before {
  content: '';
  grid-column: 1;
}

/* Even items: content on left side of line */
.diffs__item:nth-child(even) .diffs__body {
  grid-column: 1;
  grid-row: 1;
  text-align: right;
}
.diffs__item:nth-child(even) .diffs__dot {
  grid-column: 2;
  grid-row: 1;
}

/* ── Dot ── */
.diffs__dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--clr-accent);
  border: 3px solid var(--clr-surface);
  position: relative;
  top: 8px;
  /* Center in the 24px column */
  justify-self: center;
  flex-shrink: 0;
  box-shadow: 0 0 0 1px var(--clr-accent);
}

/* ── Body ── */
.diffs__body {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

/* ── Off-grid number ── */
.diffs__num {
  font-family: var(--font-display);
  font-size: clamp(3rem, 7vw, 5rem);
  line-height: 1;
  color: transparent;
  -webkit-text-stroke: 1px rgba(27,77,62,0.12);
  user-select: none;
  display: block;
  /* Off-grid: number overflows its column slightly */
  margin-inline: -8px;
}

/* ── Icon + title row ── */
.diffs__icon-title {
  display: flex;
  align-items: center;
  gap: 10px;
}

.diffs__icon-title i {
  font-size: 1.375rem;
  color: var(--clr-accent);
  flex-shrink: 0;
}

.diffs__name {
  font-family: var(--font-display);
  font-size: 1.4rem;
  line-height: 1.25;
  color: var(--clr-text);
  margin: 0;
}

.diffs__desc {
  font-family: var(--font-body);
  font-size: 0.95rem;
  line-height: 1.65;
  color: var(--clr-muted);
  margin: 0;
}

/* Even: right-align text group */
.diffs__item:nth-child(even) .diffs__icon-title {
  flex-direction: row-reverse;
  justify-content: flex-end;
}

/* ── Keyframes ── */
@keyframes clipReveal {
  from {
    clip-path: polygon(0 0, 100% 0, 100% 0, 0 0);
    opacity: 0;
  }
  to {
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
    opacity: 1;
  }
}
```

---

### Fallback JS (no animation-timeline support)

```js
const supportsTimeline = CSS.supports('animation-timeline', 'view()');
if (!supportsTimeline) {
  const items = document.querySelectorAll('.diffs__item');
  const io = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        const delay = parseInt(e.target.style.getPropertyValue('--item-i') || 0) * 100;
        setTimeout(() => {
          e.target.style.cssText += '; animation: clipReveal 600ms ease-out both;';
          io.unobserve(e.target);
        }, delay);
      }
    });
  }, { threshold: 0.15 });
  items.forEach(item => {
    item.style.opacity = '0';
    io.observe(item);
  });
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  /* Stack all items on same side (left of line) */
  .diffs__timeline {
    left: 28px;
    transform: none;
  }

  .diffs__item {
    grid-template-columns: 56px 1fr;
    gap: 0 20px;
    padding-block: clamp(28px, 4vw, 48px);
  }

  /* All items: dot in col 1, body in col 2 */
  .diffs__item .diffs__dot,
  .diffs__item:nth-child(even) .diffs__dot {
    grid-column: 1;
    grid-row: 1;
    justify-self: center;
    align-self: start;
    margin-top: 8px;
  }

  .diffs__item .diffs__body,
  .diffs__item:nth-child(even) .diffs__body {
    grid-column: 2;
    grid-row: 1;
    text-align: left;
  }

  .diffs__item:nth-child(even) .diffs__icon-title {
    flex-direction: row;
    justify-content: flex-start;
  }

  .diffs__num {
    font-size: clamp(2.5rem, 10vw, 4rem);
  }
}
```

---

## Section 5 — Contato

**Archetype:** Split Assimétrico (45/55)
**Constraints:** Dark Mode + Floating Cards (glassmorphism) + Imagem Fullbleed

---

### HTML Structure

```html
<section class="hosp-contact" aria-label="Contato e localização do hospital">
  <div class="hosp-contact__grid">

    <!-- Left: copy + info (45%) -->
    <div class="hosp-contact__left">
      <span class="hosp-contact__eyebrow">Plantão 24 horas</span>
      <h2 class="hosp-contact__title">Estamos abertos agora.</h2>
      <p class="hosp-contact__sub">Nosso hospital nunca fecha. Entre em contato pelo WhatsApp ou telefone — nossa equipe responde imediatamente.</p>

      <div class="hosp-contact__info-list">

        <div class="hosp-contact__info-item">
          <i class="ph ph-map-pin" aria-hidden="true"></i>
          <div>
            <p class="hosp-contact__info-label">Endereço</p>
            <p class="hosp-contact__info-value">Rua Itapeti, 154 — São Paulo, SP</p>
          </div>
        </div>

        <div class="hosp-contact__info-item">
          <i class="ph ph-clock" aria-hidden="true"></i>
          <div>
            <p class="hosp-contact__info-label">Horário</p>
            <p class="hosp-contact__info-value">24 horas · 7 dias por semana</p>
          </div>
        </div>

        <div class="hosp-contact__info-item">
          <i class="ph ph-phone" aria-hidden="true"></i>
          <div>
            <p class="hosp-contact__info-label">Telefone</p>
            <p class="hosp-contact__info-value">
              <a href="tel:+551123733144" class="hosp-contact__tel">(11) 2373-3144</a>
            </p>
          </div>
        </div>

        <div class="hosp-contact__info-item">
          <i class="ph ph-envelope" aria-hidden="true"></i>
          <div>
            <p class="hosp-contact__info-label">E-mail</p>
            <p class="hosp-contact__info-value">
              <a href="mailto:hospital@vetpiera.com.br" class="hosp-contact__tel">hospital@vetpiera.com.br</a>
            </p>
          </div>
        </div>

      </div>

      <a href="https://wa.me/5511991334520" class="btn btn--accent hosp-contact__cta" target="_blank" rel="noopener">
        <i class="ph ph-whatsapp-logo" aria-hidden="true"></i>
        Chamar no WhatsApp
      </a>
    </div>

    <!-- Right: map placeholder (55%) -->
    <div class="hosp-contact__right" aria-label="Mapa da localização">
      <div class="hosp-contact__map" aria-hidden="true">
        <!-- Replace with real Google Maps embed iframe -->
        <div class="hosp-contact__map-placeholder">
          <i class="ph ph-map-trifold" aria-hidden="true"></i>
          <span>Mapa</span>
        </div>
      </div>
      <!-- Floating glass card overlay -->
      <div class="hosp-contact__glass-card" aria-hidden="true">
        <div class="hosp-contact__glass-dot"></div>
        <p class="hosp-contact__glass-text">Aberto agora</p>
        <p class="hosp-contact__glass-sub">24h · 7 dias</p>
      </div>
    </div>

  </div>
</section>
```

---

### Layout CSS

```css
.hosp-contact {
  background: var(--clr-dark);
  overflow: hidden;
}

.hosp-contact__grid {
  display: grid;
  grid-template-columns: 45fr 55fr;
  min-height: 600px;
}

/* ── Left panel ── */
.hosp-contact__left {
  padding: clamp(64px, 8vw, 96px) var(--pad-x) clamp(64px, 8vw, 96px) clamp(24px, calc((100vw - var(--container)) / 2 + var(--pad-x)), 128px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: clamp(16px, 2vw, 24px);
}

.hosp-contact__eyebrow {
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
}

.hosp-contact__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: #FFFFFF;
  letter-spacing: -0.02em;
  margin: 0;
}

.hosp-contact__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: rgba(255,255,255,0.60);
  line-height: 1.65;
  max-width: 380px;
  margin: 0;
}

/* Info list */
.hosp-contact__info-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-block: clamp(16px, 2vw, 24px);
}

.hosp-contact__info-item {
  display: flex;
  align-items: flex-start;
  gap: 16px;
}

.hosp-contact__info-item > i {
  font-size: 1.25rem;
  color: var(--clr-accent);
  flex-shrink: 0;
  margin-top: 2px;
}

.hosp-contact__info-label {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.35);
  margin: 0 0 4px;
}

.hosp-contact__info-value {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  color: rgba(255,255,255,0.85);
  margin: 0;
  line-height: 1.5;
}

.hosp-contact__tel {
  color: rgba(255,255,255,0.85);
  text-decoration: none;
  transition: color 200ms ease;
}
.hosp-contact__tel:hover {
  color: var(--clr-accent);
}

/* CTA */
.hosp-contact__cta {
  align-self: flex-start;
  margin-top: 8px;
}
.hosp-contact__cta:hover {
  box-shadow: 0 8px 32px rgba(201,168,76,0.35);
}

/* ── Right panel (map) ── */
.hosp-contact__right {
  position: relative;
  background: rgba(255,255,255,0.04);
  border-left: 1px solid rgba(255,255,255,0.08);
}

.hosp-contact__map {
  width: 100%;
  height: 100%;
  min-height: 400px;
  /* Replace with: <iframe src="maps url" style="width:100%;height:100%;border:0;"> */
}

/* Map placeholder styling */
.hosp-contact__map-placeholder {
  width: 100%;
  height: 100%;
  min-height: 400px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  color: rgba(255,255,255,0.20);
  font-family: var(--font-body);
  font-size: 0.875rem;
}

.hosp-contact__map-placeholder i {
  font-size: 2.5rem;
}

/* ── Floating glass card ── */
.hosp-contact__glass-card {
  position: absolute;
  bottom: 32px;
  left: 24px;
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px) saturate(1.5);
  -webkit-backdrop-filter: blur(20px) saturate(1.5);
  border: 1px solid rgba(255,255,255,0.14);
  border-radius: var(--radius);
  padding: 16px 20px;
  display: flex;
  align-items: center;
  gap: 12px;
  min-width: 160px;
}

.hosp-contact__glass-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #4ade80; /* green alive dot */
  flex-shrink: 0;
  animation: livePulse 2s ease infinite; /* reuse keyframe from services section */
  box-shadow: 0 0 0 0 rgba(74,222,128,0.5);
}

@keyframes livePulse {
  0%   { box-shadow: 0 0 0 0 rgba(74,222,128,0.5); }
  70%  { box-shadow: 0 0 0 8px rgba(74,222,128,0); }
  100% { box-shadow: 0 0 0 0 rgba(74,222,128,0); }
}

.hosp-contact__glass-text {
  font-family: var(--font-body);
  font-size: 0.875rem;
  font-weight: 600;
  color: #FFFFFF;
  margin: 0;
}

.hosp-contact__glass-sub {
  font-family: var(--font-body);
  font-size: 0.75rem;
  color: rgba(255,255,255,0.50);
  margin: 2px 0 0;
}
```

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .hosp-contact__grid {
    grid-template-columns: 1fr 1fr;
  }
  .hosp-contact__left {
    padding-left: var(--pad-x);
  }
}
```

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .hosp-contact__grid {
    grid-template-columns: 1fr;
  }
  /* Map comes first on mobile */
  .hosp-contact__right {
    order: -1;
    border-left: none;
    border-bottom: 1px solid rgba(255,255,255,0.08);
  }
  .hosp-contact__map,
  .hosp-contact__map-placeholder {
    min-height: auto;
    aspect-ratio: 16 / 9;
  }
  .hosp-contact__left {
    padding-block: clamp(48px, 8vw, 72px);
  }
  .hosp-contact__sub {
    max-width: 100%;
  }
}
```

---

## Global Accessibility Notes (Hospital-specific)

- `.hosp-hero__stamp` has `aria-hidden="true"` — it is purely decorative
- Spotlight div has `aria-hidden="true"` and `pointer-events: none`
- All flip cards have `tabindex="0"` and respond to `Enter`/`Space` for keyboard flip
- Map area: if iframe is used, provide `title="Mapa de localização da VetPiera"`
- `prefers-reduced-motion`: skip all `animation` properties, show final state:

```css
@media (prefers-reduced-motion: reduce) {
  .hosp-hero__eyebrow,
  .hosp-hero__headline,
  .hosp-hero__sub,
  .hosp-hero__actions,
  .hosp-hero__stamp {
    animation: none;
    opacity: 1;
    transform: none;
  }
  .diffs__item {
    animation: none;
    opacity: 1;
    clip-path: none;
  }
  .services__flip {
    transition: none;
  }
  .hosp-hero__scroll-line {
    animation: none;
  }
}
```

---

## Asset Requirements

| Asset | Dimensions | Format | Notes |
|---|---|---|---|
| `/images/hospital-hero.jpg` | 1920×1080px min | JPG | Dark vet clinic interior, emergency mood |
| `/images/hospital-uti.jpg` | 800×600px | JPG | ICU/UTI environment, green tones |
| Phosphor Icons | CDN | SVG font | All `ph-` classes used above |
