# VetPiera — Home Page Layout Specification

**File:** `home/layout.md`
**Last updated:** 2026-03-13
**Designer:** Art Director (Claude)
**Status:** Ready for development

---

## Global Tokens (apply to all pages)

```css
:root {
  /* Colors */
  --clr-primary:       #1B4D3E;
  --clr-accent:        #C9A84C;
  --clr-dark:          #0F2D24;
  --clr-bg:            #FAFAF8;
  --clr-primary-pale:  #E8F2ED;
  --clr-surface:       #FFFFFF;
  --clr-border:        #E2E8E5;
  --clr-text:          #1A1A1A;
  --clr-muted:         #5C6B74;

  /* Typography */
  --font-display: 'DM Serif Display', Georgia, serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
  --fs-hero:  clamp(2.75rem, 5.5vw, 4.5rem);
  --fs-h2:    clamp(2rem, 4vw, 3rem);
  --fs-h3:    clamp(1.4rem, 2.5vw, 1.9rem);
  --fs-body:  clamp(1rem, 1.5vw, 1.1rem);
  --fs-sm:    0.875rem;

  /* Spacing */
  --sp-section: clamp(80px, 10vw, 128px);
  --sp-inner:   clamp(40px, 5vw, 64px);
  --container:  1200px;
  --pad-x:      clamp(24px, 5vw, 64px);

  /* Shape */
  --radius:    12px;
  --radius-lg: 20px;

  /* Easing */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
}
```

---

## Section 1 — Hero

**Archetype:** Split Assimétrico (55/45) com diagonal edge
**Constraints:** Split Diagonal + Mouse Parallax + Clip Reveal (word-by-word) + Counter Animation

---

### HTML Structure

```html
<section class="hero" aria-label="Hero principal">
  <div class="hero__copy"> <!-- 55% left -->
    <span class="hero__eyebrow">Clínica Veterinária de Referência</span>
    <h1 class="hero__headline">
      <span class="hero__word">O</span>
      <span class="hero__word">cuidado</span>
      <span class="hero__word">veterinário</span>
      <span class="hero__word">completo</span>
      <span class="hero__word">que</span>
      <span class="hero__word">o</span>
      <span class="hero__word">seu</span>
      <span class="hero__word">pet</span>
      <span class="hero__word">merece.</span>
    </h1>
    <p class="hero__sub">Atendimento humano, tecnologia de ponta e mais de 22 anos de experiência cuidando de quem você ama.</p>
    <div class="hero__actions">
      <a href="/hospital" class="btn btn--accent">Hospital 24h →</a>
      <a href="/especialidades" class="btn btn--outline">Conhecer Especialidades</a>
    </div>
  </div>
  <div class="hero__media" aria-hidden="true"> <!-- 45% right -->
    <div class="hero__photo" id="heroPhoto"></div>
    <div class="hero__vignette"></div>
  </div>
  <div class="hero__badge" aria-label="22 anos de experiência">
    <span class="hero__badge-num" id="heroBadgeCounter">0</span>
    <span class="hero__badge-label">anos de<br>experiência</span>
  </div>
</section>
```

---

### Layout CSS

```css
.hero {
  display: grid;
  grid-template-columns: 55fr 45fr;
  min-height: 100svh;
  position: relative;
  overflow: hidden;
  background: var(--clr-bg);
}

/* ── Left panel ── */
.hero__copy {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-block: clamp(100px, 14vw, 160px);
  padding-inline: var(--pad-x);
  padding-right: clamp(40px, 6vw, 80px);
  background: var(--clr-bg);
}

/* Diagonal edge cutting into the right side */
.hero__copy::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--clr-bg);
  clip-path: polygon(0 0, 48% 0, 100% 100%, 0 100%);
  right: -80px;
  z-index: -1;
  pointer-events: none;
}

/* ── Right panel (media) ── */
.hero__media {
  position: relative;
  overflow: hidden;
}

.hero__photo {
  width: 100%;
  height: 100%;
  background-image: url('/images/hero-placeholder.jpg');
  background-size: cover;
  background-position: 50% 50%;
  /* JS updates this via --mx/--my */
  transition: background-position 0.1s linear;
  will-change: background-position;
}

/* Vignette overlay on photo */
.hero__vignette {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse 80% 80% at 100% 50%, transparent 50%, rgba(15,45,36,0.55) 100%),
    linear-gradient(to right, rgba(250,250,248,0.6) 0%, transparent 30%);
  pointer-events: none;
}

/* ── Badge ── */
.hero__badge {
  position: absolute;
  /* sits on the diagonal seam, vertically centered-ish */
  top: 50%;
  left: calc(55% - 60px);
  transform: translate(-50%, -50%);
  z-index: 10;
  display: flex;
  align-items: baseline;
  gap: 10px;
  pointer-events: none;
}

.hero__badge-num {
  font-family: var(--font-display);
  font-size: clamp(5rem, 12vw, 9rem);
  line-height: 1;
  color: var(--clr-primary);
  opacity: 0.12;
  letter-spacing: -0.03em;
  /* opacity increases after counter ends (JS adds class) */
  transition: opacity 400ms ease;
}

.hero__badge-num.is-done {
  opacity: 0.18;
}

.hero__badge-label {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--clr-muted);
  line-height: 1.4;
}
```

---

### Typography CSS

