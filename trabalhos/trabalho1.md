# Atividade 2 - Desenvolvimento de Modelos (MLP, CNN, GAN e GNN)

## Instruções Gerais
- Implementar em Python (PyTorch ou TensorFlow/Keras).
- Cada experimento deve conter: Descrição, Preparação, Arquitetura, Configuração, Métricas e Análise Crítica.
- Comparar pelo menos duas configurações por modelo.
- Incluir divisão de dados e gráficos de treino.

---

## Questão 1: MLP - Breast Cancer Wisconsin
**Objetivo:** Apoiar a classificação de tumores benignos ou malignos.
- **Base:** Breast Cancer Wisconsin (UCI ou Scikit-learn).
- **Entregáveis:** Pré-processamento (padronização), arquitetura (camadas/ativação), métricas (acurácia, precisão, recall, F1, matriz de confusão) e análise crítica (por que MLP? Por que métricas além da acurácia?).

## Questão 2: CNN - Fashion-MNIST
**Objetivo:** Automatizar classificação de vestuário.
- **Base:** Fashion-MNIST.
- **Entregáveis:** Normalização, arquitetura CNN (conv, pooling, FC), avaliação com erros/acertos e discussão sobre filtros, pooling e pesos compartilhados.

## Questão 3: GAN - MNIST
**Objetivo:** Gerar novas amostras plausíveis (não classificar).
- **Base:** MNIST.
- **Entregáveis:** Gerador, discriminador, vetor latente, registro de amostras em diferentes épocas (início/meio/fim) e discussão sobre instabilidade/mode collapse.

## Questão 4: GNN - Cora
**Objetivo:** Classificar artigos científicos em rede de citações.
- **Base:** Cora (PyTorch Geometric ou DGL).
- **Entregáveis:** Definição de nós/arestas, explicação de X, A e embeddings, implementação de GCN e discussão sobre propagação de informação entre vizinhos.

## Questão 5: Escolha de Arquitetura
**Objetivo:** Reflexão sobre a prática do cientista de dados.
- **Tarefas:** Comparativos (MLP vs CNN; CNN vs GAN; MLP vs GNN) e discussão sobre custo computacional, interpretabilidade e estrutura do dado.