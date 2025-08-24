<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7e617f0b8de85a43957a853aba09bfeb",
  "translation_date": "2025-08-24T10:17:06+00:00",
  "source_file": "lessons/5-NLP/18-Transformers/README.md",
  "language_code": "pt"
}
-->
# Mecanismos de Atenção e Transformers

## [Questionário pré-aula](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/118)

Um dos problemas mais importantes no domínio do PLN (Processamento de Linguagem Natural) é a **tradução automática**, uma tarefa essencial que sustenta ferramentas como o Google Tradutor. Nesta seção, vamos focar na tradução automática ou, de forma mais geral, em qualquer tarefa de *sequência para sequência* (também chamada de **transdução de frases**).

Com RNNs, a tarefa de sequência para sequência é implementada por duas redes recorrentes, onde uma rede, o **codificador**, comprime uma sequência de entrada em um estado oculto, enquanto outra rede, o **decodificador**, expande esse estado oculto em um resultado traduzido. Existem alguns problemas com essa abordagem:

* O estado final da rede codificadora tem dificuldade em lembrar o início de uma frase, o que resulta em baixa qualidade do modelo para frases longas.
* Todas as palavras em uma sequência têm o mesmo impacto no resultado. Na realidade, no entanto, palavras específicas na sequência de entrada frequentemente têm mais impacto nos resultados sequenciais do que outras.

Os **Mecanismos de Atenção** fornecem um meio de ponderar o impacto contextual de cada vetor de entrada em cada previsão de saída da RNN. Isso é implementado criando atalhos entre os estados intermediários da RNN de entrada e a RNN de saída. Dessa forma, ao gerar o símbolo de saída y<sub>t</sub>, consideramos todos os estados ocultos de entrada h<sub>i</sub>, com diferentes coeficientes de peso α<sub>t,i</sub>.

![Imagem mostrando um modelo codificador/decodificador com uma camada de atenção aditiva](../../../../../lessons/5-NLP/18-Transformers/images/encoder-decoder-attention.png)