```css
/* Eyebrow */
.hero__eyebrow {
  display: inline-block;
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
  margin-bottom: clamp(16px, 2.5vw, 24px);
}

/* Headline */
.hero__headline {
  font-family: var(--font-display);
  font-size: var(--fs-hero);
  line-height: 1.08;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0 0 clamp(20px, 3vw, 32px);
  display: flex;
  flex-wrap: wrap;
  gap: 0.25em;
}

/* Each word wrapped for clip-path reveal */
.hero__word {
  display: inline-block;
  clip-path: polygon(0 0, 100% 0, 100% 0, 0 0);
  /* JS removes this initial state and applies the final state */
}

.hero__word.is-revealed {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  transition: clip-path 600ms var(--ease-out-expo);
}

/* Sub */
.hero__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  color: var(--clr-muted);
  line-height: 1.65;
  max-width: 420px;
  margin-bottom: clamp(32px, 4vw, 48px);
  opacity: 0;
  transform: translateY(16px);
}

.hero__sub.is-visible {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 650ms var(--ease-out-expo) 800ms,
              transform 650ms var(--ease-out-expo) 800ms;
}

/* CTAs row */
.hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  opacity: 0;
  transform: translateY(16px);
}

.hero__actions.is-visible {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 600ms var(--ease-out-expo) 1000ms,
              transform 600ms var(--ease-out-expo) 1000ms;
}
```

---

### Button Base Styles (Global)

```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-family: var(--font-body);
  font-size: 0.9375rem;
  font-weight: 600;
  line-height: 1;
  padding: 14px 28px;
  border-radius: 8px;
  border: 2px solid transparent;
  cursor: pointer;
  text-decoration: none;
  transition:
    background-color 280ms ease,
    box-shadow 280ms ease,
    transform 200ms ease,
    border-color 280ms ease,
    color 280ms ease;
}

.btn--accent {
  background: var(--clr-accent);
  color: #FFFFFF;
  border-color: var(--clr-accent);
}
.btn--accent:hover {
  background: #b8922e;
  border-color: #b8922e;
  box-shadow: 0 6px 24px rgba(201,168,76,0.32);
  transform: translateY(-2px);
}

.btn--outline {
  background: transparent;
  color: var(--clr-text);
  border-color: var(--clr-text);
}
.btn--outline:hover {
  background: var(--clr-text);
  color: #FFFFFF;
  transform: translateY(-2px);
}

.btn--primary {
  background: var(--clr-primary);
  color: #FFFFFF;
  border-color: var(--clr-primary);
}
.btn--primary:hover {
  background: var(--clr-dark);
  border-color: var(--clr-dark);
  box-shadow: 0 6px 24px rgba(27,77,62,0.30);
  transform: translateY(-2px);
}

.btn--ghost {
  background: rgba(255,255,255,0.1);
  color: #FFFFFF;
  border-color: rgba(255,255,255,0.35);
  backdrop-filter: blur(8px);
}
.btn--ghost:hover {
  background: rgba(255,255,255,0.18);
  border-color: rgba(255,255,255,0.6);
}
```

---

### Animation Specs

#### Word-by-word Clip Reveal (JS-driven)

**Trigger:** `DOMContentLoaded` — starts immediately on page load (eyebrow fades first, then words)

```js
// Eyebrow fades up first
document.querySelector('.hero__eyebrow').style.cssText =
  'opacity:0; transform:translateY(12px); transition: opacity 550ms cubic-bezier(0.16,1,0.3,1) 100ms, transform 550ms cubic-bezier(0.16,1,0.3,1) 100ms';
requestAnimationFrame(() => {
  document.querySelector('.hero__eyebrow').style.cssText =
    'opacity:1; transform:translateY(0); transition: opacity 550ms cubic-bezier(0.16,1,0.3,1) 100ms, transform 550ms cubic-bezier(0.16,1,0.3,1) 100ms';
});

// Words reveal sequentially
const words = document.querySelectorAll('.hero__word');
words.forEach((word, i) => {
  setTimeout(() => word.classList.add('is-revealed'), 300 + i * 80);
});

// Sub and actions appear after words
setTimeout(() => {
  document.querySelector('.hero__sub').classList.add('is-visible');
  document.querySelector('.hero__actions').classList.add('is-visible');
}, 300 + words.length * 80 + 100);
```

- Each word: `clip-path` transition `600ms cubic-bezier(0.16,1,0.3,1)`
- Stagger: `80ms` between words
- First word delay: `300ms` after page load
- Sub appears: after last word + 100ms extra delay

#### Counter Animation — Badge "22"

**Trigger:** `IntersectionObserver` on `.hero__badge` (threshold 0.5)
**Duration:** 1400ms
**Easing:** ease-out (approximated with cubic-bezier steps)

```js
function animateCounter(el, from, to, duration) {
  const startTime = performance.now();
  function update(now) {
    const elapsed = now - startTime;
    const progress = Math.min(elapsed / duration, 1);
    // ease-out quad
    const eased = 1 - Math.pow(1 - progress, 2);
    el.textContent = Math.round(from + (to - from) * eased);
    if (progress < 1) requestAnimationFrame(update);
    else el.closest('.hero__badge-num').classList.add('is-done');
  }
  requestAnimationFrame(update);
}

const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      animateCounter(document.getElementById('heroBadgeCounter'), 0, 22, 1400);
      observer.disconnect();
    }
  });
}, { threshold: 0.5 });
observer.observe(document.querySelector('.hero__badge'));
```

#### Mouse Parallax — Hero Photo

**Trigger:** `mousemove` on `.hero` element

```js
const hero = document.querySelector('.hero');
const photo = document.getElementById('heroPhoto');
const STRENGTH = 0.015;

hero.addEventListener('mousemove', e => {
  const rect = hero.getBoundingClientRect();
  const cx = rect.width / 2;
  const cy = rect.height / 2;
  const dx = (e.clientX - rect.left - cx) * STRENGTH;
  const dy = (e.clientY - rect.top - cy) * STRENGTH;
  photo.style.backgroundPosition = `calc(50% + ${dx}px) calc(50% + ${dy}px)`;
});

hero.addEventListener('mouseleave', () => {
  photo.style.backgroundPosition = '50% 50%';
  // smooth reset
  photo.style.transition = 'background-position 800ms cubic-bezier(0.16,1,0.3,1)';
  setTimeout(() => { photo.style.transition = ''; }, 800);
});
```

