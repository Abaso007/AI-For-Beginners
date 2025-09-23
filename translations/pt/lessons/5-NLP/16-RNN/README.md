<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e2273cc150380a5e191903cea858f021",
  "translation_date": "2025-09-23T13:48:11+00:00",
  "source_file": "lessons/5-NLP/16-RNN/README.md",
  "language_code": "pt"
}
-->
# Redes Neuronais Recorrentes

## [Questionário pré-aula](https://ff-quizzes.netlify.app/en/ai/quiz/31)

Nas secções anteriores, utilizámos representações semânticas ricas de texto e um classificador linear simples sobre as embeddings. Esta arquitetura captura o significado agregado das palavras numa frase, mas não considera a **ordem** das palavras, porque a operação de agregação sobre as embeddings remove esta informação do texto original. Como estes modelos não conseguem modelar a ordem das palavras, não conseguem resolver tarefas mais complexas ou ambíguas, como geração de texto ou resposta a perguntas.

Para capturar o significado de uma sequência de texto, precisamos de usar outra arquitetura de rede neural, chamada **rede neural recorrente**, ou RNN. Numa RNN, passamos a nossa frase pela rede, um símbolo de cada vez, e a rede produz um **estado**, que depois passamos novamente à rede com o próximo símbolo.

![RNN](../../../../../translated_images/rnn.27f5c29c53d727b546ad3961637a267f0fe9ec5ab01f2a26a853c92fcefbb574.pt.png)

> Imagem do autor

Dada a sequência de entrada de tokens X<sub>0</sub>,...,X<sub>n</sub>, a RNN cria uma sequência de blocos de rede neural e treina esta sequência de ponta a ponta usando retropropagação. Cada bloco de rede recebe um par (X<sub>i</sub>,S<sub>i</sub>) como entrada e produz S<sub>i+1</sub> como resultado. O estado final S<sub>n</sub> ou (saída Y<sub>n</sub>) é enviado para um classificador linear para produzir o resultado. Todos os blocos da rede partilham os mesmos pesos e são treinados de ponta a ponta usando uma única passagem de retropropagação.

Como os vetores de estado S<sub>0</sub>,...,S<sub>n</sub> são passados pela rede, esta consegue aprender as dependências sequenciais entre palavras. Por exemplo, quando a palavra *não* aparece em algum lugar da sequência, a rede pode aprender a negar certos elementos dentro do vetor de estado, resultando em negação.

> ✅ Como os pesos de todos os blocos RNN na imagem acima são partilhados, a mesma imagem pode ser representada como um único bloco (à direita) com um loop de feedback recorrente, que passa o estado de saída da rede de volta para a entrada.

## Anatomia de uma Célula RNN

Vamos ver como uma célula RNN simples é organizada. Ela aceita o estado anterior S<sub>i-1</sub> e o símbolo atual X<sub>i</sub> como entradas, e tem de produzir o estado de saída S<sub>i</sub> (e, por vezes, também estamos interessados noutra saída Y<sub>i</sub>, como no caso de redes generativas).

Uma célula RNN simples tem duas matrizes de pesos internas: uma transforma um símbolo de entrada (vamos chamá-la de W) e outra transforma um estado de entrada (H). Neste caso, a saída da rede é calculada como &sigma;(W&times;X<sub>i</sub>+H&times;S<sub>i-1</sub>+b), onde &sigma; é a função de ativação e b é um viés adicional.

<img alt="Anatomia da Célula RNN" src="images/rnn-anatomy.png" width="50%"/>

> Imagem do autor

Em muitos casos, os tokens de entrada são passados por uma camada de embedding antes de entrar na RNN para reduzir a dimensionalidade. Neste caso, se a dimensão dos vetores de entrada for *emb_size* e o vetor de estado for *hid_size*, o tamanho de W será *emb_size*&times;*hid_size*, e o tamanho de H será *hid_size*&times;*hid_size*.

## Memória de Longo e Curto Prazo (LSTM)

Um dos principais problemas das RNNs clássicas é o chamado problema de **gradientes que desaparecem**. Como as RNNs são treinadas de ponta a ponta numa única passagem de retropropagação, têm dificuldade em propagar o erro para as primeiras camadas da rede, e assim a rede não consegue aprender relações entre tokens distantes. Uma das formas de evitar este problema é introduzir **gestão explícita de estado** usando os chamados **gates**. Existem duas arquiteturas bem conhecidas deste tipo: **Memória de Longo e Curto Prazo** (LSTM) e **Unidade de Relevo com Gate** (GRU).

