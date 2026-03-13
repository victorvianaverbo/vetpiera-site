---
description: desenvolver
---

# Instruções

Você vai construir a página completa. Seu trabalho é pegar o design aprovado (hero + primeira seção) e expandir para todas as seções da copy, mantendo a linguagem visual e elevando a qualidade seção por seção.

## Etapa 1: Carregar a Especificação

### Identificar a Pasta da Pagina

Identifique em qual pasta da pagina voce esta trabalhando. Os arquivos devem estar dentro da pasta criada pelo `/gerar-copy` (ex: `pagina-vendas/`).

**IMPORTANTE:** Pastas com prefixo `_backup_` sao versoes antigas - IGNORE-AS.

### Arquivos Necessarios

1. Leia o `copy.md` — todas as seções que precisam ser construídas
2. Leia o `index.html` e `style.css` atuais — o hero + primeira seção já aprovados definem a linguagem visual

### Extrair a Linguagem Visual do Design Aprovado

Antes de construir qualquer seção, extraia do `index.html` e `style.css` existentes:
- Paleta de cores exata (hex codes)
- Font pairing usado (heading + body) — MANTER o mesmo em toda a página
- Espaçamentos e proporções
- Tom das animações e estilo de interatividade
- Elementos gráficos/decorativos recorrentes

## Etapa 2: Consultar a Skill Creative Reference

ANTES de planejar qualquer seção, leia `.agent/skills/creative-reference/SKILL.md`.

Para CADA seção nova, escolha:
1. **UM arquétipo** — diferente das seções anteriores
2. **2+ constraints** de categorias diferentes

**NUNCA repita o mesmo arquétipo em seções consecutivas.**

**NUNCA use padrões genéricos:** 3 cards lado a lado, grid simétrico de features, depoimentos com foto circular, bullets com checkmarks, FAQ com accordion básico.

## Etapa 3: Planejar e Construir Seção por Seção

Antes de começar, liste para o usuário:
1. Quais seções serão construídas (baseado no `copy.md`)
2. O arquétipo escolhido para cada seção
3. Bibliotecas externas necessárias, se houver

### Processo para cada seção

1. **Declare o arquétipo, constraints e justificativa** — ex: "Seção X: Arquétipo Layered + Constraints Glassmorphism e Hover Lift. Justificativa: o conteúdo de depoimentos se beneficia da profundidade visual."
2. **Implemente o HTML** com semântica correta
3. **Implemente o CSS** com valores exatos (nunca aproximados)
4. **Adicione elementos encantadores** — veja seção abaixo
5. **Implemente interatividade** (hover, animações, scroll)
6. **Verifique visualmente** antes de passar para a próxima

### Regras de Implementação

#### HTML
- Use semântica correta (section, article, figure, etc.)
- Adicione `data-aos` onde especificado
- Use classes descritivas e consistentes
- Inclua todos os atributos de acessibilidade

#### CSS — Nível de Detalhe Obrigatório

Use valores exatos. Nunca vague:

- NAO "padding grande" → SIM `padding: 80px 0`
- NAO "animacao legal" → SIM `fade-up 800ms ease-out delay 200ms, triggered at 20% viewport`
- NAO "hover bonito" → SIM `translateY(-8px) + scale(1.02) + box-shadow 0 20px 40px rgba(0,0,0,0.2), 400ms cubic-bezier(0.16, 1, 0.3, 1)`
- NAO "texto grande" → SIM `clamp(2.5rem, 5vw, 4.5rem), font-weight 700, line-height 1.1`
- NAO "cor escura" → SIM `#1A1A2E`

Siga a linguagem visual do design aprovado (cores, fontes, espaçamentos do hero). Implemente TODOS os estados (hover, active, focus). Responsividade completa (mobile-first).

#### JavaScript (se necessário)
- Adicione no `script.js` existente
- Comente o código para clareza
- Evite bibliotecas pesadas quando possível com vanilla JS

### O que NUNCA fazer

- NUNCA omitir uma animação porque "dá trabalho"
- NUNCA simplificar um efeito porque "é complexo"
- NUNCA pular a responsividade
- NUNCA ignorar estados de hover/focus
- NUNCA usar cores aproximadas (use os hex exatos)
- NUNCA mudar medidas especificadas
- NUNCA remover elementos decorativos

### Elementos Encantadores (adicionar em cada seção)

Além do óbvio, adicione elementos que surpreendem:

**Micro-interações:**
- Cursores customizados em áreas específicas
- Tooltips animados
- Feedback visual em interações
- Estados de loading interessantes

**Animações Elaboradas:**
- Parallax em elementos específicos
- Elementos que seguem o mouse
- Scroll-linked animations (CSS `animation-timeline`)
- Reveal com `clip-path`
- Stagger animations

**Detalhes de Craft:**
- Gradientes em textos
- Glassmorphism
- Noise/grain textures
- Linhas decorativas animadas
- Shapes orgânicos flutuantes
- Efeitos de luz/glow
- `mix-blend-mode` criativos

**Surpresas:**
- Transições inesperadas
- Easter eggs sutis
- Animações que recompensam exploração

### Se algo não estiver claro