- Movement range: ±20px (achieved with STRENGTH 0.015 at standard viewport)
- Reset transition: `800ms cubic-bezier(0.16,1,0.3,1)` on mouse leave

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .hero {
    grid-template-columns: 58fr 42fr;
  }
  .hero__badge {
    left: calc(58% - 40px);
  }
}
```

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .hero {
    grid-template-columns: 1fr;
    grid-template-rows: auto 55vw;
    min-height: auto;
  }
  .hero__copy {
    padding-block: clamp(80px, 12vw, 120px) clamp(40px, 6vw, 64px);
    padding-inline: var(--pad-x);
  }
  .hero__copy::after {
    display: none; /* diagonal only on desktop */
  }
  .hero__media {
    order: -1; /* photo on top */
    height: 55vw;
    min-height: 240px;
  }
  .hero__badge {
    position: relative;
    top: auto;
    left: auto;
    transform: none;
    margin-top: 24px;
  }
  .hero__badge-num {
    font-size: clamp(4rem, 18vw, 7rem);
  }
  /* Disable mouse parallax on touch devices (JS checks 'ontouchstart') */
}
```

---

## Section 2 — Units ("Duas Unidades")

**Archetype:** Bento Box com dois cards grandes
**Constraints:** Color Blocking + Hover Flip 3D + Grain Overlay

---

### HTML Structure

```html
<section class="units" aria-label="Nossas unidades">
  <div class="units__header">
    <h2 class="units__title">Duas unidades.<br>Um só compromisso.</h2>
  </div>
  <div class="units__grid">

    <!-- Hospital 24h card (dark) -->
    <div class="unit unit--dark" tabindex="0" aria-label="Hospital Veterinário 24h — clique para ver detalhes">
      <div class="unit__inner">
        <!-- FRONT -->
        <div class="unit__front">
          <span class="unit__tag">Hospital Veterinário</span>
          <h3 class="unit__name">Emergência<br>24 horas.</h3>
          <p class="unit__desc">Atendimento de urgência e emergência ininterrupto, UTI veterinária equipada e equipe médica de plantão.</p>
          <a href="/hospital" class="btn btn--ghost unit__cta">Ver hospital →</a>
        </div>
        <!-- BACK -->
        <div class="unit__back" aria-hidden="true">
          <div class="unit__back-content">
            <p class="unit__back-label">Telefone</p>
            <p class="unit__back-value">(11) 2373-3144</p>
            <p class="unit__back-label">Endereço</p>
            <p class="unit__back-value">Rua Itapeti, 154<br>São Paulo – SP</p>
            <p class="unit__back-label">Horário</p>
            <p class="unit__back-value">24 horas, 7 dias por semana</p>
            <a href="tel:+551123733144" class="btn btn--accent unit__back-cta">Ligar agora →</a>
          </div>
        </div>
      </div>
    </div>

    <!-- Especialidades card (pale green) -->
    <div class="unit unit--light" tabindex="0" aria-label="Clínica de Especialidades — clique para ver detalhes">
      <div class="unit__inner">
        <!-- FRONT -->
        <div class="unit__front">
          <span class="unit__tag">Clínica de Especialidades</span>
          <h3 class="unit__name">25 especialidades<br>veterinárias.</h3>
          <p class="unit__desc">Consultas com especialistas, exames diagnósticos avançados e acompanhamento humanizado do início ao fim.</p>
          <a href="/especialidades" class="btn btn--primary unit__cta">Ver especialidades →</a>
        </div>
        <!-- BACK -->
        <div class="unit__back" aria-hidden="true">
          <div class="unit__back-content">
            <p class="unit__back-label">Telefone</p>
            <p class="unit__back-value">(11) 2373-3144</p>
            <p class="unit__back-label">Endereço</p>
            <p class="unit__back-value">Rua Itapeti, 154<br>São Paulo – SP</p>
            <p class="unit__back-label">Horário</p>
            <p class="unit__back-value">Seg–Sex: 9h–18h<br>Sáb: 9h–13h</p>
            <a href="/especialidades#contato" class="btn btn--primary unit__back-cta">Agendar consulta →</a>
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
.units {
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
  background: var(--clr-bg);
}

.units__header {
  max-width: var(--container);
  margin-inline: auto;
  margin-bottom: clamp(48px, 6vw, 80px);
}

.units__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.15;
  color: var(--clr-text);
  letter-spacing: -0.02em;
}

.units__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0; /* no gap — cards touch */
  max-width: var(--container);
  margin-inline: auto;
  border-radius: var(--radius-lg);
  overflow: hidden;
}
```

---

### Card Flip CSS

