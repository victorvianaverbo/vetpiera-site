# VetPiera — Especialidades Page Layout Specification

**File:** `especialidades/layout.md`
**Last updated:** 2026-03-13
**Designer:** Art Director (Claude)
**Status:** Ready for development

> This file assumes Global Tokens defined in `home/layout.md` are already applied via the shared CSS.
> All CSS tokens (colors, fonts, spacing, radius, easing) are inherited from `:root`.

---

## Page-Level Notes

- URL: `/especialidades`
- Title: `25 Especialidades Veterinárias | VetPiera`
- Meta description: `Da neurologia à reabilitação — conheça as 25 especialidades veterinárias da VetPiera e agende uma consulta com nossos especialistas em São Paulo.`
- Nav state: highlight "Especialidades" link in navigation

---

## Section 1 — Hero

**Archetype:** Split Vertical (50/50)
**Constraints:** Overlap Elements (badge "25" invade a borda) + Counter Animation + Imagem Granulada + Fade Left

---

### HTML Structure

```html
<section class="esp-hero" aria-label="Especialidades veterinárias VetPiera">

  <!-- Left side: copy -->
  <div class="esp-hero__left">
    <span class="esp-hero__eyebrow" style="--delay: 0.05s">Clínica de Especialidades</span>
    <h1 class="esp-hero__headline" style="--delay: 0.2s">
      25 especialidades veterinárias.<br>
      Um cuidado feito <em class="esp-hero__em">sob medida</em><br>
      para o seu animal.
    </h1>
    <p class="esp-hero__sub" style="--delay: 0.38s">
      Da neurologia à reabilitação — contamos com especialistas de ponta para diagnosticar, tratar e cuidar com excelência em cada área da medicina veterinária.
    </p>
    <div class="esp-hero__actions" style="--delay: 0.55s">
      <a href="#contato" class="btn btn--accent">Agendar uma consulta →</a>
      <a href="#especialidades-lista" class="btn btn--outline-pale">Ver especialidades</a>
    </div>
  </div>

  <!-- Right side: photo with grain -->
  <div class="esp-hero__right" aria-hidden="true">
    <div class="esp-hero__photo"></div>
    <div class="esp-hero__grain"></div>
  </div>

  <!-- Badge "25" — overlaps the vertical dividing seam -->
  <div class="esp-hero__badge" aria-label="25 especialidades veterinárias">
    <div class="esp-hero__badge-inner">
      <span class="esp-hero__badge-num" id="espBadgeCounter">0</span>
      <div class="esp-hero__badge-labels">
        <span class="esp-hero__badge-l1">especialidades</span>
        <span class="esp-hero__badge-l2">veterinárias</span>
      </div>
    </div>
  </div>

</section>
```

---

### Layout CSS

```css
.esp-hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 100svh;
  position: relative;
  overflow: hidden;
}

/* ── Left panel ── */
.esp-hero__left {
  background: var(--clr-dark);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-block: clamp(120px, 14vw, 180px) clamp(80px, 10vw, 120px);
  padding-inline: var(--pad-x) clamp(48px, 6vw, 88px);
  position: relative;
  z-index: 2;
}

/* ── Right panel ── */
.esp-hero__right {
  position: relative;
  overflow: hidden;
}

.esp-hero__photo {
  width: 100%;
  height: 100%;
  background-image: url('/images/especialidades-hero.jpg');
  background-size: cover;
  background-position: center top;
  background-color: #0a1e16; /* fallback */
}

/* Grain overlay */
.esp-hero__grain {
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 256px 256px;
  opacity: 0.04;
  mix-blend-mode: overlay;
  pointer-events: none;
}

/* ── Badge (overlaps the seam) ── */
.esp-hero__badge {
  position: absolute;
  bottom: clamp(40px, 6vw, 72px);
  /* Centered on the 50/50 dividing line */
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
}

.esp-hero__badge-inner {
  background: var(--clr-surface);
  border-radius: 16px;
  padding: 20px 32px;
  display: flex;
  align-items: center;
  gap: 16px;
  box-shadow: 0 8px 32px rgba(15,45,36,0.20), 0 1px 3px rgba(15,45,36,0.08);
  white-space: nowrap;
}

.esp-hero__badge-num {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  line-height: 1;
  color: var(--clr-primary);
  letter-spacing: -0.02em;
  /* starts at 0, JS counts to 25 */
}

.esp-hero__badge-labels {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.esp-hero__badge-l1 {
  font-family: var(--font-body);
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--clr-muted);
  text-transform: uppercase;
  letter-spacing: 0.06em;
  line-height: 1.3;
}

.esp-hero__badge-l2 {
  font-family: var(--font-body);
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--clr-muted);
  text-transform: uppercase;
  letter-spacing: 0.06em;
  line-height: 1.3;
}
```

---

### Copy Animations (Fade Left)

