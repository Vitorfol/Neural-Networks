# Questão 5: Escolha de arquitetura para dados sequenciais em Ciência de Dados

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

Em textos mais longos, LSTMs tendem a apresentar desempenho superior às RNNs simples. Isso ocorre porque RNNs tradicionais têm dificuldade em manter informação relevante por muitos passos temporais, principalmente devido ao problema do desaparecimento do gradiente. Como consequência, relações semânticas distantes no texto podem deixar de influenciar corretamente a decisão final do modelo.

A LSTM surge justamente como uma evolução das RNNs para lidar melhor com esse tipo de problema. Por meio de portas de controle e de uma célula de memória, ela consegue decidir quais informações devem ser mantidas, esquecidas ou atualizadas ao longo da sequência. Assim, torna-se mais adequada para tarefas com textos longos, como reviews de filmes, em que a opinião final pode depender de informações distribuídas ao longo de várias frases.

O principal trade-off é o custo computacional. LSTMs possuem mais parâmetros e operações internas do que RNNs simples, tornando o treinamento e a inferência mais custosos. Portanto, a LSTM tende a ser mais robusta em textos longos, mas cobra mais processamento.

---

### LSTM vs GRU em desempenho, custo e número de parâmetros

A LSTM e a GRU foram criadas para lidar melhor com dependências temporais do que a RNN simples, mas fazem isso com estruturas internas diferentes. A LSTM utiliza três portas principais e uma célula de memória separada, o que dá maior controle sobre o fluxo de informação. A GRU, por outro lado, simplifica essa estrutura ao usar menos portas e ao não manter uma célula de memória separada.

Na prática, isso faz com que a GRU tenha menor número de parâmetros e menor custo computacional em relação à LSTM. Por ser mais simples, ela costuma treinar mais rápido e exigir menos recursos. Ainda assim, em muitas tarefas, principalmente com sequências curtas ou moderadas, a GRU pode atingir desempenho semelhante ao da LSTM.

A LSTM pode ser mais vantajosa quando o problema exige maior capacidade de modelagem, especialmente em sequências longas e com dependências mais complexas. Já a GRU tende a ser uma boa escolha quando se busca equilíbrio entre desempenho e eficiência computacional.

---

### GRU em mensagens curtas versus LSTM em reviews longas

Nas questões anteriores, a GRU foi aplicada à detecção de spam em mensagens SMS, enquanto a LSTM foi aplicada à classificação de sentimento em reviews do IMDb. Esses dois cenários representam bem o tipo de problema em que cada arquitetura tende a ser mais adequada.

Mensagens SMS são geralmente curtas, objetivas e possuem padrões mais diretos, como links, números, termos promocionais, urgência ou palavras típicas de spam. Nesse contexto, a GRU é uma boa escolha porque consegue capturar dependências temporais relevantes com menor custo computacional. Como as sequências são menores, nem sempre é necessário usar uma arquitetura mais pesada como a LSTM.

Já reviews de filmes costumam ser mais longas e podem conter opiniões misturadas, mudanças de tom, negações, contraste entre aspectos positivos e negativos e dependências semânticas mais distantes. Nesse cenário, a LSTM tende a ser mais apropriada, pois sua célula de memória e seus portões ajudam a manter informações relevantes ao longo de uma sequência maior.

Nos experimentos, ambas as abordagens foram adequadas aos seus respectivos problemas. A GRU apresentou bom desempenho na tarefa de spam, enquanto a LSTM precisou de uma configuração mais robusta para lidar melhor com a complexidade das reviews. A configuração mais simples da LSTM apresentou sinais de underfitting, o que reforça que textos longos exigem maior capacidade de modelagem.

---

### Modelos recorrentes treinados do zero versus Transformer pré-treinado

Modelos recorrentes, como RNN, LSTM e GRU, foram treinados do zero nos experimentos. Isso significa que seus embeddings e seus pesos internos foram aprendidos diretamente a partir das bases utilizadas em cada questão. Essa abordagem é mais simples de implementar, mais barata computacionalmente e viável em máquinas comuns, principalmente quando se usam modelos pequenos e bases de tamanho moderado.

