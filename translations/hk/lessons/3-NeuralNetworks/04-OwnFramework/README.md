<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "789d6c3fb6fc7948a470b33078a5983a",
  "translation_date": "2025-09-23T12:51:29+00:00",
  "source_file": "lessons/3-NeuralNetworks/04-OwnFramework/README.md",
  "language_code": "hk"
}
-->
# 神經網絡簡介：多層感知器

在上一節中，你學習了最簡單的神經網絡模型——單層感知器，一種線性二分類模型。

在本節中，我們將擴展這個模型，形成一個更靈活的框架，使我們能夠：

* 除了二分類之外，還能進行**多分類**
* 除了分類問題之外，還能解決**回歸問題**
* 區分那些非線性可分的類別

我們還將在 Python 中開發自己的模塊化框架，讓我們能夠構建不同的神經網絡架構。

## [課前測驗](https://ff-quizzes.netlify.app/en/ai/quiz/7)

## 機器學習的形式化

讓我們從形式化機器學習問題開始。假設我們有一個訓練數據集 **X** 和標籤 **Y**，我們需要構建一個模型 *f*，以便做出最準確的預測。預測的質量由**損失函數** &lagran; 來衡量。以下是常用的損失函數：

* 對於回歸問題，當我們需要預測一個數值時，可以使用**絕對誤差** &sum;<sub>i</sub>|f(x<sup>(i)</sup>)-y<sup>(i)</sup>|，或**平方誤差** &sum;<sub>i</sub>(f(x<sup>(i)</sup>)-y<sup>(i)</sup>)<sup>2</sup>
* 對於分類問題，我們使用**0-1損失**（本質上與模型的**準確率**相同），或**邏輯損失**。

對於單層感知器，函數 *f* 被定義為線性函數 *f(x)=wx+b*（其中 *w* 是權重矩陣，*x* 是輸入特徵向量，*b* 是偏置向量）。對於不同的神經網絡架構，這個函數可以採用更複雜的形式。

> 在分類問題中，通常希望網絡輸出是對應類別的概率。為了將任意數字轉換為概率（例如對輸出進行歸一化），我們通常使用**softmax**函數 &sigma;，此時函數 *f* 變為 *f(x)=&sigma;(wx+b)*

在上述 *f* 的定義中，*w* 和 *b* 被稱為**參數** &theta;=⟨*w,b*⟩。給定數據集 ⟨**X**,**Y**⟩，我們可以計算整個數據集上的總誤差，作為參數 &theta; 的函數。

> ✅ **神經網絡訓練的目標是通過調整參數 &theta; 來最小化誤差**

## 梯度下降優化

有一種著名的函數優化方法叫做**梯度下降**。其核心思想是，我們可以計算損失函數對參數的導數（在多維情況下稱為**梯度**），並以使誤差減少的方式調整參數。其形式化如下：

* 用一些隨機值初始化參數 w<sup>(0)</sup>, b<sup>(0)</sup>
* 重複以下步驟多次：
    - w<sup>(i+1)</sup> = w<sup>(i)</sup>-&eta;&part;&lagran;/&part;w
    - b<sup>(i+1)</sup> = b<sup>(i)</sup>-&eta;&part;&lagran;/&part;b

在訓練過程中，優化步驟應基於整個數據集進行計算（記住損失是通過所有訓練樣本的總和計算的）。然而，在實際操作中，我們會取數據集的小部分，稱為**小批量**，並基於數據子集計算梯度。由於每次隨機選取子集，這種方法被稱為**隨機梯度下降**（SGD）。

## 多層感知器與反向傳播

如上所述，單層網絡能夠分類線性可分的類別。為了構建更豐富的模型，我們可以將網絡的多層結合起來。數學上，這意味著函數 *f* 將具有更複雜的形式，並通過多個步驟計算：
* z<sub>1</sub>=w<sub>1</sub>x+b<sub>1</sub>
* z<sub>2</sub>=w<sub>2</sub>&alpha;(z<sub>1</sub>)+b<sub>2</sub>
* f = &sigma;(z<sub>2</sub>)

其中，&alpha; 是**非線性激活函數**，&sigma; 是 softmax 函數，參數 &theta;=<*w<sub>1</sub>,b<sub>1</sub>,w<sub>2</sub>,b<sub>2</sub>*>。

梯度下降算法保持不變，但計算梯度會更加困難。根據鏈式微分法則，我們可以計算導數如下：

* &part;&lagran;/&part;w<sub>2</sub> = (&part;&lagran;/&part;&sigma;)(&part;&sigma;/&part;z<sub>2</sub>)(&part;z<sub>2</sub>/&part;w<sub>2</sub>)
* &part;&lagran;/&part;w<sub>1</sub> = (&part;&lagran;/&part;&sigma;)(&part;&sigma;/&part;z<sub>2</sub>)(&part;z<sub>2</sub>/&part;&alpha;)(&part;&alpha;/&part;z<sub>1</sub>)(&part;z<sub>1</sub>/&part;w<sub>1</sub>)

> ✅ 鏈式微分法則用於計算損失函數對參數的導數。

注意，所有這些表達式的最左部分是相同的，因此我們可以有效地從損失函數開始計算導數，並沿著計算圖“向後”進行。因此，訓練多層感知器的方法被稱為**反向傳播**，或“backprop”。

<img alt="計算圖" src="images/ComputeGraphGrad.png"/>

> TODO: 圖片引用

> ✅ 我們將在筆記本示例中更詳細地介紹反向傳播。

## 結論

在本課中，我們構建了自己的神經網絡庫，並將其用於簡單的二維分類任務。

## 🚀 挑戰

在配套的筆記本中，你將實現自己的框架，用於構建和訓練多層感知器。你將能夠詳細了解現代神經網絡的運作方式。

前往 [OwnFramework](OwnFramework.ipynb) 筆記本並完成其中的內容。

## [課後測驗](https://ff-quizzes.netlify.app/en/ai/quiz/8)

## 回顧與自學

反向傳播是 AI 和 ML 中常用的算法，值得[深入研究](https://wikipedia.org/wiki/Backpropagation)。

## [作業](lab/README.md)

在本次實驗中，你需要使用本課中構建的框架來解決 MNIST 手寫數字分類問題。

* [說明](lab/README.md)
* [筆記本](lab/MyFW_MNIST.ipynb)

---