```css
/* Shared fadeLeft keyframe */
@keyframes fadeLeft {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.esp-hero__eyebrow,
.esp-hero__headline,
.esp-hero__sub,
.esp-hero__actions {
  opacity: 0;
  /* Animation triggered via JS on DOMContentLoaded */
  animation: fadeLeft 650ms cubic-bezier(0.16, 1, 0.3, 1) var(--delay, 0s) both;
}

/* JS adds .is-loaded to the section to trigger CSS animations */
.esp-hero.is-loaded .esp-hero__eyebrow,
.esp-hero.is-loaded .esp-hero__headline,
.esp-hero.is-loaded .esp-hero__sub,
.esp-hero.is-loaded .esp-hero__actions {
  /* animation already specified above; just ensure opacity is reset */
}
```

```js
// Trigger animations on load
document.addEventListener('DOMContentLoaded', () => {
  document.querySelector('.esp-hero').classList.add('is-loaded');
});
```

---

### Typography CSS

```css
.esp-hero__eyebrow {
  display: inline-block;
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
  margin-bottom: clamp(16px, 2.5vw, 24px);
}

.esp-hero__headline {
  font-family: var(--font-display);
  font-size: var(--fs-hero);
  line-height: 1.08;
  color: #FFFFFF;
  letter-spacing: -0.025em;
  margin: 0 0 clamp(20px, 3vw, 32px);
}

.esp-hero__em {
  color: var(--clr-accent);
  font-style: italic;
}

.esp-hero__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: rgba(255,255,255,0.65);
  line-height: 1.65;
  max-width: 440px;
  margin: 0 0 clamp(32px, 4vw, 48px);
}

.esp-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
}

/* Ghost CTA variant for light-on-dark */
.btn--outline-pale {
  background: transparent;
  color: rgba(255,255,255,0.80);
  border-color: rgba(255,255,255,0.30);
}
.btn--outline-pale:hover {
  background: rgba(255,255,255,0.08);
  color: #FFFFFF;
  border-color: rgba(255,255,255,0.60);
  transform: translateY(-2px);
}
```

---

### Counter Animation — Badge "25"

**Trigger:** `IntersectionObserver` on `.esp-hero__badge` (threshold 0.5)
**Duration:** 1200ms
**Easing:** ease-out cubic

```js
function animateCounter(el, from, to, duration) {
  const startTime = performance.now();
  function update(now) {
    const elapsed = now - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3); // ease-out cubic
    el.textContent = Math.round(from + (to - from) * eased);
    if (progress < 1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}

const badge = document.querySelector('.esp-hero__badge');
if (badge) {
  const io = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        animateCounter(document.getElementById('espBadgeCounter'), 0, 25, 1200);
        io.disconnect();
      }
    });
  }, { threshold: 0.5 });
  io.observe(badge);
}
```

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .esp-hero {
    grid-template-columns: 55fr 45fr;
  }
}
```

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .esp-hero {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  /* Photo below copy on mobile */
  .esp-hero__right {
    height: 55vw;
    min-height: 240px;
  }
  .esp-hero__left {
    padding-block: clamp(80px, 12vw, 120px) clamp(100px, 14vw, 140px);
    /* Extra bottom padding to clear the badge */
  }
  /* Badge repositioned — centered below the two stacked panels */
  .esp-hero__badge {
    bottom: -28px; /* half-overlaps the bottom of the photo */
    left: 50%;
    transform: translateX(-50%);
  }
  .esp-hero__badge-inner {
    padding: 16px 24px;
  }
  .esp-hero__headline {
    font-size: clamp(2.25rem, 7.5vw, 3.25rem);
  }
}
```

---

## Section 2 — Especialistas em Destaque

**Archetype:** Split com Overlap (fotos grandes + bio overlay)
**Constraints:** Hover Reveal (glassmorphism bio overlay) + Floating Cards + Contained Center

---

### HTML Structure

