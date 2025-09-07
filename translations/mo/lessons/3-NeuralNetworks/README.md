<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5abc5f7978919be90cd313f0c20e8228",
  "translation_date": "2025-09-07T14:28:48+00:00",
  "source_file": "lessons/3-NeuralNetworks/README.md",
  "language_code": "mo"
}
-->
# 神經網路簡介

![神經網路簡介內容摘要的手繪圖](../../../../translated_images/ai-neuralnetworks.1c687ae40bc86e834f497844866a26d3e0886650a67a4bbe29442e2f157d3b18.mo.png)

如我們在介紹中所討論的，實現智能的一種方法是訓練一個**電腦模型**或**人工大腦**。自20世紀中期以來，研究人員嘗試了不同的數學模型，直到最近這個方向證明非常成功。這些模仿大腦的數學模型被稱為**神經網路**。

> 有時神經網路被稱為*人工神經網路*（Artificial Neural Networks，ANNs），以表明我們討論的是模型，而不是實際的神經元網路。

## 機器學習

神經網路屬於一個更大的學科，稱為**機器學習**，其目標是利用數據訓練能夠解決問題的電腦模型。機器學習是人工智能的重要組成部分，但我們在這份課程中不會涵蓋傳統的機器學習。

> 請參考我們的獨立課程 **[機器學習入門](http://github.com/microsoft/ml-for-beginners)**，以了解更多關於傳統機器學習的內容。

在機器學習中，我們假設有一些例子數據集 **X**，以及相應的輸出值 **Y**。例子通常是由**特徵**組成的N維向量，而輸出被稱為**標籤**。

我們將探討兩種最常見的機器學習問題：

* **分類**：需要將輸入對象分類到兩個或多個類別中。
* **回歸**：需要為每個輸入樣本預測一個數值。

> 當以張量表示輸入和輸出時，輸入數據集是一個大小為 M×N 的矩陣，其中 M 是樣本數量，N 是特徵數量。輸出標籤 **Y** 是大小為 M 的向量。

在這份課程中，我們將專注於神經網路模型。

## 神經元的模型

從生物學中我們知道，我們的大腦由神經細胞組成，每個神經細胞有多個「輸入」（軸突）和一個輸出（樹突）。軸突和樹突可以傳導電信號，而軸突與樹突之間的連接可以表現出不同程度的導電性（由神經遞質控制）。

![神經元模型](../../../../translated_images/synapse-wikipedia.ed20a9e4726ea1c6a3ce8fec51c0b9bec6181946dca0fe4e829bc12fa3bacf01.mo.jpg) | ![神經元模型](../../../../translated_images/artneuron.1a5daa88d20ebe6f5824ddb89fba0bdaaf49f67e8230c1afbec42909df1fc17e.mo.png)
----|----
真實神經元 *（[圖片](https://en.wikipedia.org/wiki/Synapse#/media/File:SynapseSchematic_lines.svg) 來自維基百科）* | 人工神經元 *（作者提供圖片）*

因此，神經元的最簡單數學模型包含幾個輸入 X<sub>1</sub>, ..., X<sub>N</sub> 和一個輸出 Y，以及一系列權重 W<sub>1</sub>, ..., W<sub>N</sub>。輸出計算公式為：

<img src="images/netout.png" alt="Y = f\left(\sum_{i=1}^N X_iW_i\right)" width="131" height="53" align="center"/>

其中 f 是某種非線性的**激活函數**。

> 早期的神經元模型在1943年由 Warren McCullock 和 Walter Pitts 在經典論文 [A logical calculus of the ideas immanent in nervous activity](https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf) 中描述。Donald Hebb 在他的書 "[The Organization of Behavior: A Neuropsychological Theory](https://books.google.com/books?id=VNetYrB8EBoC)" 中提出了這些網路的訓練方法。

## 本章內容

在本章中，我們將學習以下內容：
* [感知器](03-Perceptron/README.md)：最早的二分類神經網路模型之一
* [多層網路](04-OwnFramework/README.md)：以及配套筆記本 [如何構建我們自己的框架](04-OwnFramework/OwnFramework.ipynb)
* [神經網路框架](05-Frameworks/README.md)：包括以下筆記本：[PyTorch](05-Frameworks/IntroPyTorch.ipynb) 和 [Keras/Tensorflow](05-Frameworks/IntroKerasTF.ipynb)
* [過擬合](../../../../lessons/3-NeuralNetworks/05-Frameworks)

---

**免責聲明**：  
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於關鍵信息，建議使用專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤釋不承擔責任。