![Imagem mostrando um exemplo de célula de memória de longo e curto prazo](../../../../../lessons/5-NLP/16-RNN/images/long-short-term-memory-cell.svg)

> Fonte da imagem a definir

A rede LSTM é organizada de forma semelhante à RNN, mas existem dois estados que são passados de camada para camada: o estado real C e o vetor oculto H. Em cada unidade, o vetor oculto H<sub>i</sub> é concatenado com a entrada X<sub>i</sub>, e eles controlam o que acontece ao estado C através de **gates**. Cada gate é uma rede neural com ativação sigmoide (saída no intervalo [0,1]), que pode ser vista como uma máscara bit a bit quando multiplicada pelo vetor de estado. Existem os seguintes gates (da esquerda para a direita na imagem acima):

* O **gate de esquecimento** recebe um vetor oculto e determina quais componentes do vetor C precisamos esquecer e quais passar adiante.
* O **gate de entrada** extrai alguma informação dos vetores de entrada e ocultos e insere-a no estado.
* O **gate de saída** transforma o estado através de uma camada linear com ativação *tanh*, depois seleciona alguns dos seus componentes usando um vetor oculto H<sub>i</sub> para produzir um novo estado C<sub>i+1</sub>.

Os componentes do estado C podem ser vistos como algumas flags que podem ser ativadas ou desativadas. Por exemplo, quando encontramos o nome *Alice* na sequência, podemos assumir que se refere a uma personagem feminina e ativar a flag no estado indicando que temos um substantivo feminino na frase. Quando encontramos posteriormente a frase *e Tom*, ativamos a flag indicando que temos um substantivo plural. Assim, manipulando o estado, podemos supostamente acompanhar as propriedades gramaticais das partes da frase.

> ✅ Um excelente recurso para entender os detalhes internos do LSTM é este ótimo artigo [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) de Christopher Olah.

## RNNs Bidirecionais e Multicamadas

Discutimos redes recorrentes que operam numa direção, do início de uma sequência até ao fim. Parece natural, porque se assemelha à forma como lemos e ouvimos discurso. No entanto, como em muitos casos práticos temos acesso aleatório à sequência de entrada, pode fazer sentido executar o cálculo recorrente em ambas as direções. Estas redes são chamadas de **RNNs bidirecionais**. Ao lidar com redes bidirecionais, precisaríamos de dois vetores de estado oculto, um para cada direção.

Uma rede recorrente, seja unidirecional ou bidirecional, captura certos padrões dentro de uma sequência e pode armazená-los num vetor de estado ou passá-los para a saída. Tal como nas redes convolucionais, podemos construir outra camada recorrente sobre a primeira para capturar padrões de nível superior e construir a partir dos padrões de baixo nível extraídos pela primeira camada. Isto leva-nos à noção de uma **RNN multicamada**, que consiste em duas ou mais redes recorrentes, onde a saída da camada anterior é passada para a próxima camada como entrada.

![Imagem mostrando uma RNN multicamada com LSTM](../../../../../translated_images/multi-layer-lstm.dd975e29bb2a59fe58b429db833932d734c81f211cad2783797a9608984acb8c.pt.jpg)

*Imagem retirada [deste excelente artigo](https://towardsdatascience.com/from-a-lstm-cell-to-a-multilayer-lstm-network-with-pytorch-2899eb5696f3) de Fernando López*

## ✍️ Exercícios: Embeddings

Continue a sua aprendizagem nos seguintes notebooks:

* [RNNs com PyTorch](RNNPyTorch.ipynb)
* [RNNs com TensorFlow](RNNTF.ipynb)

## Conclusão

Nesta unidade, vimos que as RNNs podem ser usadas para classificação de sequências, mas na verdade, elas podem lidar com muitas outras tarefas, como geração de texto, tradução automática e mais. Vamos considerar essas tarefas na próxima unidade.

## 🚀 Desafio

Leia alguma literatura sobre LSTMs e considere as suas aplicações:

- [Grid Long Short-Term Memory](https://arxiv.org/pdf/1507.01526v1.pdf)
- [Show, Attend and Tell: Neural Image Caption
Generation with Visual Attention](https://arxiv.org/pdf/1502.03044v2.pdf)

## [Questionário pós-aula](https://ff-quizzes.netlify.app/en/ai/quiz/32)

## Revisão e Autoestudo

- [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) de Christopher Olah.

## [Tarefa: Notebooks](assignment.md)

---

