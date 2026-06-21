# Atividade 3 - Modelagem de Sequências com RNN, LSTM, GRU e Transformer em Ciência de Dados

## Instruções Gerais
- Implementar em Python (preferencialmente PyTorch ou TensorFlow/Keras).
- Cada experimento deve conter: Descrição, Preparação, Arquitetura, Configuração, Métricas e Análise Crítica.
- Seguir as orientações específicas para tarefas de texto (tokenização, vocabulário, padding, truncamento, attention masks).
- Indicar modelo, tokenizer, estratégia de ajuste e custos observados ao utilizar modelos pré-treinados.
- Discutir e interpretar os resultados frente ao contexto prático de negócios apresentado em cada problema.

---

## Questão 1: RNN Simples - AG News
**Objetivo:** Automatizar a classificação de notícias em categorias temáticas para uma empresa de monitoramento de mídia.
- **Base:** AG News Dataset (Hugging Face datasets `ag_news`, TorchText ou Kaggle; permitido subconjunto preservando as 4 classes).
- **Entregáveis:**
  - **Descrição:** Explicação de como o problema de classificação de notícias se encaixa em aprendizado supervisionado de sequências e a adequação da RNN simples frente a uma MLP.
  - **Preparação:** Tokenização, vocabulário, conversão para sequências numéricas, padding, truncamento (limite máximo) e divisão em treino/validação/teste. Explicações teóricas sobre a necessidade de conversão numérica, do padding em batches e a diferença de classificação binária vs. multiclasse.
  - **Arquitetura & Configuração:** RNN simples detalhando vocabulário, embedding, dimensão oculta, camadas, camada de saída, hiperparâmetros (perda, otimizador, épocas, batch size).
  - **Métricas:** Acurácia, precisão, recall, F1-score e matriz de confusão.
  - **Análise Crítica:** Análise de classes fáceis, confusas, causas de erros, sintomas de underfitting/overfitting e as limitações das RNNs simples em sequências longas.

## Questão 2: LSTM - IMDb Movie Reviews
**Objetivo:** Classificar automaticamente avaliações de filmes como positivas ou negativas para uma plataforma de streaming.
- **Base:** IMDb Movie Reviews Dataset (Hugging Face `imdb`, `tensorflow.keras.datasets.imdb` ou Kaggle; permitido subconjunto balanceado).
- **Entregáveis:**
  - **Descrição:** Justificativa da classificação como tarefa de sequência e discussão do papel da ordem das palavras e do desafio de textos longos.
  - **Preparação:** Limpeza opcional, tokenização, vocabulário, mapeamento numérico, comprimento máximo, padding e splits de dados. Explicação sobre o papel de embeddings e do padding.
  - **Arquitetura & Configuração:** LSTM para classificação binária. Comparar pelo menos duas configurações (ex: variação de dropout, de dimensão oculta ou de embeddings) especificando parâmetros (vocabulário, embedding, estados ocultos, camadas LSTM, dropout, saída, perda, otimizador, épocas e batch size).
  - **Métricas:** Acurácia, precisão, recall, F1-score e matriz de confusão para ambas as variações comparativas.
  - **Análise Crítica:** Indicação de qual configuração foi melhor, sintomas de overfitting, avaliação de exemplos corretos e incorretos (analisando causas como negação, contraste, novos termos ou longos textos), vantagens da LSTM vs. RNN, e importância da análise conjunta de métricas.

## Questão 3: GRU - SMS Spam Collection
**Objetivo:** Automatizar a detecção de spam e ham em mensagens SMS curtas.
- **Base:** SMS Spam Collection Dataset (UCI, Kaggle ou Hugging Face).
- **Entregáveis:**
  - **Descrição:** Descrição dos dados de texto curto. Explicação de por que mensagens curtas são tratadas como sequências, diferenças de SMS vs. reviews longas e impacto de desbalanceamento de classes.
  - **Preparação:** Divisão, codificação do target (ham/spam), tokenização, vocabulário, conversão para sequências numéricas, padding e tamanho máximo.
  - **Arquitetura & Configuração:** GRU especificando tamanho do vocabulário, dimensão de embedding, dimensão do estado oculto, número de camadas, dropout, camada final, perda, otimizador, épocas e batch size.
  - **Métricas:** Acurácia, precisão, recall, F1-score e matriz de confusão.
  - **Análise Crítica:** Identificar qual métrica é crucial para spam (impacto de falsos positivos vs. negativos), análise de comportamento sobre desbalanceamento, overfitting, justificativa do uso de GRU em sequências curtas e por que ela é mais simples estruturalmente que a LSTM.

## Questão 4: Transformer - SST-2 (Stanford Sentiment Treebank)
**Objetivo:** Classificar o sentimento de frases curtas usando um modelo Transformer pré-treinado compacto.
- **Base:** SST-2 (Hugging Face `glue` subset `sst2`). Modelo base `distilbert-base-uncased` com cabeça binária (permitido amostragem e poucas épocas).
- **Entregáveis:**
  - **Descrição:** Discussão teórica sobre tokenização por subpalavras, máscaras de atenção (attention masks), truncamento, e as diferenças essenciais na preparação de dados para Transformer vs. recorrentes.
  - **Preparação:** Tokenização com tokenizer original, limites de sequência, aplicação de truncamento e padding, geração de attention masks e divisão de dados.
  - **Arquitetura & Configuração:** Implementação do DistilBERT com cabeça classificadora. Escolher e justificar uma abordagem: Fine-tuning completo vs. Extração de representações (congelamento das camadas do codificador). Parâmetros (modelo, tokenizer, comprimento de sequência, batch size, épocas, learning rate, perda e otimizador).
  - **Métricas:** Acurácia, precisão, recall, F1-score e matriz de confusão.
  - **Análise Crítica:** Vantagens de utilizar pré-treino, custo de hardware, impacto da sequência máxima, limitações e diagnóstico de quando o uso de Transformers pode ser considerado excessivo ou desnecessário.

## Questão 5: Escolha de Arquitetura
**Objetivo:** Simular decisões de modelagem de um cientista de dados avaliando modelos, custos e cenários.
- **Tarefas:**
  - **Tabela de Síntese:** Preencher tabela cruzando: Arquitetura, Base Utilizada, Tipo de Dado, Tarefa Principal, Força Principal e Limitação Principal.
  - **Comparações de Alto Nível:** Discutir objetivamente:
    * RNN simples vs. LSTM em textos mais longos.
    * LSTM vs. GRU (desempenho, custo de treinamento e escala de parâmetros).
    * Cenário GRU em textos curtos vs. LSTM em resenhas longas.
    * Modelos recorrentes treinados do zero vs. representações pré-treinadas de Transformers.
    * Custo computacional geral em treino e inferência.
    * Impacto da tokenização e do comprimento de sequência.
  - **Tomada de Decisão Teórica:** Reflexão sobre a ponderação de fatores: estrutura e tamanho do dado, dependências temporais, custos, interpretabilidade, pré-treino disponível, overfitting e objetivo estratégico. Conclusão apontando por que não se deve decidir arquitetura apenas com base no critério de "novidade".
