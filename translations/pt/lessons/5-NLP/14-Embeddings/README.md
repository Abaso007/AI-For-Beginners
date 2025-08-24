<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e40b47ac3fd48f71304ede1474e66293",
  "translation_date": "2025-08-24T08:53:41+00:00",
  "source_file": "lessons/5-NLP/14-Embeddings/README.md",
  "language_code": "pt"
}
-->
# Embeddings

## [Pre-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/114)

Ao treinar classificadores baseados em BoW ou TF/IDF, trabalhávamos com vetores de saco de palavras de alta dimensão com comprimento `vocab_size`, e estávamos a converter explicitamente de vetores de representação posicional de baixa dimensão para uma representação esparsa one-hot. No entanto, esta representação one-hot não é eficiente em termos de memória. Além disso, cada palavra é tratada de forma independente, ou seja, os vetores codificados one-hot não expressam qualquer semelhança semântica entre palavras.

A ideia de **embedding** é representar palavras através de vetores densos de menor dimensão, que de alguma forma refletem o significado semântico de uma palavra. Mais tarde, discutiremos como construir embeddings de palavras significativos, mas, por agora, vamos apenas pensar nos embeddings como uma forma de reduzir a dimensionalidade de um vetor de palavras.

Assim, a camada de embedding receberia uma palavra como entrada e produziria um vetor de saída com o tamanho especificado por `embedding_size`. De certa forma, é muito semelhante a uma camada `Linear`, mas, em vez de receber um vetor codificado one-hot, será capaz de receber um número de palavra como entrada, permitindo-nos evitar a criação de grandes vetores codificados one-hot.

Ao usar uma camada de embedding como a primeira camada na nossa rede de classificação, podemos mudar de um modelo de saco de palavras para um modelo de **embedding bag**, onde primeiro convertemos cada palavra no nosso texto no embedding correspondente e, em seguida, calculamos alguma função agregada sobre todos esses embeddings, como `sum`, `average` ou `max`.

![Imagem mostrando um classificador com embeddings para cinco palavras de sequência.](../../../../../lessons/5-NLP/14-Embeddings/images/embedding-classifier-example.png)

> Imagem do autor

## ✍️ Exercícios: Embeddings

Continue a sua aprendizagem nos seguintes notebooks:
* [Embeddings com PyTorch](../../../../../lessons/5-NLP/14-Embeddings/EmbeddingsPyTorch.ipynb)
* [Embeddings com TensorFlow](../../../../../lessons/5-NLP/14-Embeddings/EmbeddingsTF.ipynb)

## Embeddings Semânticos: Word2Vec

Embora a camada de embedding tenha aprendido a mapear palavras para representações vetoriais, esta representação não necessariamente possui muito significado semântico. Seria interessante aprender uma representação vetorial tal que palavras semelhantes ou sinónimos correspondam a vetores próximos entre si em termos de alguma distância vetorial (por exemplo, distância Euclidiana).

Para isso, precisamos de pré-treinar o nosso modelo de embedding numa grande coleção de texto de uma forma específica. Uma maneira de treinar embeddings semânticos é chamada de [Word2Vec](https://en.wikipedia.org/wiki/Word2vec). Baseia-se em duas arquiteturas principais que são usadas para produzir uma representação distribuída de palavras:

 - **Continuous bag-of-words** (CBoW) — nesta arquitetura, treinamos o modelo para prever uma palavra a partir do contexto circundante. Dado o ngram $(W_{-2},W_{-1},W_0,W_1,W_2)$, o objetivo do modelo é prever $W_0$ a partir de $(W_{-2},W_{-1},W_1,W_2)$.
 - **Continuous skip-gram** é o oposto do CBoW. O modelo usa a janela de palavras de contexto circundante para prever a palavra atual.

CBoW é mais rápido, enquanto o skip-gram é mais lento, mas faz um trabalho melhor ao representar palavras menos frequentes.

![Imagem mostrando os algoritmos CBoW e Skip-Gram para converter palavras em vetores.](../../../../../lessons/5-NLP/14-Embeddings/images/example-algorithms-for-converting-words-to-vectors.png)

> Imagem retirada [deste artigo](https://arxiv.org/pdf/1301.3781.pdf)

Os embeddings pré-treinados do Word2Vec (bem como outros modelos semelhantes, como GloVe) também podem ser usados no lugar da camada de embedding em redes neuronais. No entanto, precisamos de lidar com vocabulários, porque o vocabulário usado para pré-treinar o Word2Vec/GloVe provavelmente será diferente do vocabulário no nosso corpus de texto. Consulte os Notebooks acima para ver como este problema pode ser resolvido.

## Embeddings Contextuais

Uma limitação importante das representações de embeddings pré-treinados tradicionais, como o Word2Vec, é o problema da desambiguação de sentidos das palavras. Embora os embeddings pré-treinados possam capturar algum significado das palavras no contexto, todos os possíveis significados de uma palavra são codificados no mesmo embedding. Isso pode causar problemas em modelos subsequentes, já que muitas palavras, como a palavra 'play', têm significados diferentes dependendo do contexto em que são usadas.

Por exemplo, a palavra 'play' nas duas frases abaixo tem significados bastante diferentes:

- Fui a uma **peça** no teatro.  
- O João quer **brincar** com os amigos.

Os embeddings pré-treinados acima representam ambos os significados da palavra 'play' no mesmo embedding. Para superar esta limitação, precisamos de construir embeddings baseados no **modelo de linguagem**, que é treinado num grande corpus de texto e *sabe* como as palavras podem ser combinadas em diferentes contextos. Discutir embeddings contextuais está fora do âmbito deste tutorial, mas voltaremos a eles ao falar sobre modelos de linguagem mais adiante no curso.

## Conclusão

Nesta lição, descobriu como construir e usar camadas de embedding no TensorFlow e PyTorch para refletir melhor os significados semânticos das palavras.

## 🚀 Desafio

O Word2Vec tem sido usado para algumas aplicações interessantes, incluindo a geração de letras de músicas e poesia. Dê uma vista de olhos a [este artigo](https://www.politetype.com/blog/word2vec-color-poems), que explica como o autor usou o Word2Vec para gerar poesia. Veja também [este vídeo de Dan Shiffmann](https://www.youtube.com/watch?v=LSS_bos_TPI&ab_channel=TheCodingTrain) para descobrir uma explicação diferente desta técnica. Depois, tente aplicar estas técnicas ao seu próprio corpus de texto, talvez obtido no Kaggle.

## [Post-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/214)

## Revisão e Autoestudo

Leia este artigo sobre o Word2Vec: [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/pdf/1301.3781.pdf)

## [Tarefa: Notebooks](assignment.md)

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos para garantir a precisão, é importante notar que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se a tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.