```html
<section class="specialists" aria-label="Especialistas em destaque">
  <div class="specialists__container">

    <header class="specialists__header">
      <h2 class="specialists__title">Especialistas em destaque.</h2>
      <p class="specialists__sub">Conheça alguns dos profissionais por trás do cuidado de excelência da VetPiera.</p>
    </header>

    <div class="specialists__grid">

      <!-- Card 1: Dr. Ryan -->
      <article class="spec-card" aria-label="Dr. Ryan — Neurologista">
        <div class="spec-card__photo" style="background-image: url('/images/dr-ryan.jpg');" role="img" aria-label="Foto do Dr. Ryan"></div>
        <!-- Bio overlay (hover reveals) -->
        <div class="spec-card__overlay">
          <p class="spec-card__role">Neurologia Veterinária</p>
          <h3 class="spec-card__name">Dr. Ryan</h3>
          <p class="spec-card__specialty">CRMV-SP 12345</p>
          <p class="spec-card__bio">Especialista em neurologia e neurocirurgia veterinária com mais de 12 anos de experiência. Referência no diagnóstico e tratamento de epilepsia e doenças do disco intervertebral.</p>
        </div>
        <!-- Info always visible below photo -->
        <div class="spec-card__footer">
          <p class="spec-card__footer-role">Neurologia</p>
          <h3 class="spec-card__footer-name">Dr. Ryan</h3>
        </div>
      </article>

      <!-- Card 2: Dra. Diana -->
      <article class="spec-card" aria-label="Dra. Diana — Fisioterapeuta">
        <div class="spec-card__photo" style="background-image: url('/images/dra-diana.jpg');" role="img" aria-label="Foto da Dra. Diana"></div>
        <div class="spec-card__overlay">
          <p class="spec-card__role">Fisioterapia & Reabilitação</p>
          <h3 class="spec-card__name">Dra. Diana</h3>
          <p class="spec-card__specialty">CRMV-SP 67890</p>
          <p class="spec-card__bio">Pioneira em fisioterapia veterinária no Brasil, com formação em reabilitação aquática, eletroterapia e acupuntura. Transforma a qualidade de vida de animais com limitações motoras.</p>
        </div>
        <div class="spec-card__footer">
          <p class="spec-card__footer-role">Fisioterapia</p>
          <h3 class="spec-card__footer-name">Dra. Diana</h3>
        </div>
      </article>

    </div>

    <div class="specialists__cta-row">
      <a href="/equipe" class="btn btn--outline">Ver toda a equipe →</a>
    </div>

  </div>
</section>
```

---

### Layout CSS

```css
.specialists {
  background: var(--clr-primary-pale);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
}

.specialists__container {
  max-width: 900px;
  margin-inline: auto;
}

/* ── Header ── */
.specialists__header {
  text-align: center;
  margin-bottom: clamp(48px, 6vw, 72px);
}

.specialists__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0 0 16px;
}

.specialists__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  max-width: 460px;
  margin-inline: auto;
}

/* ── Grid ── */
.specialists__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: clamp(20px, 3vw, 32px);
}

/* ── Card ── */
.spec-card {
  border-radius: var(--radius-lg);
  overflow: hidden;
  position: relative;
  cursor: pointer;
  background: var(--clr-surface);
  /* Subtle entrance shadow */
  box-shadow: 0 2px 12px rgba(15,45,36,0.06);
  transition: box-shadow 400ms ease, transform 400ms var(--ease-out-expo);
}

.spec-card:hover {
  box-shadow: 0 16px 48px rgba(15,45,36,0.15);
  transform: translateY(-4px);
}

/* ── Photo ── */
.spec-card__photo {
  height: 380px;
  background-size: cover;
  background-position: center top;
  background-color: #1a3a2e; /* fallback */
  position: relative;
}

/* ── Bio overlay ── */
.spec-card__overlay {
  position: absolute;
  /* Covers the photo area only — top: 0 to footer top */
  top: 0;
  left: 0;
  right: 0;
  height: 380px; /* matches photo height */
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  background: linear-gradient(
    to top,
    rgba(15, 45, 36, 0.88) 0%,
    rgba(15, 45, 36, 0.60) 30%,
    rgba(15, 45, 36, 0) 55%
  );
  padding: clamp(24px, 3vw, 36px);

  /* Initial: hidden */
  opacity: 0;
  transition: opacity 400ms ease;
}

.spec-card:hover .spec-card__overlay {
  opacity: 1;
}

/* ── Overlay content ── */
.spec-card__role {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-accent);
  margin: 0 0 6px;
}

.spec-card__name {
  font-family: var(--font-display);
  font-size: 1.4rem;
  line-height: 1.2;
  color: #FFFFFF;
  margin: 0 0 4px;
}

.spec-card__specialty {
  font-family: var(--font-body);
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--clr-primary-pale);
  margin: 0 0 12px;
}

.spec-card__bio {
  font-family: var(--font-body);
  font-size: 0.875rem;
  line-height: 1.55;
  color: rgba(255,255,255,0.75);
  margin: 0;
  /* Clip to 4 lines */
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* ── Footer (always visible) ── */
.spec-card__footer {
  padding: 20px clamp(20px, 2.5vw, 28px) 24px;
  background: var(--clr-surface);
}

.spec-card__footer-role {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-muted);
  margin: 0 0 4px;
}

.spec-card__footer-name {
  font-family: var(--font-display);
  font-size: 1.2rem;
  color: var(--clr-text);
  margin: 0;
}

/* ── CTA row ── */
.specialists__cta-row {
  display: flex;
  justify-content: center;
  margin-top: clamp(40px, 5vw, 60px);
}
```

---

### Mobile: Bio always visible