> O modelo codificador-decodificador com mecanismo de atenção aditiva em [Bahdanau et al., 2015](https://arxiv.org/pdf/1409.0473.pdf), citado deste [blog post](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html)

A matriz de atenção {α<sub>i,j</sub>} representaria o grau em que certas palavras de entrada influenciam a geração de uma palavra específica na sequência de saída. Abaixo está um exemplo de tal matriz:

![Imagem mostrando um alinhamento de exemplo encontrado pelo RNNsearch-50, retirada de Bahdanau - arviz.org](../../../../../lessons/5-NLP/18-Transformers/images/bahdanau-fig3.png)

> Figura de [Bahdanau et al., 2015](https://arxiv.org/pdf/1409.0473.pdf) (Fig.3)

Os mecanismos de atenção são responsáveis por grande parte do estado da arte atual ou próximo ao atual no PLN. No entanto, adicionar atenção aumenta significativamente o número de parâmetros do modelo, o que levou a problemas de escalabilidade com RNNs. Uma limitação chave na escalabilidade das RNNs é que a natureza recorrente dos modelos dificulta o agrupamento e a paralelização do treinamento. Em uma RNN, cada elemento de uma sequência precisa ser processado em ordem sequencial, o que significa que não pode ser facilmente paralelizado.

![Codificador Decodificador com Atenção](../../../../../lessons/5-NLP/18-Transformers/images/EncDecAttention.gif)

> Figura do [Blog do Google](https://research.googleblog.com/2016/09/a-neural-network-for-machine.html)

A adoção de mecanismos de atenção, combinada com essa limitação, levou à criação dos agora modelos Transformers de estado da arte que conhecemos e usamos hoje, como BERT e Open-GPT3.

## Modelos Transformers

Uma das principais ideias por trás dos transformers é evitar a natureza sequencial das RNNs e criar um modelo que seja paralelizável durante o treinamento. Isso é alcançado implementando duas ideias:

* codificação posicional
* uso do mecanismo de auto-atenção para capturar padrões em vez de RNNs (ou CNNs) (é por isso que o artigo que introduz os transformers se chama *[Attention is all you need](https://arxiv.org/abs/1706.03762)*)

### Codificação/Embelezamento Posicional

A ideia da codificação posicional é a seguinte:  
1. Ao usar RNNs, a posição relativa dos tokens é representada pelo número de passos, e, portanto, não precisa ser representada explicitamente.  
2. No entanto, ao mudarmos para atenção, precisamos saber as posições relativas dos tokens dentro de uma sequência.  
3. Para obter a codificação posicional, aumentamos nossa sequência de tokens com uma sequência de posições dos tokens na sequência (ou seja, uma sequência de números 0, 1, ...).  
4. Em seguida, misturamos a posição do token com um vetor de embelezamento do token. Para transformar a posição (inteiro) em um vetor, podemos usar diferentes abordagens:

* Embelezamento treinável, semelhante ao embelezamento de tokens. Esta é a abordagem que consideramos aqui. Aplicamos camadas de embelezamento tanto nos tokens quanto em suas posições, resultando em vetores de embelezamento com as mesmas dimensões, que então somamos.
* Função fixa de codificação posicional, como proposto no artigo original.

<img src="images/pos-embedding.png" width="50%"/>

> Imagem do autor

O resultado que obtemos com o embelezamento posicional incorpora tanto o token original quanto sua posição dentro de uma sequência.

### Auto-Atenção Multi-Cabeça

Em seguida, precisamos capturar alguns padrões dentro de nossa sequência. Para isso, os transformers usam um mecanismo de **auto-atenção**, que é essencialmente atenção aplicada à mesma sequência como entrada e saída. Aplicar auto-atenção nos permite levar em conta o **contexto** dentro da frase e ver quais palavras estão inter-relacionadas. Por exemplo, permite-nos ver quais palavras são referidas por correferências, como *it*, e também considerar o contexto:

![](../../../../../lessons/5-NLP/18-Transformers/images/CoreferenceResolution.png)

> Imagem do [Blog do Google](https://research.googleblog.com/2017/08/transformer-novel-neural-network.html)

Nos transformers, usamos **Atenção Multi-Cabeça** para dar à rede o poder de capturar vários tipos diferentes de dependências, como relações de palavras de longo prazo vs. curto prazo, correferência vs. outra coisa, etc.

O [Notebook TensorFlow](../../../../../lessons/5-NLP/18-Transformers/TransformersTF.ipynb) contém mais detalhes sobre a implementação das camadas do transformer.

### Atenção Codificador-Decodificador

Nos transformers, a atenção é usada em dois lugares:

* Para capturar padrões dentro do texto de entrada usando auto-atenção.
* Para realizar a tradução de sequência - é a camada de atenção entre o codificador e o decodificador.

A atenção codificador-decodificador é muito semelhante ao mecanismo de atenção usado nas RNNs, conforme descrito no início desta seção. Este diagrama animado explica o papel da atenção codificador-decodificador.

![GIF animado mostrando como as avaliações são realizadas em modelos transformers.](../../../../../lessons/5-NLP/18-Transformers/images/transformer-animated-explanation.gif)

Como cada posição de entrada é mapeada de forma independente para cada posição de saída, os transformers podem paralelizar melhor do que as RNNs, o que permite modelos de linguagem muito maiores e mais expressivos. Cada cabeça de atenção pode ser usada para aprender diferentes relações entre palavras, melhorando as tarefas de Processamento de Linguagem Natural.

## BERT

**BERT** (Bidirectional Encoder Representations from Transformers) é uma rede transformer muito grande com várias camadas: 12 camadas para o *BERT-base* e 24 para o *BERT-large*. O modelo é inicialmente pré-treinado em um grande corpus de dados textuais (Wikipedia + livros) usando treinamento não supervisionado (prevendo palavras mascaradas em uma frase). Durante o pré-treinamento, o modelo absorve níveis significativos de compreensão da linguagem, que podem ser aproveitados com outros conjuntos de dados usando ajuste fino. Esse processo é chamado de **aprendizagem por transferência**.

![imagem de http://jalammar.github.io/illustrated-bert/](../../../../../lessons/5-NLP/18-Transformers/images/jalammarBERT-language-modeling-masked-lm.png)

> Imagem [fonte](http://jalammar.github.io/illustrated-bert/)

## ✍️ Exercícios: Transformers

Continue o seu aprendizado nos seguintes notebooks:

* [Transformers em PyTorch](../../../../../lessons/5-NLP/18-Transformers/TransformersPyTorch.ipynb)
* [Transformers em TensorFlow](../../../../../lessons/5-NLP/18-Transformers/TransformersTF.ipynb)

## Conclusão

Nesta lição, você aprendeu sobre Transformers e Mecanismos de Atenção, ferramentas essenciais na caixa de ferramentas do PLN. Existem muitas variações das arquiteturas de Transformers, incluindo BERT, DistilBERT, BigBird, OpenGPT3 e mais, que podem ser ajustadas. O [pacote HuggingFace](https://github.com/huggingface/) fornece um repositório para treinar muitas dessas arquiteturas com PyTorch e TensorFlow.

## 🚀 Desafio

## [Questionário pós-aula](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/218)

## Revisão e Autoestudo

* [Blog post](https://mchromiak.github.io/articles/2017/Sep/12/Transformer-Attention-is-all-you-need/), explicando o clássico artigo [Attention is all you need](https://arxiv.org/abs/1706.03762) sobre transformers.
* [Uma série de posts no blog](https://towardsdatascience.com/transformers-explained-visually-part-1-overview-of-functionality-95a6dd460452) sobre transformers, explicando a arquitetura em detalhe.

## [Tarefa](assignment.md)

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos para garantir a precisão, é importante ter em conta que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se a tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes da utilização desta tradução.