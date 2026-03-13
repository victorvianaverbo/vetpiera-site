---
description: publicar
---

# Instrucoes

O usuario quer colocar o site no ar. Antes de comecar, faca o pre-check abaixo. Depois use a skill `deploy` que contem toda a logica necessaria.

## Pre-check: Contas Necessarias

Antes de qualquer coisa, pergunte ao usuario:

"Para publicar o site, voce vai precisar de duas contas gratuitas. Voce ja tem:"

1. **Conta no GitHub** (github.com) — onde o codigo do site fica guardado
2. **Conta no Netlify** (netlify.com) — o servico que deixa o site no ar

Pergunte separadamente:
- "Voce ja tem conta no GitHub?"
- "Voce ja tem conta no Netlify?"

**Se nao tiver alguma das contas:**
- GitHub: "Acesse github.com, clique em 'Sign up' e crie uma conta gratuita. Me avise quando tiver pronto."
- Netlify: "Acesse netlify.com, clique em 'Sign up' e crie uma conta gratuita (pode entrar com o GitHub). Me avise quando tiver pronto."

**So continue apos confirmar que o usuario tem as duas contas.**

## Processo

1. **Leia a skill `deploy`** (`.agent/skills/deploy/SKILL.md`) e siga as instrucoes detalhadas
2. A skill cobre: primeiro deploy, atualizacoes, cenarios A/B/C/D, troubleshooting, e verificacoes pre-deploy

## REGRA DE OURO: Autonomia Total

**VOCE DEVE fazer tudo sozinho. NUNCA peca para o usuario executar comandos manualmente.**

Quando um comando for interativo (como `netlify init`), VOCE deve:
1. Executar o comando
2. Enviar os inputs necessarios para responder aos prompts
3. Continuar ate concluir

Se algo falhar, tente resolver. So peca ajuda ao usuario se realmente nao conseguir resolver sozinho.

## Ao Finalizar

Apos o deploy:

1. Informe que o site esta no ar
2. Forneca o link do site
3. **PARE COMPLETAMENTE E AGUARDE**

## IMPORTANTE: Regras de Comportamento

- Apos o deploy, PARE e aguarde instrucao do usuario
- NUNCA continue fazendo alteracoes automaticamente
- NUNCA rode outros workflows automaticamente