```css
@media (max-width: 768px) {
  /* On mobile, overlay is always visible at 60% opacity */
  .spec-card__overlay {
    opacity: 0.85;
    /* Bio slightly truncated on mobile to fit */
    background: linear-gradient(
      to top,
      rgba(15, 45, 36, 0.92) 0%,
      rgba(15, 45, 36, 0.40) 60%,
      rgba(15, 45, 36, 0) 100%
    );
  }
  /* Disable hover effect (bio always visible) */
  .spec-card:hover .spec-card__overlay {
    opacity: 0.85;
  }
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .specialists__grid {
    grid-template-columns: 1fr;
  }
  .spec-card__photo,
  .spec-card__overlay {
    height: 320px;
  }
  .spec-card:hover {
    transform: none; /* disable lift on touch */
  }
}
```

---

## Section 3 — Grid de Especialidades

**Archetype:** Broken Grid / Editorial
**Constraints:** Mixed Weights (números enormes vs. nomes pequenos) + Overflow Visible + Hover Color

---

### HTML Structure

```html
<section class="esp-grid" id="especialidades-lista" aria-label="Lista de especialidades veterinárias">
  <div class="esp-grid__container">

    <header class="esp-grid__header">
      <h2 class="esp-grid__title">Todas as nossas<br>especialidades.</h2>
      <p class="esp-grid__sub">Cada especialidade conta com profissionais certificados, protocolos atualizados e tecnologia diagnóstica própria.</p>
    </header>

    <!-- Featured 5 — vertical editorial list -->
    <div class="esp-grid__featured" aria-label="Especialidades em destaque">

      <div class="esp-grid__item" style="--item-num: '1'">
        <span class="esp-grid__num" aria-hidden="true">1</span>
        <h3 class="esp-grid__name">Neurologia</h3>
        <i class="ph ph-brain esp-grid__icon" aria-hidden="true"></i>
      </div>

      <div class="esp-grid__item" style="--item-num: '2'">
        <span class="esp-grid__num" aria-hidden="true">2</span>
        <h3 class="esp-grid__name">Ortopedia</h3>
        <i class="ph ph-bone esp-grid__icon" aria-hidden="true"></i>
      </div>

      <div class="esp-grid__item" style="--item-num: '3'">
        <span class="esp-grid__num" aria-hidden="true">3</span>
        <h3 class="esp-grid__name">Fisioterapia</h3>
        <i class="ph ph-activity esp-grid__icon" aria-hidden="true"></i>
      </div>

      <div class="esp-grid__item" style="--item-num: '4'">
        <span class="esp-grid__num" aria-hidden="true">4</span>
        <h3 class="esp-grid__name">Cardiologia</h3>
        <i class="ph ph-heartbeat esp-grid__icon" aria-hidden="true"></i>
      </div>

      <div class="esp-grid__item" style="--item-num: '5'">
        <span class="esp-grid__num" aria-hidden="true">5</span>
        <h3 class="esp-grid__name">Oncologia</h3>
        <i class="ph ph-drop esp-grid__icon" aria-hidden="true"></i>
      </div>

    </div>

    <!-- All other specialties — tag grid -->
    <div class="esp-grid__other" aria-label="Outras especialidades">
      <p class="esp-grid__other-label">E mais 20 especialidades:</p>
      <div class="esp-grid__tags">
        <span class="esp-grid__tag">Oftalmologia</span>
        <span class="esp-grid__tag">Odontologia</span>
        <span class="esp-grid__tag">Endocrinologia</span>
        <span class="esp-grid__tag">Dermatologia</span>
        <span class="esp-grid__tag">Medicina Felina</span>
        <span class="esp-grid__tag">Neonatologia</span>
        <span class="esp-grid__tag">Anestesiologia</span>
        <span class="esp-grid__tag">Diagnóstico por Imagem</span>
        <span class="esp-grid__tag">Reabilitação</span>
        <span class="esp-grid__tag">Comportamento Animal</span>
        <span class="esp-grid__tag">Nutrição Clínica</span>
        <span class="esp-grid__tag">Clínica Geral</span>
        <span class="esp-grid__tag">Acupuntura</span>
        <span class="esp-grid__tag">Imunologia</span>
        <span class="esp-grid__tag">Cirurgia Geral</span>
        <span class="esp-grid__tag">Cirurgia Laparoscópica</span>
        <span class="esp-grid__tag">Hemoterapia</span>
        <span class="esp-grid__tag">Terapia Intensiva</span>
        <span class="esp-grid__tag">Gastroenterologia</span>
        <span class="esp-grid__tag">Nefrologia</span>
      </div>
    </div>

  </div>
</section>
```

---

### Layout CSS

