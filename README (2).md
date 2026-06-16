# EV ChargeOps Assistant

Projeto desenvolvido para o EV Challenge 2026, parceria FIAP e GoodWe.

## Integrantes

[João] - RM: 571355
[Filipe] - RM: 571131
[Guilherme] - RM: 572957
[Enzo] - RM: 572037
[David] - RM: 574147
[Lucas] - RM: 573497

## Problema

Condomínios que instalam eletropostos GoodWe acabam enfrentando vários problemas no dia a dia. Quando muitos moradores tentam carregar o carro ao mesmo tempo, a rede elétrica do prédio pode sobrecarregar. Além disso, não existe um jeito simples de saber quem usou qual estação e quanto cada um gastou, então o síndico precisa fazer tudo no manual, o que gera confusão na hora de dividir a conta de luz.

Fora isso, quando algo dá errado com uma estação, o morador não tem nenhum canal rápido para tirar dúvida ou reportar o problema.

## O que o chatbot faz?

O ChargeOps Assistant é um chatbot com inteligência artificial feito para ajudar as pessoas que vivem ou trabalham em condomínios com eletropostos GoodWe. A ideia é ter um assistente que responde perguntas, ajuda a agendar recargas, mostra o consumo de cada morador e orienta em caso de falha no equipamento.

O chatbot atende três tipos de usuário. O morador que quer saber se tem estação livre, agendar um horário ou ver quanto gastou no mês. O síndico que precisa de relatórios de consumo, quer configurar limites de potência ou entender como funciona o faturamento. E o técnico de manutenção que precisa de informações sobre falhas e procedimentos para resolver problemas nos equipamentos.

## Tecnologias

Na Sprint 1 a ideia era usar o GPT-4o da OpenAI. Na Sprint 2, como não tínhamos créditos na OpenAI, trocamos para o Llama 3.3 70B rodando no Groq, que tem um tier gratuito e era uma das opções permitidas pela tarefa ("Llama, OpenAI, Gemini ou outra"). O Llama responde muito bem em português, mantém o contexto da conversa e a qualidade é comparável à do GPT-4o para o nosso caso.

A API do Groq é compatível com o SDK da OpenAI, então usamos a mesma biblioteca `openai`, só mudando a base_url e a chave. Isso facilita trocar de modelo no futuro sem reescrever o código.

Na Sprint 2 implementamos um protótipo funcional em Python que já roda no Google Colab. Ele injeta o system prompt com o contexto da GoodWe, guarda o histórico da conversa (numa lista de mensagens que é enviada ao modelo a cada pergunta) e responde com base nos dados de recarga. Os dados da GoodWe estão simulados no código, já que ainda não temos acesso à API real.

A arquitetura completa para a versão de produção (backend em FastAPI, histórico no PostgreSQL, cache de sessão no Redis, orquestração com LangChain e interface em React embutida no portal do condomínio) é o plano futuro do projeto. Para o protótipo desta sprint usamos só o necessário para o chatbot conversar de forma coerente.

## Como executar

### No Google Colab (recomendado)

1. Abra um novo notebook no Google Colab.
2. Instale a biblioteca da OpenAI numa célula:
   ```
   !pip install openai
   ```
3. Adicione sua chave do Groq nos **Secrets** do Colab (ícone de chave na barra lateral), com o nome `GROQ_API_KEY`. Não escreva a chave direto no código.
4. Cole o conteúdo do `chatbot.py` numa célula e rode.
5. Chame `conversar()` para iniciar o chat, ou `rodar_testes()` para rodar os casos de teste de uma vez.

### Em uma IDE (VS Code, PyCharm, etc.)

1. Instale a dependência:
   ```
   pip install openai
   ```
2. Defina a variável de ambiente com sua chave:
   ```
   export GROQ_API_KEY="sua-chave-aqui"      # Linux/Mac
   set GROQ_API_KEY=sua-chave-aqui           # Windows
   ```
3. Rode o arquivo:
   ```
   python chatbot.py
   ```

## Dependências

- Python 3.10 ou superior
- biblioteca `openai`

## Variáveis de ambiente

- `GROQ_API_KEY` - chave de acesso à API do Groq. No Colab, vai nos Secrets; fora do Colab, na variável de ambiente. A chave nunca aparece no código nem no repositório.

## Exemplo de uso

```
Você: oi, tem alguma estação livre agora?
Assistente: No momento temos duas estações disponíveis: a CHR-001 e a CHR-004.
A CHR-002 está em uso (deve liberar por volta das 19:45) e a CHR-003 está fora
do ar por uma falha. Quer iniciar uma recarga agora ou prefere agendar um horário?

Você: quanto vou pagar esse mês? sou do apto 202
Assistente: Em maio o apto 202 consumiu 31,1 kWh no total...
(o chatbot mostra a conta separando pico e fora de pico e dá uma dica de economia)
```

## Estrutura do repositório

```
ev-chargeops-chatbot/
    README.md
    chatbot.py
    system_prompt.md
    modelo_de_teste.md
    resultados_testes.md
    fluxograma_chargebot.png
```
