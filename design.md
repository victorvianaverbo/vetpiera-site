# Identidade Visual — VetPiera (Proposta Premium)

---

## Identidade Atual — Problemas

| Elemento | Atual | Problema |
|---|---|---|
| Cor primária | #86C232 (verde limão saturado) | Tom brilhante demais, associado a sites baratos |
| Gradiente | #1a4e17 → #2a7a22 | Muito escuro e sem harmonia com o verde primário |
| Fonte heading | Lora 700 | Boa, mas muito comum — não diferencia |
| Fonte body | Roboto 400 | Genérica demais para posicionamento premium |
| Botão primário | border-radius: 50px (pílula) | Forma genérica, "Web 2.0" |
| Espaçamento | section padding: 30px | Muito apertado — parece bagunçado |
| Sombras | 6px 6px 9px rgba(0,0,0,0.2) | Angular e datada |

---

## Paleta de Cores — Proposta Premium

### Cor Principal
```
--color-primary:     #1B4D3E   /* verde floresta profundo — autoridade, saúde */
--color-primary-light: #2A6B56  /* hover states, gradientes suaves */
--color-primary-pale:  #E8F2ED  /* fundos suaves, seções alternadas */
```

### Acento
```
--color-accent:      #C9A84C   /* ouro/bronze quente — toque premium */
--color-accent-dark: #A88535   /* hover do acento */
```

### Neutros
```
--color-bg:          #FAFAF8   /* branco quente — mais sofisticado que #fff puro */
--color-surface:     #FFFFFF   /* fundo de cards */
--color-border:      #E2E8E5   /* bordas suaves */

--color-text-primary:   #1A1A1A   /* títulos e texto principal */
--color-text-secondary: #5C6B74   /* texto de apoio, legendas */
--color-text-inverse:   #FFFFFF   /* texto sobre fundos escuros */
```

### Footer / Escuro
```
--color-dark:        #0F2D24   /* footer, seções de destaque escuras */
--color-dark-medium: #1B4D3E   /* variação */
```

### Razão da escolha
- Verde floresta (#1B4D3E) remete a natureza, saúde e seriedade sem parecer barato
- Ouro (#C9A84C) adiciona toque premium sem exagero — funciona como acento em CTAs secundários, ícones e detalhes
- O branco quente (#FAFAF8) faz o site respirar e parecer mais cuidado que o branco puro

---

## Tipografia — Proposta Premium

### Fonte de Título: DM Serif Display
```css
font-family: 'DM Serif Display', serif;
font-weight: 400; /* a fonte já tem personalidade com peso regular */
```
- Elegante, moderna, com personalidade sem ser carregada
- Ideal para headlines de impacto em clínicas e serviços de saúde de alto padrão
- Google Fonts: https://fonts.google.com/specimen/DM+Serif+Display

### Fonte de Corpo: DM Sans
```css
font-family: 'DM Sans', sans-serif;
font-weight: 300 | 400 | 500;
```
- Família irmã da DM Serif — harmonia perfeita entre headline e corpo
- Leitura limpa, espaçamento generoso, moderna
- Google Fonts: https://fonts.google.com/specimen/DM+Sans

### Escala Tipográfica
```css
--font-heading:  'DM Serif Display', serif;
--font-body:     'DM Sans', sans-serif;

/* Tamanhos fluidos (clamp: mobile → desktop) */
--text-hero:     clamp(2.5rem, 5vw, 4rem);      /* headline principal */
--text-h2:       clamp(2rem, 4vw, 3rem);         /* títulos de seção */
--text-h3:       clamp(1.25rem, 2.5vw, 1.75rem); /* subtítulos */
--text-body:     clamp(1rem, 1.5vw, 1.125rem);   /* corpo */
--text-small:    0.875rem;                        /* legendas, labels */

/* Line-heights */
--lh-heading: 1.2;
--lh-body:    1.65;
```

---

## Botões — Proposta Premium

```css
/* Primário — verde floresta sólido */
.btn-primary {
  background: var(--color-primary);
  color: var(--color-text-inverse);
  border-radius: 8px;           /* retangular arredondado — não pílula */
  padding: 14px 32px;
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 1rem;
  letter-spacing: 0.02em;
  transition: background 0.2s, transform 0.15s;
}
.btn-primary:hover {
  background: var(--color-primary-light);
  transform: translateY(-1px);  /* elevação sutil */
}

/* Secundário — outlined */
.btn-secondary {
  background: transparent;
  color: var(--color-primary);
  border: 1.5px solid var(--color-primary);
  border-radius: 8px;
  padding: 13px 32px;
  font-weight: 500;
  transition: background 0.2s, color 0.2s;
}
.btn-secondary:hover {
  background: var(--color-primary);
  color: var(--color-text-inverse);
}

/* Acento — ouro (uso pontual, ex: depoimentos, parceria) */
.btn-accent {
  background: var(--color-accent);
  color: var(--color-dark);
  border-radius: 8px;
  padding: 14px 32px;
  font-weight: 600;
}
```

---

## Componentes — Cards

```css
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: 32px;
  /* sem box-shadow pesada — bordar suaves funcionam melhor no premium */
}

/* Card com destaque de topo (usado nos pilares/diferenciais) */
.card--accent-top {
  border-top: 3px solid var(--color-primary);
}

/* Card escuro (usado em depoimentos) */
.card--dark {
  background: var(--color-dark);
  color: var(--color-text-inverse);
  border: none;
}
```

---

## Espaçamento

```css
/* Espaçamentos generosos — o que faz o site parecer premium */
--spacing-section:  clamp(80px, 10vw, 120px);  /* entre seções */
--spacing-inner:    clamp(40px, 5vw, 64px);     /* dentro das seções */
--spacing-card-gap: clamp(16px, 3vw, 32px);     /* entre cards */

/* Container */
--container-max: 1200px;
--container-padding: clamp(24px, 5vw, 80px);
```

---

## Header

```
Fundo: #FFFFFF com border-bottom: 1px solid var(--color-border)
Logo: versão verde floresta (#1B4D3E)
Nav links: --color-text-primary, hover: --color-primary
CTA no header: .btn-primary (verde floresta)
Position: sticky, top: 0
```

---

## Hero — Tratamento Visual

```
Fundo: var(--color-bg) ou imagem com overlay
Overlay (se usar foto): linear-gradient(135deg, rgba(15,45,36,0.75) 0%, rgba(27,77,62,0.4) 100%)
Headline: var(--font-heading), --text-hero, --color-text-inverse (sobre foto)
Subheadline: var(--font-body), --text-body * 1.1, opacity: 0.9
```

---

## Seções Alternadas

```
Seção padrão:      fundo var(--color-bg)       — #FAFAF8
Seção destaque:    fundo var(--color-primary-pale) — #E8F2ED
Seção escura:      fundo var(--color-dark)      — #0F2D24 (depoimentos, footer)
```

---

## Resumo Visual — Antes vs. Depois

| | Antes | Depois |
|---|---|---|
| Verde primário | #86C232 (limão saturado) | #1B4D3E (floresta profundo) |
| Acento | nenhum | #C9A84C (ouro/bronze) |
| Fonte heading | Lora | DM Serif Display |
| Fonte body | Roboto | DM Sans |
| Botão shape | 50px radius (pílula) | 8px radius (retangular) |
| Espaçamento seções | 30px | 80–120px |
| Fundo | #FFFFFF puro | #FAFAF8 (branco quente) |
| Sombras | Angulares e pesadas | Removidas — substituídas por bordas sutis |
| Sensação geral | Clínica popular, web 2.0 | Premium, especializada, confiável |