```css
/* ── Flip container ── */
.unit {
  position: relative;
  min-height: 360px;
  perspective: 1000px;
  cursor: pointer;
}

.unit__inner {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: inherit;
  transform-style: preserve-3d;
  transition: transform 600ms cubic-bezier(0.16, 1, 0.3, 1);
  will-change: transform;
}

/* Flip on hover (desktop) */
.unit:hover .unit__inner,
.unit:focus .unit__inner {
  transform: rotateY(180deg);
}

/* Front face */
.unit__front,
.unit__back {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: clamp(32px, 5vw, 56px);
}

/* Back face starts rotated */
.unit__back {
  transform: rotateY(180deg);
}

/* ── Dark card ── */
.unit--dark .unit__front { background: var(--clr-dark); }
.unit--dark .unit__back  { background: var(--clr-primary); }

/* Dark card grain overlay */
.unit--dark .unit__front::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 200px 200px;
  opacity: 0.03;
  mix-blend-mode: overlay;
  pointer-events: none;
  border-radius: inherit;
}

/* ── Light card ── */
.unit--light .unit__front { background: var(--clr-primary-pale); }
.unit--light .unit__back  { background: var(--clr-primary-pale); }

/* ── Typography inside cards ── */
.unit__tag {
  display: inline-block;
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 6px 14px;
  border-radius: 100px;
  margin-bottom: auto; /* push to top by using flex + margin-bottom auto trick */
  align-self: flex-start;
  position: absolute;
  top: clamp(32px, 5vw, 56px);
  left: clamp(32px, 5vw, 56px);
}

.unit--dark .unit__tag {
  background: rgba(201,168,76,0.15);
  border: 1px solid rgba(201,168,76,0.3);
  color: var(--clr-accent);
}
.unit--light .unit__tag {
  background: rgba(27,77,62,0.1);
  border: 1px solid rgba(27,77,62,0.2);
  color: var(--clr-primary);
}

.unit__name {
  font-family: var(--font-display);
  font-size: var(--fs-h3);
  line-height: 1.15;
  letter-spacing: -0.02em;
  margin-bottom: 16px;
}
.unit--dark .unit__name  { color: #FFFFFF; }
.unit--light .unit__name { color: var(--clr-text); }

.unit__desc {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  line-height: 1.6;
  margin-bottom: 32px;
}
.unit--dark .unit__desc  { color: rgba(255,255,255,0.6); }
.unit--light .unit__desc { color: var(--clr-muted); }

/* ── Back face content ── */
.unit__back-content {
  display: flex;
  flex-direction: column;
  gap: 4px;
  width: 100%;
}

.unit__back-label {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-top: 16px;
  margin-bottom: 2px;
}
.unit--dark .unit__back-label  { color: var(--clr-accent); }
.unit--light .unit__back-label { color: var(--clr-primary); }

.unit__back-value {
  font-family: var(--font-display);
  font-size: 1.1rem;
  line-height: 1.4;
}
.unit--dark .unit__back-value  { color: #FFFFFF; }
.unit--light .unit__back-value { color: var(--clr-text); }

.unit__back-cta {
  margin-top: 28px;
}
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .units__grid {
    grid-template-columns: 1fr;
    border-radius: var(--radius-lg);
    gap: 16px;
  }

  .unit {
    min-height: 280px;
    border-radius: var(--radius-lg);
  }

  /* On mobile: flip on click (JS toggles .is-flipped) */
  .unit:hover .unit__inner {
    transform: none; /* disable hover flip */
  }
  .unit.is-flipped .unit__inner {
    transform: rotateY(180deg);
  }
}
```

**JS for mobile flip (click toggle):**

```js
// Only enable click-flip on touch devices
if ('ontouchstart' in window) {
  document.querySelectorAll('.unit').forEach(card => {
    card.addEventListener('click', () => card.classList.toggle('is-flipped'));
  });
}
```

---

## Section 3 — Pilares ("O que nos diferencia")

**Archetype:** Editorial (linhas horizontais, estilo revista)
**Constraints:** Headline Outline Gigante (números 01-04) + Overlap Elements + View Timeline CSS + Stagger

---

### HTML Structure

```html
<section class="pillars" aria-label="Nossos diferenciais">
  <div class="pillars__container">
    <header class="pillars__header">
      <h2 class="pillars__title">O que nos<br>diferencia.</h2>
    </header>

    <div class="pillars__list">

      <div class="pillars__row" style="--row-i: 0">
        <span class="pillars__num" aria-hidden="true">01</span>
        <div class="pillars__content">
          <div class="pillars__tag">
            <i class="ph ph-cpu" aria-hidden="true"></i>
            <span>Tecnologia</span>
          </div>
          <h3 class="pillars__name">Tecnologia avançada</h3>
          <p class="pillars__text">Equipamentos de última geração — tomografia, endoscopia, ecocardiografia e cirurgia laparoscópica a serviço do diagnóstico preciso.</p>
        </div>
      </div>

      <div class="pillars__row" style="--row-i: 1">
        <span class="pillars__num" aria-hidden="true">02</span>
        <div class="pillars__content">
          <div class="pillars__tag">
            <i class="ph ph-stethoscope" aria-hidden="true"></i>
            <span>Equipe</span>
          </div>
          <h3 class="pillars__name">Equipe especializada</h3>
          <p class="pillars__text">Mais de 40 profissionais com especialização reconhecida — médicos veterinários, fisioterapeutas, nutricionistas e anestesiologistas.</p>
        </div>
      </div>

      <div class="pillars__row" style="--row-i: 2">
        <span class="pillars__num" aria-hidden="true">03</span>
        <div class="pillars__content">
          <div class="pillars__tag">
            <i class="ph ph-heart" aria-hidden="true"></i>
            <span>Cuidado</span>
          </div>
          <h3 class="pillars__name">Cuidado humanizado</h3>
          <p class="pillars__text">Cada animal é tratado como único. Comunicamos com transparência e mantemos tutores informados em cada etapa do atendimento.</p>
        </div>
      </div>

      <div class="pillars__row" style="--row-i: 3">
        <span class="pillars__num" aria-hidden="true">04</span>
        <div class="pillars__content">
          <div class="pillars__tag">
            <i class="ph ph-calendar-check" aria-hidden="true"></i>
            <span>Experiência</span>
          </div>
          <h3 class="pillars__name">22 anos de experiência</h3>
          <p class="pillars__text">Desde 2002 construindo confiança através de resultados — uma das clínicas veterinárias mais antigas e respeitadas de São Paulo.</p>
        </div>
      </div>

    </div>
  </div>
</section>
```

