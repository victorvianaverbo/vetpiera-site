# Funil de Vendas com IA

Framework para criar landing pages unicas com HTML, CSS e JavaScript puros. Sem npm, node ou webpack. Infraestrutura 100% Netlify.

---

## Comandos

### Fluxo Principal

```
/descoberta → /pesquisa-mercado → /narrativa → /gerar-copy → /gerar-design → /desenvolver → /publicar
```

> Se voce ja tem um produto definido, pode pular direto para `/pesquisa-mercado`.

| Comando | O que faz |
|---------|-----------|
| `/inicio` | Boas-vindas e orientacao para o primeiro passo |
| `/descoberta` | Descobre o produto ideal com base em paixoes, habilidades e dores do aluno |
| `/pesquisa-mercado` | Pesquisa concorrentes, dores do publico e refina a oferta |
| `/narrativa` | Constroi identidade do comunicador, analisa players e cria a big idea |
| `/gerar-copy` | Cria os textos persuasivos da pagina de vendas |
| `/gerar-design` | Define identidade visual, cria Hero + 1 secao de amostra |
| `/desenvolver` | Constroi a pagina completa com todas as secoes |
| `/publicar` | Deploy para producao via Netlify |

### Auxiliares

| Comando | O que faz |
|---------|-----------|
| `/visualizar-local` | Servidor local na porta 8888 |
| `/otimizar` | Auditoria e correcoes de performance |
| `/previsualizar` | Deploy Preview via Pull Request |
| `/debug` | Investiga e resolve erros |

---

## Inicio Rapido

Abra no Google Antigravity e use `/inicio` para comecar.

---

## Estrutura do Projeto

```
meu-projeto/
├── pagina-vendas/        # Cada pagina tem sua pasta
│   ├── index.html
│   ├── style.css
│   ├── script.js
│   └── copy.md           # Textos gerados
├── pagina-obrigado/      # Outras paginas
├── netlify.toml
└── .agent/               # Configuracoes do framework
```

---

## Versoes Alternativas

Ao pedir uma nova versao da pagina, a versao atual vai para `_backup_v1/` e a nova e criada na raiz. Versoes anteriores ficam preservadas.

---

## Estrutura gerada pelo fluxo

```
meu-projeto/
├── produto/
│   ├── descoberta.md         # Produto e avatar definidos
│   ├── pesquisa-mercado.md   # Analise de concorrentes e mercado
│   └── narrativa.md          # Big idea e posicionamento
├── pagina-vendas/
│   ├── index.html
│   ├── style.css
│   └── copy.md
├── netlify.toml
└── .agent/
```

---

## Requisitos

- Google Antigravity (gratis)
- Netlify CLI (`npm install -g netlify-cli`)
- Conta Netlify (gratis)