```css
.esp-grid {
  background: var(--clr-bg);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
}

.esp-grid__container {
  max-width: var(--container);
  margin-inline: auto;
}

/* ── Header ── */
.esp-grid__header {
  text-align: center;
  margin-bottom: clamp(56px, 7vw, 88px);
}

.esp-grid__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0 0 16px;
}

.esp-grid__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  max-width: 520px;
  margin-inline: auto;
}

/* ── Featured list ── */
.esp-grid__featured {
  max-width: 860px;
  margin-inline: auto;
  margin-bottom: clamp(56px, 7vw, 80px);
}

/* ── Individual featured item ── */
.esp-grid__item {
  display: grid;
  grid-template-columns: 80px 1fr auto;
  align-items: center;
  gap: 32px;
  padding-block: 28px;
  padding-inline: 0;
  border-bottom: 1px solid var(--clr-border);
  cursor: pointer;
  position: relative;
  border-radius: 0;

  /* Transition for hover color change */
  transition:
    background 350ms ease,
    border-radius 350ms ease,
    padding 350ms ease;
}

.esp-grid__item:first-child {
  border-top: 1px solid var(--clr-border);
}

/* Hover: fill with primary green */
.esp-grid__item:hover {
  background: var(--clr-primary);
  border-radius: var(--radius);
  padding-inline: 20px;
  /* Remove border visual during hover (handled via box-shadow) */
  border-color: transparent;
}

/* Prevent border collision on hover */
.esp-grid__item:hover + .esp-grid__item {
  border-top-color: transparent;
}

/* ── Number (giant Mixed Weight) ── */
.esp-grid__num {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  line-height: 1;
  color: var(--clr-primary);
  opacity: 0.25;
  transition: color 350ms ease, opacity 350ms ease;
  display: block;
  text-align: right;
}

.esp-grid__item:hover .esp-grid__num {
  color: rgba(255,255,255,0.15);
  opacity: 1;
}

/* ── Name (smaller, contrasting weight) ── */
.esp-grid__name {
  font-family: var(--font-display);
  font-size: clamp(1.4rem, 2.5vw, 2rem);
  line-height: 1.2;
  color: var(--clr-text);
  margin: 0;
  transition: color 350ms ease;
}

.esp-grid__item:hover .esp-grid__name {
  color: #FFFFFF;
}

/* ── Icon ── */
.esp-grid__icon {
  font-size: 1.5rem;
  color: var(--clr-accent);
  flex-shrink: 0;
  transition: color 350ms ease;
}

.esp-grid__item:hover .esp-grid__icon {
  color: var(--clr-accent); /* stays gold on hover */
}

/* ── Tag grid (other specialties) ── */
.esp-grid__other {
  max-width: 860px;
  margin-inline: auto;
}

.esp-grid__other-label {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-muted);
  margin-bottom: 20px;
}

.esp-grid__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.esp-grid__tag {
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 500;
  color: var(--clr-text);
  background: var(--clr-surface);
  border: 1px solid var(--clr-border);
  border-radius: 100px;
  padding: 8px 18px;
  cursor: default;
  transition:
    border-color 250ms ease,
    border-left-width 250ms ease,
    padding-left 250ms ease,
    color 250ms ease;
}

.esp-grid__tag:hover {
  /* Sophisticated hover: border-left accent instead of background fill */
  border-left: 3px solid var(--clr-accent);
  padding-left: 14px; /* compensate for wider border */
  color: var(--clr-primary);
  border-color: var(--clr-border);
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .esp-grid__item {
    grid-template-columns: 60px 1fr auto;
    gap: 16px;
    padding-block: 22px;
  }
  .esp-grid__num {
    font-size: clamp(2rem, 8vw, 3rem);
  }
  .esp-grid__name {
    font-size: clamp(1.2rem, 4.5vw, 1.6rem);
  }
  /* Disable hover color change on touch */
  .esp-grid__item:hover {
    background: transparent;
    padding-inline: 0;
    border-radius: 0;
  }
  .esp-grid__item:hover .esp-grid__name {
    color: var(--clr-text);
  }
  .esp-grid__item:hover .esp-grid__num {
    color: var(--clr-primary);
    opacity: 0.25;
  }
}
```

---

## Section 4 — Processo ("Como Funciona")

**Archetype:** Poster com números gigantes
**Constraints:** Headline outline gigante (1, 2, 3) + Clip Reveal + View Timeline + Stagger

---

### HTML Structure