---

### Layout CSS

```css
.pillars {
  padding-block: var(--sp-section);
  background: var(--clr-bg);
}

.pillars__container {
  max-width: 900px;
  margin-inline: auto;
  padding-inline: var(--pad-x);
}

.pillars__header {
  margin-bottom: clamp(48px, 7vw, 80px);
}

.pillars__title {
  font-family: var(--font-display);
  font-size: var(--fs-h2);
  line-height: 1.1;
  color: var(--clr-text);
  letter-spacing: -0.02em;
}

/* ── Row layout ── */
.pillars__list {
  display: flex;
  flex-direction: column;
}

.pillars__row {
  display: grid;
  grid-template-columns: 140px 1fr;
  gap: 40px;
  align-items: start;
  padding-block: 40px;
  border-top: 1px solid var(--clr-border);
  position: relative;
  cursor: default;

  /* View Timeline animation */
  animation: fadeUpRow 0.7s ease-out both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
  animation-delay: calc(var(--row-i, 0) * 80ms);
}

.pillars__row:last-child {
  border-bottom: 1px solid var(--clr-border);
}

/* ── Giant outline number ── */
.pillars__num {
  font-family: var(--font-display);
  font-size: clamp(4rem, 9vw, 7rem);
  line-height: 1;
  color: transparent;
  -webkit-text-stroke: 1px rgba(27,77,62,0.15);
  text-stroke: 1px rgba(27,77,62,0.15);
  user-select: none;
  display: block;
  /* Overlap: number bleeds beyond its 140px column */
  margin-right: -20px;
  transition: -webkit-text-stroke-color 400ms ease, opacity 400ms ease;
  opacity: 1;
  /* Number uses stroke opacity rather than color opacity for correct rendering */
  -webkit-text-stroke-color: rgba(27,77,62,0.15);
}

.pillars__row:hover .pillars__num {
  -webkit-text-stroke-color: rgba(27,77,62,0.35);
  transition: -webkit-text-stroke-color 400ms ease;
}

/* ── Content ── */
.pillars__content {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding-top: 8px; /* align baseline with number */
}

.pillars__tag {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-accent);
}

.pillars__tag i {
  font-size: 1rem;
  color: var(--clr-accent);
}

.pillars__name {
  font-family: var(--font-display);
  font-size: 1.6rem;
  line-height: 1.25;
  color: var(--clr-text);
  letter-spacing: -0.01em;
  margin: 0;
}

.pillars__text {
  font-family: var(--font-body);
  font-size: 0.95rem;
  line-height: 1.7;
  color: var(--clr-muted);
  max-width: 560px;
  margin: 0;
}

/* ── Keyframes ── */
@keyframes fadeUpRow {
  from {
    opacity: 0;
    transform: translateY(24px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

### Fallback for browsers without animation-timeline (JS)

```js
// Feature detect CSS animation-timeline
const supportsTimeline = CSS.supports('animation-timeline', 'view()');
if (!supportsTimeline) {
  const rows = document.querySelectorAll('.pillars__row');
  const io = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => {
          e.target.style.cssText = 'opacity:1; transform:translateY(0); transition: opacity 700ms ease, transform 700ms ease';
          io.unobserve(e.target);
        }, i * 80);
      }
    });
  }, { threshold: 0.15 });
  rows.forEach(r => {
    r.style.cssText = 'opacity:0; transform:translateY(24px)';
    io.observe(r);
  });
}
```

---

### Responsive Breakpoints

#### < 760px (mobile)

```css
@media (max-width: 760px) {
  .pillars__row {
    grid-template-columns: 1fr;
    gap: 8px;
    padding-block: 32px;
  }

  .pillars__num {
    font-size: clamp(3rem, 14vw, 5rem);
    margin-right: 0;
    /* Number goes above content */
    order: -1;
  }

  .pillars__content {
    padding-top: 0;
  }
}
```

---

## Section 4 — Depoimentos

**Archetype:** Single Focus com carousel CSS puro
**Constraints:** Aspas Decorativas Gigantes + Slide In + Counter Stars (aparecem uma a uma) + Dark Mode

---

### HTML Structure

```html
<section class="testimonials" aria-label="Depoimentos de clientes">
  <div class="testimonials__inner">

    <!-- Radio controls (CSS carousel) -->
    <input type="radio" name="testimonial" id="t1" class="testimonials__radio" checked>
    <input type="radio" name="testimonial" id="t2" class="testimonials__radio">
    <input type="radio" name="testimonial" id="t3" class="testimonials__radio">

    <!-- Decorative quote marks -->
    <div class="testimonials__quote-mark" aria-hidden="true">"</div>

    <!-- Track -->
    <div class="testimonials__track-wrapper">
      <div class="testimonials__track">

        <div class="testimonials__slide">
          <div class="testimonials__stars" aria-label="5 estrelas">
            <i class="ph-fill ph-star" style="--star-i:0" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:1" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:2" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:3" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:4" aria-hidden="true"></i>
          </div>
          <blockquote class="testimonials__quote">
            "Minha cadela precisou de cirurgia de emergência às 3h da manhã. A equipe do hospital foi incrível — profissional, humana e super atenciosa durante toda a recuperação."
          </blockquote>
          <footer class="testimonials__author">
            <p class="testimonials__name">Ana Paula M.</p>
            <p class="testimonials__pet">Tutora da Luna, Golden Retriever</p>
          </footer>
        </div>

        <div class="testimonials__slide">
          <div class="testimonials__stars" aria-label="5 estrelas">
            <i class="ph-fill ph-star" style="--star-i:0" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:1" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:2" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:3" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:4" aria-hidden="true"></i>
          </div>
          <blockquote class="testimonials__quote">
            "A especialidade de neurologia da VetPiera salvou a vida do meu gato. O Dr. Ryan explicou cada etapa do diagnóstico com paciência e cuidado extraordinários."
          </blockquote>
          <footer class="testimonials__author">
            <p class="testimonials__name">Carlos Eduardo R.</p>
            <p class="testimonials__pet">Tutor do Simba, Persa</p>
          </footer>
        </div>

        <div class="testimonials__slide">
          <div class="testimonials__stars" aria-label="5 estrelas">
            <i class="ph-fill ph-star" style="--star-i:0" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:1" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:2" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:3" aria-hidden="true"></i>
            <i class="ph-fill ph-star" style="--star-i:4" aria-hidden="true"></i>
          </div>
          <blockquote class="testimonials__quote">
            "Faço acompanhamento com a Dra. Diana há dois anos para a fisioterapia da minha cachorra. A evolução é impressionante e o atendimento é sempre excepcional."
          </blockquote>
          <footer class="testimonials__author">
            <p class="testimonials__name">Mariana F.</p>
            <p class="testimonials__pet">Tutora da Mel, Labrador</p>
          </footer>
        </div>

      </div>
    </div>

    <!-- Navigation dots -->
    <nav class="testimonials__nav" aria-label="Navegar entre depoimentos">
      <label for="t1" class="testimonials__dot" aria-label="Depoimento 1"></label>
      <label for="t2" class="testimonials__dot" aria-label="Depoimento 2"></label>
      <label for="t3" class="testimonials__dot" aria-label="Depoimento 3"></label>
    </nav>

  </div>
