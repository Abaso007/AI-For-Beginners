<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7ba20f54a5bfcd6521018cdfb17c7c57",
  "translation_date": "2025-09-23T13:46:46+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/README.md",
  "language_code": "pt"
}
-->
# Modelação de Linguagem

Embeddings semânticos, como Word2Vec e GloVe, são, na verdade, um primeiro passo para a **modelação de linguagem** - criar modelos que de alguma forma *compreendem* (ou *representam*) a natureza da linguagem.

## [Questionário pré-aula](https://ff-quizzes.netlify.app/en/ai/quiz/29)

A ideia principal por trás da modelação de linguagem é treiná-los em conjuntos de dados não rotulados de forma não supervisionada. Isto é importante porque temos enormes quantidades de texto não rotulado disponíveis, enquanto a quantidade de texto rotulado estará sempre limitada pelo esforço necessário para rotular. Na maioria das vezes, podemos construir modelos de linguagem que conseguem **prever palavras em falta** no texto, porque é fácil ocultar uma palavra aleatória no texto e usá-la como amostra de treino.

## Treinar Embeddings

Nos nossos exemplos anteriores, utilizámos embeddings semânticos pré-treinados, mas é interessante ver como esses embeddings podem ser treinados. Existem várias ideias possíveis que podem ser utilizadas:

* **Modelação de linguagem N-Gram**, onde prevemos um token olhando para os N tokens anteriores (N-gram).
* **Continuous Bag-of-Words** (CBoW), onde prevemos o token central $W_0$ numa sequência de tokens $W_{-N}$, ..., $W_N$.
* **Skip-gram**, onde prevemos um conjunto de tokens vizinhos {$W_{-N},\dots, W_{-1}, W_1,\dots, W_N$} a partir do token central $W_0$.

![imagem do artigo sobre conversão de palavras em vetores](../../../../../translated_images/example-algorithms-for-converting-words-to-vectors.fbe9207a726922f6f0f5de66427e8a6eda63809356114e28fb1fa5f4a83ebda7.pt.png)

> Imagem retirada [deste artigo](https://arxiv.org/pdf/1301.3781.pdf)

## ✍️ Notebooks de Exemplo: Treinar modelo CBoW

Continue a sua aprendizagem nos seguintes notebooks:

* [Treinar CBoW Word2Vec com TensorFlow](CBoW-TF.ipynb)
* [Treinar CBoW Word2Vec com PyTorch](CBoW-PyTorch.ipynb)

## Conclusão

Na aula anterior vimos que embeddings de palavras funcionam como magia! Agora sabemos que treinar embeddings de palavras não é uma tarefa muito complexa, e devemos ser capazes de treinar os nossos próprios embeddings para texto específico de um domínio, se necessário.

## [Questionário pós-aula](https://ff-quizzes.netlify.app/en/ai/quiz/30)

## Revisão & Estudo Individual

* [Tutorial oficial do PyTorch sobre Modelação de Linguagem](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html).
* [Tutorial oficial do TensorFlow sobre treinar modelo Word2Vec](https://www.TensorFlow.org/tutorials/text/word2vec).
* Utilizar o framework **gensim** para treinar os embeddings mais comuns em poucas linhas de código está descrito [nesta documentação](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html).

## 🚀 [Tarefa: Treinar Modelo Skip-Gram](lab/README.md)

No laboratório, desafiamos você a modificar o código desta aula para treinar um modelo skip-gram em vez de CBoW. [Leia os detalhes](lab/README.md)

---

