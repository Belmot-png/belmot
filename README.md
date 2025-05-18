# PROMPT CREATOR v2.0

**Autor:** Leoni Santos "Belmot"

**Data:** Maio de 2025 (Conforme código fonte)

**Versão:** 2.0

## Descrição

O **PROMPT CREATOR** é um assistente inteligente implementado em Python, projetado para auxiliar usuários na criação e refinamento de prompts para geração de imagem e texto utilizando a API do Google Gemini. Ele guia o usuário através de um processo iterativo, transformando ideias iniciais em prompts detalhados, claros e eficazes, prontos para serem usados com modelos de IA generativa. Ao final do processo, o prompt refinado em português é também traduzido para o inglês.

Este projeto utiliza o Google AI Developer Kit (ADK) para a interação com o agente especializado em engenharia de prompts e a biblioteca `google-generativeai` para a tradução final.

## Funcionalidades Principais

*   **Criação Iterativa de Prompts:** Interage com o usuário para refinar progressivamente a ideia do prompt.
*   **Suporte para Imagem e Texto:** Gera prompts otimizados tanto para geração de imagens quanto para geração de texto.
*   **Engenharia de Prompt Inteligente:** O agente "PromptEngineerPro" aplica heurísticas e faz perguntas relevantes para melhorar a qualidade do prompt, considerando:
    *   **Para Imagens:** Sujeito, cenário, composição, estilo artístico, iluminação, atmosfera, paleta de cores, nível de detalhe e parâmetros específicos.
    *   **Para Texto:** Objetivo, verbo de ação, tópico, formato, público-alvo, tom, informações essenciais, comprimento e estrutura.
*   **Tradução Automática:** Após o refinamento, o prompt final em português é traduzido para o inglês.
*   **Interface de Linha de Comando:** Interação amigável via console.

## Pré-requisitos

*   Python 3.x
*   Uma chave de API do Google Gemini.
*   As seguintes bibliotecas Python (instaladas automaticamente se executado em um ambiente como Google Colab que suporte `!pip`):
    *   `google-generativeai`
    *   `google-adk`
    *   (Outras dependências padrão como `os`, `sys`, `re`, `textwrap`, `IPython`)

## Configuração

1.  **Obtenha uma Chave de API do Google Gemini:**
    *   Acesse o [Google AI Studio](https://aistudio.google.com/) (ou o portal relevante do Google Cloud) para gerar sua chave de API.

2.  **Configure a Chave de API no Ambiente:**
    *   **Google Colab (Recomendado para este script):**
        *   No painel à esquerda, clique no ícone de chave ("Secrets").
        *   Crie um novo secret chamado `GOOGLE_API_KEY`.
        *   Cole sua chave de API no campo "Value".
        *   Certifique-se de que o acesso ao notebook está habilitado para este secret.
    *   **Ambiente Local (Alternativo):**
        *   Você pode definir a chave como uma variável de ambiente chamada `GOOGLE_API_KEY`. O script tentará lê-la se não encontrar no Colab Secrets.

3.  **Modelos Utilizados (Maio de 2025, conforme código):**
    *   **Agente ADK:** `gemini-2.0-flash`
    *   **Tradução:** `gemini-2.0-flash`
    *   *Nota: Se esses modelos não estiverem disponíveis ou você desejar usar outros, modifique as variáveis `ADK_MODEL_ID` e `TRANSLATION_MODEL_ID` no script.*

## Como Usar

1.  **Execute o script Python (`PROMPT_CREATOR.txt` ou renomeado para `.py`).**
    *   Se estiver no Google Colab, abra o arquivo `.ipynb` ou cole o conteúdo do script em uma célula de código.
2.  O script primeiramente instalará as dependências necessárias (se executado em um ambiente que suporte `!pip`).
3.  Ele solicitará sua chave de API do Google Gemini (se não configurada via Colab Secrets ou variáveis de ambiente, embora a versão atual priorize Colab Secrets).
4.  Você será perguntado se deseja criar um prompt para **IMAGEM** ou **TEXTO**.
5.  Em seguida, forneça sua ideia inicial para o prompt.
6.  O "Prompt Engineer Pro" apresentará uma primeira versão do prompt ("**Prompt Revisado**") e algumas perguntas ("**Perguntas**") para ajudar a refinar sua ideia.
7.  Responda às perguntas ou forneça feedback adicional.
8.  O processo se repete: o prompt é revisado e novas perguntas são feitas.
9.  Quando estiver satisfeito com o "Prompt Revisado", digite `fim` em vez de responder às perguntas.
10. O script exibirá o seu prompt finalizado em português e, em seguida, a versão traduzida para o inglês.

## Estrutura do Código

*   **SETUP INICIAL:** Instalação de bibliotecas e importações.
*   **CONFIGURAÇÃO DA API KEY:** Carregamento seguro da chave de API.
*   **Definição de Modelos:** Especificação dos modelos Gemini a serem usados.
*   **FUNÇÃO CALL_AGENT:** Função auxiliar para interagir com o agente ADK.
*   **FUNÇÕES DE EXIBIÇÃO E EXTRAÇÃO:** Utilitários para formatar a saída e extrair seções da resposta do agente.
*   **INSTRUÇÕES PARA O AGENTE:** O "system prompt" detalhado que define o comportamento do "PromptEngineerPro".
*   **CRIAÇÃO DO AGENTE:** Instanciação do agente ADK.
*   **LOOP DE INTERAÇÃO PRINCIPAL:**
    *   Coleta a intenção inicial do usuário.
    *   Entra em um loop iterativo:
        *   Envia o contexto e a resposta do usuário para o agente.
        *   Recebe e exibe o prompt revisado e novas perguntas.
        *   Coleta o feedback do usuário.
    *   Ao finalizar (`fim`):
        *   Exibe o prompt final em português.
        *   Realiza a tradução para o inglês usando o modelo Gemini diretamente.
        *   Exibe o prompt traduzido.

## Limitações e Pontos de Atenção

*   A qualidade da engenharia de prompt e da tradução depende da capacidade dos modelos Gemini especificados (`ADK_MODEL_ID`, `TRANSLATION_MODEL_ID`).
*   O modelo `gemini-2.0-flash` é referenciado para Maio de 2025. Verifique a disponibilidade e os nomes dos modelos atuais se estiver usando em uma data diferente.
*   O script assume execução em um ambiente como Google Colab para o gerenciamento de secrets e instalação de pacotes via `!pip`. Adaptações podem ser necessárias para outros ambientes.
*   A conexão com a internet é necessária para acessar a API do Google Gemini.

## Como Contribuir (Exemplo)

Se você deseja contribuir com este projeto, sinta-se à vontade para:
1.  Fazer um "Fork" do repositório.
2.  Criar uma nova "branch" para sua feature (`git checkout -b feature/MinhaNovaFeature`).
3.  Fazer "commit" das suas alterações (`git commit -am 'Adiciona MinhaNovaFeature'`).
4.  Fazer "push" para a branch (`git push origin feature/MinhaNovaFeature`).
5.  Abrir um "Pull Request".

## Licença (Exemplo)

Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
(Se você não tiver um arquivo LICENSE, pode adicionar um ou escolher uma licença apropriada.)

---