Se alguma especificação estiver ambígua:
1. Releia o contexto ao redor
2. Considere o design aprovado como referência
3. Se ainda estiver ambíguo, PERGUNTE ao usuário antes de assumir

## Etapa 4: Checklist de Finalização (OBRIGATÓRIO)

**A tarefa NÃO está completa até passar por TODOS os itens abaixo.**

### Verificação de Completude
- [ ] Todas as seções do `copy.md` foram implementadas?
- [ ] Nenhuma seção foi simplificada ou omitida?
- [ ] Cada seção tem arquétipo e constraints próprios?

### Fidelidade Criativa
- [ ] O font pairing foi mantido consistente em toda a página?
- [ ] A paleta de cores está consistente com o design aprovado?
- [ ] Nenhum padrão genérico foi introduzido (3 cards, grid simétrico)?

### Performance (Crítico)
- [ ] Todas imagens usando Netlify CDN (`/.netlify/images?url=...`)
- [ ] Imagens com width/height numéricos definidos
- [ ] Hero SEM animação de entrada (opacity:0, fade-in, data-aos)
- [ ] Hero com `loading="eager"`, resto com `loading="lazy"`
- [ ] Scripts pesados (Three.js, GSAP) com Dynamic Import + IntersectionObserver
- [ ] AOS inicializado com `disableMutationObserver: true`

### Acessibilidade
- [ ] Todos os links/botões com foco visível
- [ ] Imagens com alt text descritivo
- [ ] Contraste de cores adequado
- [ ] Hierarquia de headings correta (h1 → h2 → h3)
- [ ] Formulário com labels e atributos corretos

### Responsividade
- [ ] Testado em 375px (mobile)
- [ ] Testado em 768px (tablet)
- [ ] Testado em 1440px (desktop)
- [ ] Nenhum overflow horizontal em nenhuma resolução
- [ ] Textos legíveis em todas as resoluções

### Animações e Interatividade
- [ ] Todas as animações especificadas implementadas
- [ ] Todos os hovers funcionando
- [ ] Transições suaves em todos os estados
- [ ] Feedback visual em interações

### Validação Final
Antes de informar que está pronto:
1. **Abra o DevTools** (F12)
2. **Verifique o Console** - não deve ter erros em vermelho
3. **Verifique o Network** - não deve ter 404
4. **Teste o formulário** - deve estar configurado corretamente

## Etapa 5: Apresentar ao Usuário

Após completar:

1. Informe que a página está pronta
2. Liste as seções construídas
3. Destaque funcionalidades especiais implementadas
4. Forneça o link (use a skill `local-server` para obter a URL correta)
5. Peça feedback

## Bibliotecas Permitidas (CDN)

Se a especificação pedir, você pode usar via CDN:

```html
<!-- Ícones (leve, pode ser CDN direto) -->
<script src="https://unpkg.com/@phosphor-icons/web" defer></script>
```

**Bibliotecas pesadas (GSAP, Three.js, particulas):** NUNCA adicionar via `<script>` no HTML. Usar Dynamic Import + IntersectionObserver no `script.js`:

```javascript
// Carrega GSAP apenas quando a secao que precisa fica visivel
function lazyLoadModule(selector, loadFn) {
  const el = document.querySelector(selector);
  if (!el) return;
  const obs = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) { obs.disconnect(); loadFn(); }
  }, { rootMargin: '200px' });
  obs.observe(el);
}

// GSAP + ScrollTrigger
lazyLoadModule('#secao-animada', async () => {
  const { gsap } = await import('https://cdn.jsdelivr.net/npm/gsap@3.12.2/+esm');
  const { ScrollTrigger } = await import('https://cdn.jsdelivr.net/npm/gsap@3.12.2/ScrollTrigger/+esm');
  gsap.registerPlugin(ScrollTrigger);
  // ... usar gsap aqui
});

// Three.js
lazyLoadModule('#secao-3d', async () => {
  const THREE = await import('https://cdn.jsdelivr.net/npm/three@0.155.0/+esm');
  // ... usar THREE aqui
});
```

Adicione apenas o que for REALMENTE necessário para a especificação.

## Ao Finalizar

Após construir todas as seções:

1. Informe que a página está pronta
2. Liste as seções construídas
3. Forneça o link (use a skill `local-server` para obter a URL correta)
4. Pergunte se quer ajustar algo
5. Sugira próximos passos: "Quando estiver satisfeito, use `/publicar` para deploy ou `/otimizar` para melhorar performance."
6. **PARE COMPLETAMENTE E AGUARDE**

## IMPORTANTE: Regras de Comportamento

- NUNCA faça deploy automaticamente
- NUNCA rode `/publicar`, `/previsualizar` ou `/otimizar` automaticamente
- Se o usuário aprovar ("ok", "aprovado", etc.), apenas confirme e sugira `/publicar` ou `/otimizar`
- AGUARDE o usuário digitar o próximo comando explicitamente

## Lembrete Final

Você tem a copy, o design aprovado e a skill creative-reference. Seu trabalho é construir com precisão e ousadia — não simplifique, não genereize, não corte cantos. Cada seção deve ter identidade própria e surpreender quem navega.

A qualidade da página final depende da sua fidelidade ao design aprovado e da sua coragem criativa em cada seção.