Transformers, por outro lado, geralmente possuem número muito maior de parâmetros e são mais caros para treinar do zero. Na prática, treinar um Transformer grande desde o início exige grande volume de dados, hardware especializado e muito tempo de processamento. Por isso, em aplicações reais, é comum utilizar Transformers pré-treinados, como o DistilBERT, e apenas ajustá-los à tarefa específica por meio de fine-tuning ou extração de representações.

A vantagem do Transformer pré-treinado é que ele já carrega conhecimento linguístico aprendido em grandes corpora de texto. Isso tende a melhorar o desempenho, especialmente quando a base específica da tarefa não é muito grande. A desvantagem é o maior custo computacional, tanto no treinamento quanto na inferência, além de maior complexidade de implementação em relação aos modelos recorrentes.

Assim, modelos recorrentes treinados do zero são mais simples, leves e controláveis, enquanto Transformers pré-treinados tendem a entregar melhor desempenho, mas com maior custo e dependência de modelos previamente treinados.

---

### Custo computacional em treinamento e inferência

O custo computacional de treinamento tende a ser maior do que o custo de inferência. Durante o treinamento, o modelo precisa processar os dados, calcular a loss, executar o backpropagation, atualizar pesos e repetir esse processo por várias épocas. Esse ciclo envolve muitas operações matemáticas e pode ser bastante custoso, principalmente em modelos com muitos parâmetros.

Na inferência, por outro lado, os pesos já estão aprendidos. O modelo apenas recebe uma entrada e produz uma previsão. Por isso, inferir costuma ser mais barato do que treinar. Mesmo assim, o custo de inferência ainda depende da arquitetura escolhida. Uma RNN simples ou uma GRU pequena tende a ser mais leve do que uma LSTM grande ou um Transformer.

Entre as arquiteturas comparadas, a RNN simples tende a ter o menor custo, seguida pela GRU, depois pela LSTM, e por fim pelo DistilBERT. O DistilBERT é mais leve que o BERT original, mas ainda é mais pesado que os modelos recorrentes utilizados nas demais questões. Assim, a escolha do modelo deve considerar não apenas a qualidade das métricas, mas também o tempo de treinamento, o tempo de resposta em produção e os recursos computacionais disponíveis.

---

### Impacto da tokenização e do tamanho das sequências

A tokenização e o tamanho das sequências têm impacto direto no desempenho e no custo dos modelos. Antes de processar texto, é necessário transformar palavras, subpalavras ou caracteres em representações numéricas. Nos modelos recorrentes, geralmente se constrói um vocabulário próprio a partir da base e cada texto é convertido em uma sequência de índices. Já em Transformers pré-treinados, como o DistilBERT, utiliza-se o tokenizer do próprio modelo, normalmente baseado em subpalavras.

O tamanho da sequência também é uma decisão importante. Sequências muito curtas podem perder informação relevante caso o texto seja truncado. Por outro lado, sequências muito longas aumentam o custo computacional, exigem mais memória e podem dificultar o treinamento. Por isso, normalmente é necessário escolher um limite máximo de tokens ou palavras, equilibrando cobertura dos exemplos e viabilidade computacional.

O padding também entra nesse processo, pois textos menores precisam ser preenchidos para formar batches com tamanho uniforme. No entanto, muito padding pode gerar desperdício computacional, já que o modelo passa a processar posições que não carregam informação real. Em Transformers, as attention masks ajudam a indicar quais posições são tokens reais e quais são padding, evitando que o modelo use essas posições artificiais no mecanismo de atenção.

Portanto, tokenização, padding, truncamento e tamanho máximo da sequência não são apenas detalhes de pré-processamento. Essas escolhas afetam diretamente o custo, a qualidade do aprendizado e a capacidade do modelo de aproveitar corretamente a informação presente no texto.

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