</section>
```

---

### Layout CSS

```css
/* Hide radios visually */
.testimonials__radio {
  position: absolute;
  opacity: 0;
  pointer-events: none;
  width: 0;
  height: 0;
}

.testimonials {
  background: var(--clr-dark);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
  position: relative;
  overflow: hidden;
}

.testimonials__inner {
  max-width: 900px;
  margin-inline: auto;
  position: relative;
}

/* ── Decorative quote mark ── */
.testimonials__quote-mark {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(8rem, 20vw, 16rem);
  line-height: 1;
  color: rgba(201,168,76,0.08);
  position: absolute;
  top: -20px;
  left: calc(-1 * var(--pad-x));
  pointer-events: none;
  user-select: none;
  z-index: 0;
}

/* ── Track wrapper ── */
.testimonials__track-wrapper {
  overflow: hidden;
  position: relative;
  z-index: 1;
}

.testimonials__track {
  display: flex;
  transition: transform 600ms cubic-bezier(0.16, 1, 0.3, 1);
}

/* ── Individual slide ── */
.testimonials__slide {
  min-width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding-inline: clamp(0px, 4vw, 60px);
}

/* ── Stars ── */
.testimonials__stars {
  display: flex;
  gap: 4px;
  margin-bottom: 32px;
}

.testimonials__stars i {
  font-size: 1.125rem;
  color: var(--clr-accent);
  opacity: 0; /* animated in via JS on slide change */
  animation: starPop 200ms ease-out both;
  animation-delay: calc(var(--star-i, 0) * 100ms);
}

@keyframes starPop {
  from {
    opacity: 0;
    transform: scale(0.4);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* ── Quote ── */
.testimonials__quote {
  font-family: var(--font-display);
  font-size: clamp(1.4rem, 3vw, 2.2rem);
  line-height: 1.45;
  color: rgba(255,255,255,0.90);
  max-width: 820px;
  margin: 0 auto 32px;
  font-style: normal;
}

/* ── Author ── */
.testimonials__name {
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--clr-accent);
  margin-bottom: 6px;
}

.testimonials__pet {
  font-family: var(--font-body);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: rgba(255,255,255,0.40);
}

/* ── Navigation dots ── */
.testimonials__nav {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 48px;
}

.testimonials__dot {
  display: block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255,255,255,0.20);
  cursor: pointer;
  transition:
    background 300ms ease,
    width 300ms ease,
    border-radius 300ms ease;
}

/* ── CSS Carousel — radio-driven track position ── */
#t1:checked ~ .testimonials__track-wrapper .testimonials__track { transform: translateX(0%);   }
#t2:checked ~ .testimonials__track-wrapper .testimonials__track { transform: translateX(-100%); }
#t3:checked ~ .testimonials__track-wrapper .testimonials__track { transform: translateX(-200%); }

/* Active dot styling via sibling selectors */
#t1:checked ~ .testimonials__nav label:nth-child(1),
#t2:checked ~ .testimonials__nav label:nth-child(2),
#t3:checked ~ .testimonials__nav label:nth-child(3) {
  background: var(--clr-accent);
  width: 24px;
  border-radius: 4px;
}
```

---

### Star animation JS (reset on slide change)

```js
// Re-trigger star animation when slide changes
document.querySelectorAll('.testimonials__radio').forEach(radio => {
  radio.addEventListener('change', () => {
    const activeSlideIndex = [...document.querySelectorAll('.testimonials__radio')].findIndex(r => r.checked);
    const slides = document.querySelectorAll('.testimonials__slide');
    const stars = slides[activeSlideIndex].querySelectorAll('.testimonials__stars i');
    stars.forEach(star => {
      star.style.animation = 'none';
      star.offsetHeight; // reflow
      star.style.animation = '';
    });
  });
});
```

---

### Responsive Breakpoints

#### < 768px (mobile)

```css
@media (max-width: 768px) {
  .testimonials__quote-mark {
    font-size: clamp(6rem, 25vw, 10rem);
    left: 0;
  }
  .testimonials__slide {
    padding-inline: 0;
  }
  .testimonials__quote {
    font-size: clamp(1.15rem, 4.5vw, 1.5rem);
  }
}
```

---

## Section 5 — Parceria ("Você é veterinário?")

**Archetype:** Minimal / White Space Hero
**Constraints:** Container Narrow + Diagonal Divider Decorativo + Hover Glow no CTA

---

### HTML Structure

```html
<section class="partnership" aria-label="Parceria com veterinários">
  <!-- Decorative SVG diagonal line -->
  <svg class="partnership__deco" aria-hidden="true" preserveAspectRatio="none"
       viewBox="0 0 1440 200" xmlns="http://www.w3.org/2000/svg">
    <line x1="0" y1="180" x2="1440" y2="20"
          stroke="#E2E8E5" stroke-width="1"/>
  </svg>

  <div class="partnership__body">
    <span class="partnership__eyebrow">Para profissionais</span>
    <h2 class="partnership__title">Você é veterinário?</h2>
    <p class="partnership__sub">A VetPiera oferece infraestrutura completa, equipe de suporte e ambiente colaborativo para médicos veterinários que buscam crescer junto a uma referência.</p>
    <a href="/parceiros" class="btn btn--outline partnership__cta">Seja parceiro →</a>
  </div>
