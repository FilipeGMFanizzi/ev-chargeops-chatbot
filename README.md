# EV ChargeOps Assistant

Projeto desenvolvido para o EV Challenge 2026, parceria FIAP e GoodWe.

## Integrantes

[João] - RM: 571355	
[Filipe] - RM: 571131
[Guilherme] - RM: 572957
[Enzo] - RM: 572037
[David] - RM: 574147
[Lucas] - RM: 573497

Problema

Condomínios que instalam eletropostos GoodWe acabam enfrentando vários problemas no dia a dia. Quando muitos moradores tentam carregar o carro ao mesmo tempo, a rede elétrica do prédio pode sobrecarregar. Além disso, não existe um jeito simples de saber quem usou qual estação e quanto cada um gastou, então o síndico precisa fazer tudo no manual, o que gera confusão na hora de dividir a conta de luz.

Fora isso, quando algo dá errado com uma estação, o morador não tem nenhum canal rápido para tirar dúvida ou reportar o problema.

O que o chatbot faz?

O ChargeOps Assistant é um chatbot com inteligência artificial feito para ajudar as pessoas que vivem ou trabalham em condomínios com eletropostos GoodWe. A ideia é ter um assistente que responde perguntas, ajuda a agendar recargas, mostra o consumo de cada morador e orienta em caso de falha no equipamento.

O chatbot atende três tipos de usuário. O morador que quer saber se tem estação livre, agendar um horário ou ver quanto gastou no mês. O síndico que precisa de relatórios de consumo, quer configurar limites de potência ou entender como funciona o faturamento. E o técnico de manutenção que precisa de informações sobre falhas e procedimentos para resolver problemas nos equipamentos.

Tecnologias escolhidas

O modelo de linguagem escolhido foi o GPT-4o da OpenAI. A escolha foi por ele ter um desempenho muito bom em português e conseguir manter o contexto da conversa por bastante tempo, o que é importante porque os usuários podem fazer perguntas em sequência e o chatbot precisa lembrar o que foi dito antes.

Para orquestrar as chamadas ao modelo e guardar o histórico da conversa, vamos usar o LangChain. Ele facilita bastante o trabalho de passar o contexto certo para o modelo a cada mensagem.

O backend vai ser feito em Python com FastAPI, que é leve e fácil de integrar com as bibliotecas de IA. O histórico das conversas vai ficar salvo no PostgreSQL e o contexto de cada sessão ativa vai ficar no Redis para ser recuperado rápido.

A interface do chat vai ser feita em React, pensando em um componente que possa ser embutido no portal do condomínio.

Fluxograma

Ver arquivo fluxograma_chargebot.png na raiz do repositório.

Modelo de teste

Ver arquivo modelo_de_teste.md na raiz do repositório.

System prompt

Ver arquivo system_prompt.md na raiz do repositório.

Estrutura do repositório

```
ev-chargeops-chatbot/
    README.md
    system_prompt.md
    modelo_de_teste.md
    fluxograma_chargebot.png
    docs/
        arquitetura.md
        personas.md
```