```html
<section class="process" aria-label="Como funciona o atendimento">
  <div class="process__container">

    <header class="process__header">
      <h2 class="process__title">Como é o seu<br>atendimento.</h2>
      <p class="process__sub">Simples, transparente e centrado no bem-estar do seu animal.</p>
    </header>

    <div class="process__grid">

      <div class="process__step" style="--i: 0">
        <span class="process__big-num" aria-hidden="true">1</span>
        <div class="process__step-content">
          <span class="process__step-line" aria-hidden="true"></span>
          <h3 class="process__step-title">Agende sua consulta</h3>
          <p class="process__step-text">Por WhatsApp, telefone ou diretamente em nosso site — escolha o especialista e o horário que melhor se encaixa na sua rotina.</p>
        </div>
      </div>

      <div class="process__step" style="--i: 1">
        <span class="process__big-num" aria-hidden="true">2</span>
        <div class="process__step-content">
          <span class="process__step-line" aria-hidden="true"></span>
          <h3 class="process__step-title">Venha à consulta</h3>
          <p class="process__step-text">Traga o histórico médico do seu animal. Nosso especialista fará uma avaliação completa e solicitará os exames necessários.</p>
        </div>
      </div>

      <div class="process__step" style="--i: 2">
        <span class="process__big-num" aria-hidden="true">3</span>
        <div class="process__step-content">
          <span class="process__step-line" aria-hidden="true"></span>
          <h3 class="process__step-title">Receba o diagnóstico</h3>
          <p class="process__step-text">Com laudo detalhado e plano de tratamento personalizado, você sai com clareza total sobre a saúde do seu pet e os próximos passos.</p>
        </div>
      </div>

    </div>

  </div>
</section>
```

---

### Layout CSS

```css
.process {
  background: var(--clr-primary-pale);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
}

.process__container {
  max-width: var(--container);
  margin-inline: auto;
}

/* ── Header ── */
.process__header {
  text-align: center;
  margin-bottom: clamp(64px, 8vw, 96px);
}

.process__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0 0 16px;
}

.process__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  max-width: 420px;
  margin-inline: auto;
}

/* ── Steps grid ── */
.process__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: clamp(24px, 4vw, 48px);
}

/* ── Individual step ── */
.process__step {
  position: relative;
  padding-top: clamp(60px, 8vw, 100px);

  /* View Timeline animation with stagger */
  animation: fadeUpClip 650ms ease-out both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
  animation-delay: calc(var(--i, 0) * 150ms);
}

/* ── Giant background number ── */
.process__big-num {
  position: absolute;
  top: 0;
  left: 0;
  font-family: var(--font-display);
  font-size: clamp(6rem, 14vw, 10rem);
  line-height: 1;
  color: transparent;
  -webkit-text-stroke: 1.5px rgba(27,77,62,0.10);
  text-stroke: 1.5px rgba(27,77,62,0.10);
  user-select: none;
  pointer-events: none;
  z-index: 0;
  letter-spacing: -0.04em;
}

/* ── Step content (z-index above number) ── */
.process__step-content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

/* Gold accent line */
.process__step-line {
  display: block;
  width: 40px;
  height: 2px;
  background: var(--clr-accent);
  border-radius: 1px;
  flex-shrink: 0;
}

.process__step-title {
  font-family: var(--font-display);
  font-size: 1.3rem;
  line-height: 1.25;
  color: var(--clr-text);
  letter-spacing: -0.01em;
  margin: 0;
}

.process__step-text {
  font-family: var(--font-body);
  font-size: 0.9rem;
  line-height: 1.7;
  color: var(--clr-muted);
  margin: 0;
}

/* ── Keyframes ── */
@keyframes fadeUpClip {
  from {
    opacity: 0;
    clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0 100%);
  }
  to {
    opacity: 1;
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  }
}
```

---

### Fallback JS (no animation-timeline support)

```js
const supportsTimeline = CSS.supports('animation-timeline', 'view()');
if (!supportsTimeline) {
  const steps = document.querySelectorAll('.process__step');
  const io = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        const delay = (parseInt(e.target.style.getPropertyValue('--i') || 0)) * 150;
        setTimeout(() => {
          e.target.style.cssText += '; animation: fadeUpClip 650ms ease-out both;';
          io.unobserve(e.target);
        }, delay);
      }
    });
  }, { threshold: 0.2 });
  steps.forEach(step => {
    step.style.opacity = '0';
    step.style.clipPath = 'polygon(0 100%, 100% 100%, 100% 100%, 0 100%)';
    io.observe(step);
  });
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .process__grid {
    grid-template-columns: 1fr;
    gap: clamp(48px, 8vw, 64px);
  }

  .process__step {
    padding-top: clamp(50px, 12vw, 80px);
  }

  .process__big-num {
    font-size: clamp(5rem, 18vw, 8rem);
  }
}
```

---

## Section 5 — Contato ("Agende agora")

**Archetype:** Split Assimétrico (45/55)
**Constraints:** Dark Mode + Floating Cards (glassmorphism) + Imagem Fullbleed (map placeholder)

---

### HTML Structure

