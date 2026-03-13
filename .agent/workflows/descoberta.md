---
description: descoberta
---

# Instruções

Você vai ajudar o aluno a descobrir qual produto digital ele vai criar e vender.

## ESCOPO DESTE WORKFLOW

Este workflow APENAS:
- Investiga paixões, habilidades e dores do aluno
- Ajuda a identificar o produto com maior potencial
- Orienta sobre boas práticas de infoproduto
- Salva o resultado em `descoberta.md`

Este workflow NÃO:
- Pesquisa mercado ou concorrentes
- Cria copy ou design
- Executa nenhuma etapa seguinte

## Antes de Começar

Crie uma pasta chamada `produto` na raiz do projeto. Todos os arquivos do processo ficarão dentro dela:

```
projeto/
├── produto/
│   ├── descoberta.md       ← será criado agora
│   ├── pesquisa-mercado.md ← será criado em /pesquisa-mercado
│   └── narrativa.md        ← será criado em /narrativa
└── .agent/
```

## Processo de Descoberta

### Fase 1: Mapeamento

Faça as perguntas abaixo **uma de cada vez**, aguardando a resposta do aluno antes de fazer a próxima:

1. "O que você sabe fazer bem, mesmo que pareça óbvio pra você? Pode ser profissional, hobby, algo que amigos sempre te pedem ajuda."
2. "Quais resultados você já conquistou na vida que outras pessoas gostariam de conquistar também?"
3. "Qual dor ou problema você já passou e superou? Algo que, olhando para trás, você gostaria que tivesse um guia para acelerar o processo."
4. "Existe algum assunto que você consegue falar por horas sem se cansar? Algo que você estuda ou acompanha por prazer."

### Fase 2: Filtro de Viabilidade

Com base nas respostas, apresente as 2 ou 3 melhores opções de produto identificadas.

Para cada opção, avalie em voz alta:
- **Demanda:** existe gente pagando por isso hoje?
- **Transformação clara:** dá pra descrever o antes e o depois do aluno?
- **Autoridade mínima:** o aluno tem credibilidade suficiente para ensinar isso?
- **Formato low ticket:** funciona como treinamento de entrada (não exige anos de resultado)?

### Fase 3: Boas Práticas de Infoproduto

Após identificar a opção mais forte, explique brevemente:

- **Nicho vs. mercado:** quanto mais específico, mais fácil de vender. "Como perder peso" perde para "Como emagrecer 5kg em 30 dias sem academia para mulheres acima de 40".
- **Transformação acima de informação:** o aluno compra o resultado, não o conteúdo.
- **Low ticket como porta de entrada:** o objetivo é gerar o primeiro cliente e a primeira prova social, não o maior faturamento imediato.
- **Não precisa ser o maior especialista do mundo:** precisa saber mais que o avatar no momento em que ele está.

### Fase 4: Definição Final

Peça ao aluno para confirmar a escolha. Quando confirmado, registre o produto com:
- **Nome provisório do produto**
- **Avatar:** quem é o cliente ideal (perfil, momento de vida, dor principal)
- **Transformação:** qual é o antes e o depois
- **Formato:** o que será entregue (videoaulas, PDF, mentorias, etc.)

## Saída

Salve o resultado em `produto/descoberta.md`:

```markdown
# Descoberta do Produto

## Produto
Nome: ...

## Avatar
Quem é: ...
Dor principal: ...
Momento de vida: ...

## Transformação
Antes: ...
Depois: ...

## Formato
...

## Observações
...
```

## Ao Finalizar

1. Informe que a descoberta foi salva
2. Mostre um resumo do produto definido
3. Pergunte se quer ajustar algo
4. Sugira a próxima etapa: "Com o produto definido, use `/pesquisa-mercado` para analisarmos o mercado e os concorrentes."
5. **PARE COMPLETAMENTE E AGUARDE**

## IMPORTANTE: Regras de Comportamento

- Faça as perguntas uma de cada vez, não em bloco
- NUNCA assuma o produto antes de ouvir o aluno
- NUNCA avance para pesquisa de mercado automaticamente
- Se o aluno já chegar com um produto definido, pule para a Fase 2 para validar a viabilidade
- AGUARDE o usuário digitar o próximo comando explicitamente
