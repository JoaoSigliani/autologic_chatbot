# 🤖 Assistente Virtual com n8n + Dialogflow

Este projeto consiste em um assistente virtual criado no **Dialogflow ES** e integrado a um fluxo automatizado no **n8n**, responsável por processamento de dados, uso de modelos LLM e retorno dinâmico ao usuário.

A comunicação entre o Dialogflow e o n8n é feita via **Webhook HTTP**, com um túnel seguro usando **ngrok**, permitindo rodar toda a automação localmente.

---

## Tecnologias utilizadas

| Tecnologia | Função |
|------------|--------|
| **Dialogflow (ES)** | Criação do chatbot e gerenciamento da conversa |
| **n8n** | Orquestração, processamento, chamadas à API e lógica |
| **ngrok** | Disponibilização do webhook público |
| **Node / JS** | Processamento e formatação dos dados |
| **Gemini API** | Envio dos dados ao Gemini para gerar as respostas |

---

## Arquitetura do fluxo

1. O usuário envia uma mensagem ao bot no Dialogflow  
2. O Dialogflow aciona o webhook
3. O n8n recebe os dados, processa e envia a mensagem para uma LLM
4. A resposta é formatada e enviada de volta ao Dialogflow
5. O usuário visualiza a resposta no chat

---

## Como executar o projeto

### 1. Inicializando o n8n e importando o workflow
- Inicialize o n8n no terminal com o comando ```n8n start```
- Crie um novo workflow
- Nas opções, clique em '***import from file***'
- Importe o arquivo ```Autologic.json``` disponibilizado neste repositório
- No nó ***Gemini Chat Model***, atualize a key do Gemini API para uma gerada recentemente

### 2. Criando túnel http com ngrok
- No terminal do ngrok, digite o comando ```ngrok http 5678```
- Em ***Forwarding***, o https gerado é o túnel que leva ao n8n inicializado no localhost

### 3. Configurando webhook no Dialogflow
- Crie um novo agente
- Em ***Fullfillment -> Webhook*** ative o webhook e cole a URL do túnel criado pelo ngrok
- Ao final da URL adicione ```/webhook/Autologic```
- Para cada intent, apague todas as respostas e clique em ***Enable webhook call for this intent***

### 4. Utilizando o chatbot
- Digite o prompt desejado no chat do Dialogflow
- Observe a resposta =)
