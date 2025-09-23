<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "6568aaae7e0e4afed4b5d74b5b223700",
  "translation_date": "2025-09-23T08:21:22+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/README.md",
  "language_code": "br"
}
-->
# Segmentação

Anteriormente, aprendemos sobre Detecção de Objetos, que nos permite localizar objetos na imagem ao prever suas *caixas delimitadoras*. No entanto, para algumas tarefas, não precisamos apenas de caixas delimitadoras, mas também de uma localização mais precisa dos objetos. Essa tarefa é chamada de **segmentação**.

## [Quiz pré-aula](https://ff-quizzes.netlify.app/en/ai/quiz/23)

A segmentação pode ser vista como **classificação de pixels**, onde para **cada** pixel da imagem devemos prever sua classe (*fundo* sendo uma das classes). Existem dois principais algoritmos de segmentação:

* **Segmentação semântica** apenas informa a classe do pixel, sem distinguir entre diferentes objetos da mesma classe.
* **Segmentação por instância** divide as classes em diferentes instâncias.

Na segmentação por instância, essas ovelhas são objetos diferentes, mas na segmentação semântica todas as ovelhas são representadas por uma única classe.

<img src="images/instance_vs_semantic.jpeg" width="50%">

> Imagem retirada [deste post de blog](https://nirmalamurali.medium.com/image-classification-vs-semantic-segmentation-vs-instance-segmentation-625c33a08d50)

Existem diferentes arquiteturas neurais para segmentação, mas todas têm a mesma estrutura. De certa forma, é semelhante ao autoencoder que você aprendeu anteriormente, mas em vez de deconstruir a imagem original, nosso objetivo é deconstruir uma **máscara**. Assim, uma rede de segmentação possui as seguintes partes:

* **Codificador (Encoder)** extrai características da imagem de entrada.
* **Decodificador (Decoder)** transforma essas características na **imagem de máscara**, com o mesmo tamanho e número de canais correspondentes ao número de classes.

<img src="images/segm.png" width="80%">

> Imagem retirada [desta publicação](https://arxiv.org/pdf/2001.05566.pdf)

Devemos destacar especialmente a função de perda usada para segmentação. Ao usar autoencoders clássicos, precisamos medir a similaridade entre duas imagens, e podemos usar o erro quadrático médio (MSE) para isso. Na segmentação, cada pixel na imagem de máscara alvo representa o número da classe (codificado em one-hot ao longo da terceira dimensão), então precisamos usar funções de perda específicas para classificação - perda de entropia cruzada, média sobre todos os pixels. Se a máscara for binária, usa-se a **perda de entropia cruzada binária** (BCE).

> ✅ One-hot encoding é uma técnica para codificar um rótulo de classe em um vetor de comprimento igual ao número de classes. Confira [este artigo](https://datagy.io/sklearn-one-hot-encode/) sobre essa técnica.

## Segmentação para Imagens Médicas

Nesta lição, veremos a segmentação em ação treinando a rede para reconhecer nevos humanos (também conhecidos como pintas) em imagens médicas. Usaremos o <a href="https://www.fc.up.pt/addi/ph2%20database.html">Banco de Dados PH<sup>2</sup></a> de imagens dermatoscópicas como fonte de imagens. Este conjunto de dados contém 200 imagens de três classes: nevo típico, nevo atípico e melanoma. Todas as imagens também possuem uma **máscara** correspondente que delimita o nevo.

> ✅ Esta técnica é particularmente apropriada para este tipo de imagem médica, mas quais outras aplicações do mundo real você consegue imaginar?

<img alt="navi" src="images/navi.png"/>

> Imagem retirada do Banco de Dados PH<sup>2</sup>

Treinaremos um modelo para segmentar qualquer nevo do fundo da imagem.

## ✍️ Exercícios: Segmentação Semântica

Abra os notebooks abaixo para aprender mais sobre diferentes arquiteturas de segmentação semântica, praticar com elas e vê-las em ação.

* [Segmentação Semântica Pytorch](SemanticSegmentationPytorch.ipynb)
* [Segmentação Semântica TensorFlow](SemanticSegmentationTF.ipynb)

## [Quiz pós-aula](https://ff-quizzes.netlify.app/en/ai/quiz/24)

## Conclusão

A segmentação é uma técnica muito poderosa para classificação de imagens, indo além das caixas delimitadoras para a classificação em nível de pixel. É uma técnica usada em imagens médicas, entre outras aplicações.

## 🚀 Desafio

A segmentação corporal é apenas uma das tarefas comuns que podemos realizar com imagens de pessoas. Outras tarefas importantes incluem **detecção de esqueleto** e **detecção de pose**. Experimente a biblioteca [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) para ver como a detecção de pose pode ser usada.

## Revisão e Autoestudo

Este [artigo da Wikipedia](https://wikipedia.org/wiki/Image_segmentation) oferece uma boa visão geral das várias aplicações dessa técnica. Aprenda mais por conta própria sobre os subdomínios de Segmentação por Instância e Segmentação Panóptica neste campo de estudo.

## [Tarefa](lab/README.md)

Neste laboratório, experimente **segmentação do corpo humano** usando o [Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) do Kaggle.

---