```html
<section class="esp-contact" id="contato" aria-label="Agende sua consulta">
  <div class="esp-contact__grid">

    <!-- Left: copy + info (45%) -->
    <div class="esp-contact__left">
      <span class="esp-contact__eyebrow">Pronto para agendar?</span>
      <h2 class="esp-contact__title">Agende agora.</h2>
      <p class="esp-contact__sub">Nossa equipe de atendimento está disponível para ajudar você a encontrar o especialista certo para o seu animal.</p>

      <div class="esp-contact__info-list">

        <div class="esp-contact__info-item">
          <i class="ph ph-map-pin" aria-hidden="true"></i>
          <div>
            <p class="esp-contact__info-label">Endereço</p>
            <p class="esp-contact__info-value">Rua Itapeti, 154 — São Paulo, SP</p>
          </div>
        </div>

        <div class="esp-contact__info-item">
          <i class="ph ph-clock" aria-hidden="true"></i>
          <div>
            <p class="esp-contact__info-label">Horário</p>
            <p class="esp-contact__info-value">Seg–Sex: 9h–18h &nbsp;·&nbsp; Sáb: 9h–13h</p>
          </div>
        </div>

        <div class="esp-contact__info-item">
          <i class="ph ph-phone" aria-hidden="true"></i>
          <div>
            <p class="esp-contact__info-label">Telefone</p>
            <p class="esp-contact__info-value">
              <a href="tel:+551123733144" class="esp-contact__tel">(11) 2373-3144</a>
            </p>
          </div>
        </div>

        <div class="esp-contact__info-item">
          <i class="ph ph-envelope" aria-hidden="true"></i>
          <div>
            <p class="esp-contact__info-label">E-mail</p>
            <p class="esp-contact__info-value">
              <a href="mailto:especialidades@vetpiera.com.br" class="esp-contact__tel">especialidades@vetpiera.com.br</a>
            </p>
          </div>
        </div>

      </div>

      <div class="esp-contact__actions">
        <a href="/especialidades#contato-form" class="btn btn--accent esp-contact__cta">
          Agendar uma consulta →
        </a>
        <a href="https://wa.me/5511991334520" class="btn btn--ghost" target="_blank" rel="noopener">
          <i class="ph ph-whatsapp-logo" aria-hidden="true"></i> WhatsApp
        </a>
      </div>
    </div>

    <!-- Right: map placeholder (55%) -->
    <div class="esp-contact__right" aria-label="Mapa de localização">
      <div class="esp-contact__map" aria-hidden="true">
        <!-- Replace with real Google Maps embed iframe:
             <iframe
               src="https://www.google.com/maps/embed?..."
               style="width:100%;height:100%;border:0;"
               allowfullscreen=""
               loading="lazy"
               referrerpolicy="no-referrer-when-downgrade"
               title="Localização da VetPiera"
             ></iframe>
        -->
        <div class="esp-contact__map-placeholder" aria-hidden="true">
          <i class="ph ph-map-trifold"></i>
          <span>Rua Itapeti, 154</span>
        </div>
      </div>

      <!-- Floating glassmorphism card -->
      <div class="esp-contact__glass-card">
        <div class="esp-contact__glass-hours">
          <i class="ph ph-clock" aria-hidden="true"></i>
          <div>
            <p class="esp-contact__glass-label">Horário de atendimento</p>
            <p class="esp-contact__glass-value">Seg–Sex: 9h–18h</p>
            <p class="esp-contact__glass-value">Sáb: 9h–13h</p>
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
.esp-contact {
  background: var(--clr-dark);
  overflow: hidden;
}

.esp-contact__grid {
  display: grid;
  grid-template-columns: 45fr 55fr;
  min-height: 620px;
}

/* ── Left panel ── */
.esp-contact__left {
  padding: clamp(64px, 8vw, 96px) var(--pad-x) clamp(64px, 8vw, 96px)
    clamp(24px, calc((100vw - var(--container)) / 2 + var(--pad-x)), 128px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: clamp(16px, 2vw, 24px);
}

.esp-contact__eyebrow {
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
}

.esp-contact__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.05;
  color: #FFFFFF;
  letter-spacing: -0.02em;
  margin: 0;
}

.esp-contact__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: rgba(255,255,255,0.60);
  line-height: 1.65;
  max-width: 380px;
  margin: 0;
}

/* Info list */
.esp-contact__info-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-block: clamp(16px, 2vw, 24px);
}

.esp-contact__info-item {
  display: flex;
  align-items: flex-start;
  gap: 16px;
}

.esp-contact__info-item > i {
  font-size: 1.25rem;
  color: var(--clr-accent);
  flex-shrink: 0;
  margin-top: 2px;
}

.esp-contact__info-label {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.35);
  margin: 0 0 4px;
}

.esp-contact__info-value {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  color: rgba(255,255,255,0.85);
  margin: 0;
  line-height: 1.5;
}

.esp-contact__tel {
  color: rgba(255,255,255,0.85);
  text-decoration: none;
  transition: color 200ms ease;
}
.esp-contact__tel:hover {
  color: var(--clr-accent);
}

/* CTAs row */
.esp-contact__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin-top: 8px;
}

.esp-contact__cta:hover {
  box-shadow: 0 8px 32px rgba(201,168,76,0.35);
}

/* ── Right panel ── */
.esp-contact__right {
  position: relative;
  background: rgba(255,255,255,0.04);
  border-left: 1px solid rgba(255,255,255,0.08);
}

.esp-contact__map {
  width: 100%;
  height: 100%;
  min-height: 400px;
}

.esp-contact__map-placeholder {
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

.esp-contact__map-placeholder i {
  font-size: 2.5rem;
}

/* ── Floating glass card ── */
.esp-contact__glass-card {
  position: absolute;
  bottom: 32px;
  left: 24px;
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px) saturate(1.5);
  -webkit-backdrop-filter: blur(20px) saturate(1.5);
  border: 1px solid rgba(255,255,255,0.14);
  border-radius: var(--radius);
  padding: 18px 20px;
}

.esp-contact__glass-hours {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

.esp-contact__glass-hours i {
  font-size: 1.125rem;
  color: var(--clr-accent);
  flex-shrink: 0;
  margin-top: 2px;
}

.esp-contact__glass-label {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: rgba(255,255,255,0.40);
  margin: 0 0 6px;
}

.esp-contact__glass-value {
  font-family: var(--font-body);
  font-size: 0.875rem;
  font-weight: 500;
  color: rgba(255,255,255,0.85);
  margin: 0;
  line-height: 1.5;
}
```

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .esp-contact__grid {
    grid-template-columns: 1fr 1fr;
  }
  .esp-contact__left {
    padding-left: var(--pad-x);
  }
}
```

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .esp-contact__grid {
    grid-template-columns: 1fr;
  }
  /* Map first on mobile */
  .esp-contact__right {
    order: -1;
    border-left: none;
    border-bottom: 1px solid rgba(255,255,255,0.08);
  }
  .esp-contact__map,
  .esp-contact__map-placeholder {
    min-height: auto;
    aspect-ratio: 16 / 9;
  }
  .esp-contact__left {
    padding-block: clamp(48px, 8vw, 72px);
  }
  .esp-contact__sub {
    max-width: 100%;
  }
  .esp-contact__actions {
    flex-direction: column;
    align-items: flex-start;
  }
  .esp-contact__glass-card {
    bottom: auto;
    top: 16px;
    left: 16px;
    right: auto;
  }
}
```