</section>
```

---

### Layout CSS

```css
.partnership {
  background: var(--clr-bg);
  padding-block: var(--sp-section);
  padding-inline: var(--pad-x);
  position: relative;
  overflow: hidden;
}

/* Diagonal SVG line decoration */
.partnership__deco {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

/* Narrow centered column */
.partnership__body {
  position: relative;
  z-index: 1;
  max-width: 480px;
  margin-inline: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: clamp(16px, 2.5vw, 24px);
}

.partnership__eyebrow {
  font-family: var(--font-body);
  font-size: var(--fs-sm);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--clr-accent);
}

.partnership__title {
  font-family: var(--font-display);
  font-size: var(--fs-h3);
  line-height: 1.2;
  color: var(--clr-text);
  letter-spacing: -0.02em;
  margin: 0;
}

.partnership__sub {
  font-family: var(--font-body);
  font-size: var(--fs-body);
  line-height: 1.65;
  color: var(--clr-muted);
  margin: 0;
}

/* CTA: outline style from base .btn--outline */
/* Override: border color is #1A1A1A (already default) */
.partnership__cta {
  border-color: var(--clr-text);
  margin-top: 8px;
}

/* Hover: glow instead of fill */
.partnership__cta:hover {
  background: transparent;
  color: var(--clr-text);
  box-shadow: 0 0 0 4px rgba(27,77,62,0.15);
  transform: none; /* override global btn translateY */
}
```

---

### Scroll-triggered entrance animation

```css
.partnership__body {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 700ms var(--ease-out-expo), transform 700ms var(--ease-out-expo);
}

.partnership__body.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

```js
const io = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('is-visible');
      io.unobserve(e.target);
    }
  });
}, { threshold: 0.3 });
io.observe(document.querySelector('.partnership__body'));
```

---

### Responsive Breakpoints

No breakpoints needed — `max-width: 480px` with `margin-inline: auto` already handles all sizes. On mobile, `padding-inline: var(--pad-x)` provides natural constraints. The SVG decorative line is hidden on very small screens:

```css
@media (max-width: 480px) {
  .partnership__deco {
    opacity: 0.5;
  }
}
```

---

## Section 6 — Footer

**Archetype:** Contained Center com grid editorial
**Constraints:** Color Blocking (preto profundo) + Broken Grid (logo escapa 20px acima) + Selective Color (apenas accent como cor)

---

### HTML Structure

```html
<footer class="footer" aria-label="Rodapé">
  <div class="footer__container">
    <!-- Logo escapes upward (Broken Grid effect) -->
    <div class="footer__logo-wrap">
      <a href="/" class="footer__logo" aria-label="VetPiera — Página inicial">
        <img src="/images/logo-white.svg" alt="VetPiera" width="140" height="40">
      </a>
    </div>

    <div class="footer__grid">

      <!-- Col 1: brand + description + social -->
      <div class="footer__col footer__col--brand">
        <p class="footer__tagline">Cuidado veterinário de excelência desde 2002.</p>
        <div class="footer__social">
          <a href="https://instagram.com/vetpiera" class="footer__social-link" aria-label="Instagram" target="_blank" rel="noopener">
            <i class="ph ph-instagram-logo" aria-hidden="true"></i>
          </a>
          <a href="https://facebook.com/vetpiera" class="footer__social-link" aria-label="Facebook" target="_blank" rel="noopener">
            <i class="ph ph-facebook-logo" aria-hidden="true"></i>
          </a>
          <a href="https://wa.me/5511991334520" class="footer__social-link" aria-label="WhatsApp" target="_blank" rel="noopener">
            <i class="ph ph-whatsapp-logo" aria-hidden="true"></i>
          </a>
        </div>
      </div>

      <!-- Col 2: Hospital 24h -->
      <div class="footer__col">
        <h4 class="footer__col-title">Hospital 24h</h4>
        <ul class="footer__list">
          <li><a href="/hospital" class="footer__link">Serviços hospitalares</a></li>
          <li><a href="/hospital#emergencia" class="footer__link">Emergência veterinária</a></li>
          <li><a href="/hospital#uti" class="footer__link">UTI veterinária</a></li>
          <li class="footer__hours">24h · 7 dias por semana</li>
          <li><a href="tel:+551123733144" class="footer__link">(11) 2373-3144</a></li>
        </ul>
      </div>

      <!-- Col 3: Especialidades -->
      <div class="footer__col">
        <h4 class="footer__col-title">Especialidades</h4>
        <ul class="footer__list">
          <li><a href="/especialidades" class="footer__link">Ver todas as especialidades</a></li>
          <li><a href="/especialidades#neurologias" class="footer__link">Neurologia</a></li>
          <li><a href="/especialidades#ortopedia" class="footer__link">Ortopedia</a></li>
          <li><a href="/especialidades#fisioterapia" class="footer__link">Fisioterapia</a></li>
          <li class="footer__hours">Seg–Sex: 9h–18h · Sáb: 9h–13h</li>
        </ul>
      </div>

    </div>

    <div class="footer__bottom">
      <p class="footer__copy">© 2026 VetPiera. Todos os direitos reservados.</p>
    </div>
  </div>
</footer>
```

