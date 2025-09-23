<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a560d5b845962cf33dc102266e409568",
  "translation_date": "2025-09-23T12:46:43+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/README.md",
  "language_code": "hk"
}
-->
# 卷積神經網絡

我們之前已經看到，神經網絡在處理圖像方面表現相當不錯，即使是單層感知器也能以合理的準確度識別 MNIST 數據集中的手寫數字。然而，MNIST 數據集非常特殊，所有的數字都被集中在圖像的中心，這使得任務變得更簡單。

## [課前測驗](https://ff-quizzes.netlify.app/en/ai/quiz/13)

在現實生活中，我們希望能夠在圖片中識別物體，而不受其在圖像中具體位置的影響。計算機視覺與一般的分類不同，因為當我們試圖在圖片中找到某個物體時，我們是在掃描圖像以尋找一些特定的**模式**及其組合。例如，當尋找一隻貓時，我們可能首先尋找水平線，這些線可能形成貓鬚，然後某些貓鬚的組合可以告訴我們這是一張貓的圖片。某些模式的相對位置和存在是重要的，而不是它們在圖像中的具體位置。

為了提取模式，我們將使用**卷積濾波器**的概念。正如你所知，圖像是由一個二維矩陣或帶有色彩深度的三維張量表示的。應用濾波器意味著我們取一個相對較小的**濾波核**矩陣，並對原始圖像中的每個像素與其鄰近點進行加權平均。我們可以將其視為一個小窗口在整個圖像上滑動，並根據濾波核矩陣中的權重對所有像素進行平均。

![垂直邊緣濾波器](../../../../../translated_images/filter-vert.b7148390ca0bc356ddc7e55555d2481819c1e86ddde9dce4db5e71a69d6f887f.hk.png) | ![水平邊緣濾波器](../../../../../translated_images/filter-horiz.59b80ed4feb946efbe201a7fe3ca95abb3364e266e6fd90820cb893b4d3a6dda.hk.png)
----|----

> 圖片由 Dmitry Soshnikov 提供

例如，如果我們對 MNIST 數字應用 3x3 的垂直邊緣和水平邊緣濾波器，我們可以在原始圖像中有垂直和水平邊緣的地方得到高亮（例如高值）。因此，這兩個濾波器可以用來“尋找”邊緣。同樣，我們可以設計不同的濾波器來尋找其他低層次的模式：

<img src="images/lmfilters.jpg" width="500" align="center"/>

> [Leung-Malik 濾波器庫](https://www.robots.ox.ac.uk/~vgg/research/texclass/filters.html)的圖片

然而，雖然我們可以手動設計濾波器來提取某些模式，我們也可以設計網絡，使其能夠自動學習模式。這是 CNN 背後的主要思想之一。

## CNN 的主要思想

CNN 的工作方式基於以下重要思想：

* 卷積濾波器可以提取模式
* 我們可以設計網絡，使濾波器能夠自動訓練
* 我們可以使用相同的方法來在高層次特徵中尋找模式，而不僅僅是在原始圖像中。因此，CNN 的特徵提取在特徵層次上工作，從低層次的像素組合開始，到更高層次的圖像部分組合。

![層次特徵提取](../../../../../translated_images/FeatureExtractionCNN.d9b456cbdae7cb643fde3032b81b2940e3cf8be842e29afac3f482725ba7f95c.hk.png)

> 圖片來自 [Hislop-Lynch 的論文](https://www.semanticscholar.org/paper/Computer-vision-based-pedestrian-trajectory-Hislop-Lynch/26e6f74853fc9bbb7487b06dc2cf095d36c9021d)，基於[他們的研究](https://dl.acm.org/doi/abs/10.1145/1553374.1553453)

## ✍️ 練習：卷積神經網絡

讓我們繼續探索卷積神經網絡的工作原理，以及如何通過相關的筆記本實現可訓練的濾波器：

* [卷積神經網絡 - PyTorch](ConvNetsPyTorch.ipynb)
* [卷積神經網絡 - TensorFlow](ConvNetsTF.ipynb)

## 金字塔架構

大多數用於圖像處理的 CNN 都遵循所謂的金字塔架構。應用於原始圖像的第一個卷積層通常具有相對較少的濾波器（8-16），這些濾波器對應於不同的像素組合，例如水平/垂直線條或筆劃。在下一層，我們減少網絡的空間維度，並增加濾波器的數量，這對應於更多簡單特徵的可能組合。隨著每一層的進展，向最終分類器移動時，圖像的空間維度減少，而濾波器的數量增加。

例如，讓我們看看 VGG-16 的架構，這是一個在 2014 年 ImageNet 的前五名分類中達到 92.7% 準確率的網絡：

![ImageNet 層](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.hk.jpg)

![ImageNet 金字塔](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.hk.jpg)

> 圖片來自 [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

## 最知名的 CNN 架構

[繼續學習最知名的 CNN 架構](CNN_Architectures.md)

---

