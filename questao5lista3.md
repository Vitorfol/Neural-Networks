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

Ao escolher uma arquitetura para resolver um problema de aprendizado de máquina, é necessário considerar diversos fatores. Não existe uma bala de prata ou um modelo universal que seja sempre a melhor escolha. O primeiro ponto a ser analisado é o próprio problema e a estrutura do dado. A partir disso, é possível restringir a família de modelos mais adequada e começar um direcionamento técnico mais coerente.

A estrutura do dado é fundamental porque diferentes tipos de entrada exigem diferentes formas de modelagem. Dados sequenciais, como textos, áudio, séries temporais e vídeos, possuem dependência de ordem; nesse caso, arquiteturas como RNN, LSTM, GRU e Transformers fazem sentido. Por outro lado, para dados sem estrutura sequencial clara, outras famílias de modelos podem ser mais adequadas. Portanto, antes de escolher uma arquitetura, é necessário entender o formato do dado, sua organização e o tipo de padrão que se espera aprender.

O tamanho da base também influencia diretamente a escolha. Modelos mais complexos, com muitos parâmetros, tendem a precisar de mais dados para generalizar bem. Se a base for pequena, uma arquitetura muito grande pode decorar os exemplos de treino e sofrer overfitting. Já bases maiores permitem treinar modelos mais robustos, embora também aumentem o custo computacional. Por isso, a escolha do modelo deve considerar tanto a quantidade de exemplos quanto a diversidade dos dados.

O tamanho médio das sequências é outro fator importante. Sequências curtas, como mensagens SMS, normalmente possuem padrões mais diretos e podem ser bem modeladas por arquiteturas mais leves, como GRU. Sequências longas, como reviews de filmes, exigem maior capacidade de manter informação ao longo do tempo, favorecendo arquiteturas como LSTM ou Transformers. Além disso, quanto maior a sequência, maior tende a ser o custo de processamento, a necessidade de memória e o risco de truncar informações relevantes.

A necessidade de modelar dependências longas também deve orientar a escolha. Em alguns problemas, a informação relevante está concentrada em poucas palavras ou em trechos próximos. Em outros, o significado depende da relação entre partes distantes do texto, como ocorre em reviews com contraste, negação ou mudança de opinião ao longo da avaliação. Nesses casos, modelos mais simples podem não ser suficientes, e arquiteturas com maior capacidade contextual passam a fazer mais sentido.

O custo de treinamento é um fator prático que não pode ser ignorado. Modelos maiores exigem mais tempo, mais memória e, muitas vezes, hardware especializado. Não faz sentido escolher um Transformer grande se o problema pode ser resolvido adequadamente por uma GRU consumindo uma fração do poder computacional. Por outro lado, também não faz sentido insistir em um modelo simples quando ele claramente não tem capacidade para capturar os padrões necessários. A decisão deve equilibrar desempenho e viabilidade.

O custo de inferência também precisa ser considerado, principalmente em aplicações reais. Após o treinamento, o modelo pode precisar responder rapidamente, processar muitos exemplos por segundo ou rodar em ambientes com poucos recursos. Nesse caso, uma arquitetura mais leve pode ser preferível mesmo que tenha desempenho um pouco menor. A melhor escolha depende não apenas da métrica final, mas também de como o modelo será usado.

A interpretabilidade é outro ponto relevante. Modelos mais complexos, como Transformers, podem atingir melhores resultados, mas tendem a ser mais difíceis de interpretar. Em contextos nos quais é necessário justificar decisões, auditar erros ou explicar previsões, essa dificuldade pode pesar contra modelos muito complexos. Assim, dependendo do objetivo do projeto, um modelo mais simples e mais interpretável pode ser mais adequado.

A disponibilidade de modelos pré-treinados também altera a decisão. Quando existe um modelo pré-treinado adequado ao domínio, como o DistilBERT para tarefas de linguagem natural, é possível aproveitar representações já aprendidas em grandes bases textuais. Isso pode melhorar o desempenho e reduzir a necessidade de treinar tudo do zero. Entretanto, esse ganho vem acompanhado de maior custo computacional e maior complexidade de uso.

O risco de overfitting deve ser avaliado em conjunto com a complexidade da arquitetura. Modelos muito simples podem sofrer underfitting, como observado na configuração mais simples da LSTM, enquanto modelos muito complexos podem se ajustar demais aos dados de treino e perder capacidade de generalização. O cientista de dados precisa observar métricas de treino, validação e teste para entender se o modelo está aprendendo de fato ou apenas memorizando padrões.

Por fim, o objetivo do projeto deve orientar toda a escolha. O modelo é apenas um mecanismo para resolver um problema. Se o objetivo é obter máxima qualidade e há recursos computacionais suficientes, uma arquitetura mais complexa pode ser justificada. Se o objetivo é eficiência, baixo custo, simplicidade de implantação ou resposta rápida, modelos mais leves podem ser preferíveis.

Assim, não faz sentido escolher uma arquitetura apenas por ser mais moderna ou mais complexa. A escolha deve partir do problema, dos dados, das restrições práticas e do objetivo final. Todo modelo possui trade-offs, e não há uma solução universal em redes neurais ou em inteligência artificial. O papel do cientista de dados é justamente entender esses trade-offs e selecionar a arquitetura mais adequada para o contexto.
