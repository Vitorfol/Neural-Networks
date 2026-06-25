# Questão 5 — Escolha de arquitetura para dados sequenciais em Ciência de Dados

## a) Comparação entre arquiteturas

| Arquitetura | Base utilizada      | Tipo de dado       | Tarefa principal                    | Força principal                                                                          | Limitação principal                                                                                                 |
| ----------- | ------------------- | ------------------ | ----------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| RNN simples | AG News             | Texto jornalístico | Classificação multiclasse           | Captura dependências temporais em dados sequenciais.                                     | Dificuldade em modelar dependências longas devido ao desaparecimento do gradiente.                                  |
| LSTM        | IMDb                | Reviews longas     | Classificação binária de sentimento | Modela dependências temporais longas por meio de portas de controle e célula de memória. | Maior custo computacional e maior número de parâmetros.                                                             |
| GRU         | SMS Spam Collection | Mensagens curtas   | Detecção de spam                    | Bom equilíbrio entre desempenho e custo computacional, com menos parâmetros que a LSTM.  | Pode apresentar menor capacidade de modelagem em tarefas muito complexas ou com dependências muito longas.          |
| DistilBERT  | SST-2               | Sentenças curtas   | Classificação binária de sentimento | Captura relações contextuais complexas utilizando conhecimento pré-treinado.             | Alto custo computacional quando comparado às arquiteturas recorrentes, apesar de ser mais leve que o BERT original. |

### Discussão

#### RNN simples

A principal contribuição da RNN simples foi introduzir a capacidade de modelar dependências temporais em dados sequenciais, permitindo trabalhar com tarefas envolvendo texto, áudio, vídeo e outras sequências. Apesar de atualmente ser pouco utilizada em aplicações práticas de Processamento de Linguagem Natural, ela foi fundamental para o desenvolvimento das arquiteturas recorrentes mais modernas, como LSTM e GRU. Sua principal limitação é a dificuldade em aprender dependências de longo prazo devido ao problema do desaparecimento do gradiente, o que reduz sua capacidade de capturar relações distantes ao longo da sequência.

---

#### LSTM

A LSTM surgiu como uma evolução das RNNs tradicionais ao introduzir portas de controle e uma célula de memória responsável por armazenar informações relevantes ao longo da sequência. Essa arquitetura permite modelar dependências temporais mais longas e reduzir significativamente o impacto do desaparecimento do gradiente, tornando-a bastante adequada para tarefas envolvendo textos longos, como classificação de reviews. Como contrapartida, sua arquitetura possui maior número de parâmetros e maior custo computacional em relação à GRU, além de ser mais simples arquiteturalmente do que os modelos baseados em Transformer.

---

#### GRU

A GRU simplifica a arquitetura da LSTM ao reduzir o número de portas e eliminar a necessidade de uma célula de memória separada. Como consequência, possui menos parâmetros e menor custo computacional, mantendo desempenho semelhante ao da LSTM em diversas aplicações práticas. Essa característica faz da GRU uma excelente alternativa para problemas envolvendo sequências menores, como mensagens SMS, em que o ganho de desempenho da LSTM nem sempre compensa seu maior custo computacional. Entretanto, por possuir uma arquitetura mais simples, pode apresentar menor capacidade de modelagem em tarefas muito complexas ou que exigem capturar dependências extremamente longas.

---

#### DistilBERT

O DistilBERT é uma versão destilada do BERT baseada na arquitetura Transformer. Sua principal vantagem é aproveitar conhecimento obtido durante o pré-treinamento, permitindo capturar relações contextuais complexas entre palavras utilizando mecanismos de atenção. Além disso, seu processamento é altamente paralelizável, diferentemente das arquiteturas recorrentes. Em geral, apresenta desempenho superior em diversas tarefas de Processamento de Linguagem Natural, especialmente quando há disponibilidade de modelos pré-treinados. Como limitação, continua sendo significativamente mais custoso computacionalmente do que RNN, LSTM e GRU, tanto em treinamento quanto em inferência, embora seja consideravelmente mais leve que o BERT original.

---

## b) Comparação objetiva entre arquiteturas

### RNN simples vs LSTM em textos mais longos

[comparar capacidade de modelar dependências, estabilidade de treinamento, limitação da RNN, vantagem da LSTM]

### LSTM vs GRU em desempenho, custo e número de parâmetros

[comparar complexidade, número de parâmetros, custo computacional e possíveis diferenças de desempenho]

### GRU em mensagens curtas versus LSTM em reviews longas

[explicar por que GRU pode funcionar bem em SMS curtos e por que LSTM pode ser mais adequada em textos longos]

### Modelos recorrentes treinados do zero versus Transformer pré-treinado

[comparar necessidade de dados, custo, qualidade das representações, generalização e uso de conhecimento prévio]

### Custo computacional em treinamento e inferência

[comparar custo relativo entre RNN, LSTM, GRU e DistilBERT]

### Impacto da tokenização e do tamanho das sequências

[explicar como tokenização, padding, truncamento e comprimento médio das sequências afetam desempenho e custo]

---

## c) Escolha da arquitetura sob a perspectiva de um cientista de dados

A escolha da arquitetura deve considerar múltiplos fatores, e não apenas a complexidade do modelo.

### Estrutura do dado

[discutir como a natureza do dado influencia a escolha]

### Tamanho da base

[discutir relação entre tamanho da base e capacidade do modelo]

### Tamanho médio das sequências

[discutir impacto do comprimento das sequências]

### Necessidade de modelar dependências longas

[discutir quando isso é crítico e quais modelos lidam melhor com isso]

### Custo de treinamento

[discutir tempo, memória, hardware e viabilidade prática]

### Custo de inferência

[discutir velocidade de uso em produção]

### Interpretabilidade

[discutir facilidade ou dificuldade de interpretar comportamento do modelo]

### Disponibilidade de modelos pré-treinados

[discutir vantagem prática de aproveitar modelos existentes]

### Risco de overfitting

[discutir relação entre complexidade, tamanho da base e generalização]

### Objetivo do projeto

[discutir como o objetivo final influencia a escolha da arquitetura]

---

## Conclusão

Em síntese, a escolha da arquitetura deve ser guiada pelo tipo de dado, pela tarefa, pelo custo computacional e pelo desempenho necessário no problema. Não faz sentido escolher um modelo apenas por ser mais moderno ou mais complexo, pois arquiteturas mais simples podem ser suficientes e até mais adequadas em cenários com dados curtos, menor custo computacional ou necessidade de implantação mais leve. Por outro lado, modelos mais sofisticados podem ser vantajosos quando o problema exige maior capacidade de representação e modelagem de contexto.