---

### Layout CSS

```css
.footer {
  background: var(--clr-dark);
  padding-bottom: clamp(40px, 6vw, 64px);
  /* No padding-top — logo handles the top spacing via negative margin */
}

.footer__container {
  max-width: var(--container);
  margin-inline: auto;
  padding-inline: var(--pad-x);
}

/* ── Logo escapes upward (Broken Grid) ── */
.footer__logo-wrap {
  display: flex;
  justify-content: flex-start;
  margin-top: -20px;   /* escapes above footer border */
  padding-top: clamp(40px, 6vw, 72px);
  margin-bottom: clamp(40px, 5vw, 64px);
  position: relative;
  z-index: 2;
}

.footer__logo {
  display: inline-block;
  /* No additional styles needed — image provides sizing */
}

.footer__logo img {
  display: block;
  height: 36px;
  width: auto;
}

/* ── Main grid ── */
.footer__grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr;
  gap: clamp(40px, 6vw, 96px);
  padding-bottom: clamp(40px, 5vw, 64px);
  border-bottom: 1px solid rgba(255,255,255,0.08);
}

/* ── Brand column ── */
.footer__tagline {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  line-height: 1.6;
  color: rgba(255,255,255,0.40);
  max-width: 280px;
  margin-bottom: 28px;
}

.footer__social {
  display: flex;
  gap: 16px;
}

.footer__social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background: rgba(255,255,255,0.06);
  color: rgba(255,255,255,0.50);
  text-decoration: none;
  font-size: 1.125rem;
  transition: background 250ms ease, color 250ms ease;
}

.footer__social-link:hover {
  background: rgba(201,168,76,0.15);
  color: var(--clr-accent); /* Selective Color: only accent as color */
}

/* ── Column typography ── */
.footer__col-title {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.30);
  margin-bottom: 20px;
}

.footer__list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.footer__link {
  font-family: var(--font-body);
  font-size: 0.9375rem;
  color: rgba(255,255,255,0.55);
  text-decoration: none;
  transition: color 250ms ease;
}

.footer__link:hover {
  color: var(--clr-accent); /* Selective Color */
}

/* Hours display (not a link) */
.footer__hours {
  font-family: var(--font-body);
  font-size: 0.8125rem;
  color: var(--clr-accent); /* always gold — selective color */
  margin-top: 8px;
}

/* ── Bottom bar ── */
.footer__bottom {
  padding-top: clamp(24px, 3vw, 40px);
  text-align: center;
}

.footer__copy {
  font-family: var(--font-body);
  font-size: 0.75rem;
  color: rgba(255,255,255,0.20);
}
```

---

### Responsive Breakpoints

#### < 1024px (tablet)

```css
@media (max-width: 1024px) {
  .footer__grid {
    grid-template-columns: 1fr 1fr;
    gap: clamp(32px, 4vw, 56px);
  }
  .footer__col--brand {
    grid-column: 1 / -1; /* full width on first row */
  }
}
```

#### < 640px (mobile)

```css
@media (max-width: 640px) {
  .footer__grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .footer__logo-wrap {
    margin-top: -12px;
  }
}
```

---

## Global Accessibility Notes

- All interactive elements have `:focus-visible` outlines: `outline: 2px solid var(--clr-accent); outline-offset: 4px`
- Carousel navigation uses `<label for="">` tied to radio inputs — keyboard accessible
- Flip cards are `tabindex="0"` with keyboard trigger on `Enter`/`Space`
- All decorative elements have `aria-hidden="true"`
- Color contrast ratios: all text on dark backgrounds checked to WCAG AA minimum

```css
/* Global focus style */
:focus-visible {
  outline: 2px solid var(--clr-accent);
  outline-offset: 4px;
  border-radius: 4px;
}

/* Flip card keyboard trigger */
.unit:focus-within .unit__inner {
  transform: rotateY(180deg);
}
```

---

## Asset Requirements

| Asset | Dimensions | Format | Notes |
|---|---|---|---|
| `/images/hero-placeholder.jpg` | 900×1100px | JPG | Dark moody vet clinic interior |
| `/images/logo-white.svg` | 140×40px | SVG | White version |
| `/images/logo-dark.svg` | 140×40px | SVG | Dark version for light bg |
| Phosphor Icons | CDN | SVG font | `ph`, `ph-fill` classes |
| DM Serif Display | Google Fonts | Woff2 | weights: 400 |
| DM Sans | Google Fonts | Woff2 | weights: 400, 500, 600 |

---

## Performance Notes

- Hero photo lazy: `loading="eager"` (above fold)
- All other images: `loading="lazy"`
- Fonts: `<link rel="preconnect" href="https://fonts.googleapis.com">` in `<head>`
- JS animations check `prefers-reduced-motion`: if true, skip all transform/opacity animations, show elements in final state immediately

```js
const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
if (reducedMotion) {
  document.querySelectorAll('.hero__word').forEach(w => w.classList.add('is-revealed'));
  document.querySelector('.hero__sub').classList.add('is-visible');
  document.querySelector('.hero__actions').classList.add('is-visible');
  document.getElementById('heroBadgeCounter').textContent = '22';
}
```