---

## Global Accessibility Notes (Especialidades-specific)

- Badge counter: for screen readers, set `aria-live="polite"` on `#espBadgeCounter` so the number is announced when animation ends
- Specialist cards: `aria-label` on `<article>` describes the doctor and specialty
- `.esp-grid__featured` items: add `role="button"` and `tabindex="0"` if they link somewhere; otherwise leave as presentational
- All icons with `aria-hidden="true"` — text labels always accompany them
- `prefers-reduced-motion`:

```css
@media (prefers-reduced-motion: reduce) {
  .esp-hero__eyebrow,
  .esp-hero__headline,
  .esp-hero__sub,
  .esp-hero__actions {
    animation: none;
    opacity: 1;
    transform: none;
  }

  .process__step {
    animation: none;
    opacity: 1;
    clip-path: none;
  }

  .spec-card__overlay {
    /* On reduced motion, bio overlay is always visible at 50% */
    opacity: 0.6;
    transition: none;
  }

  .esp-grid__item {
    transition: none;
  }
}
```

---

## Complete Scroll Animation Reference

All View Timeline animations on this page require this `@supports` wrapper or the JS fallback:

```css
@supports (animation-timeline: view()) {
  .process__step {
    animation: fadeUpClip 650ms ease-out both;
    animation-timeline: view();
    animation-range: entry 0% entry 40%;
    animation-delay: calc(var(--i, 0) * 150ms);
  }
}

/* Without @supports, elements are visible by default */
.process__step {
  opacity: 1;
  clip-path: none;
}
```

---

## Asset Requirements

| Asset | Dimensions | Format | Notes |
|---|---|---|---|
| `/images/especialidades-hero.jpg` | 960×1200px | JPG | Specialist examining animal, warm clinical light |
| `/images/dr-ryan.jpg` | 600×760px | JPG | Headshot/portrait, professional, center-top composition |
| `/images/dra-diana.jpg` | 600×760px | JPG | Headshot/portrait, professional, center-top composition |
| Phosphor Icons | CDN | SVG font | All `ph-` classes used above |
| DM Serif Display | Google Fonts | Woff2 | weight: 400 only |
| DM Sans | Google Fonts | Woff2 | weights: 400, 500, 600 |

---

## Inter-Page Navigation Notes

- Hero CTA "Agendar uma consulta →" → `href="#contato"` (same page anchor)
- Hero CTA "Ver especialidades" → `href="#especialidades-lista"` (same page anchor)
- Specialists CTA "Ver toda a equipe →" → `href="/equipe"` (future page)
- Contact CTAs → WhatsApp opens in new tab with `rel="noopener noreferrer"`
- All `<a>` with `target="_blank"` must include `rel="noopener noreferrer"`
