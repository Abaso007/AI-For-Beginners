<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0b306c04f5337b6e7430e5c0b16bb5c0",
  "translation_date": "2025-08-24T21:55:14+00:00",
  "source_file": "lessons/4-ComputerVision/09-Autoencoders/README.md",
  "language_code": "tw"
}
-->
# 自動編碼器

在訓練 CNN 時，其中一個問題是我們需要大量的標記數據。以圖像分類為例，我們需要將圖像分成不同的類別，這是一項需要手動完成的工作。

## [課前測驗](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/109)

然而，我們可能希望使用原始（未標記）的數據來訓練 CNN 特徵提取器，這被稱為**自監督學習**。取代標籤，我們將使用訓練圖像作為網絡的輸入和輸出。**自動編碼器**的主要概念是，我們將有一個**編碼器網絡**，將輸入圖像轉換為某種**潛在空間**（通常只是某種較小尺寸的向量），然後是**解碼器網絡**，其目標是重建原始圖像。

> ✅ [自動編碼器](https://wikipedia.org/wiki/Autoencoder) 是“一種用於學習未標記數據的高效編碼的人工神經網絡。”

由於我們訓練自動編碼器以捕捉原始圖像中的盡可能多的信息以進行準確的重建，網絡試圖找到最佳的**嵌入**來捕捉輸入圖像的含義。

![自動編碼器示意圖](../../../../../translated_images/autoencoder_schema.5e6fc9ad98a5eb6197f3513cf3baf4dfbe1389a6ae74daebda64de9f1c99f142.tw.jpg)

> 圖片來源：[Keras 博客](https://blog.keras.io/building-autoencoders-in-keras.html)

## 使用自動編碼器的場景

雖然重建原始圖像本身似乎沒有太大的用途，但有一些場景自動編碼器特別有用：

* **降低圖像的維度以進行可視化**或**訓練圖像嵌入**。通常，自動編碼器比 PCA 效果更好，因為它考慮了圖像的空間特性和層次特徵。
* **去噪**，即去除圖像中的噪點。由於噪點攜帶了大量無用的信息，自動編碼器無法將所有噪點都嵌入到相對較小的潛在空間中，因此它只捕捉圖像的重要部分。在訓練去噪器時，我們從原始圖像開始，並使用人工添加噪點的圖像作為自動編碼器的輸入。
* **超分辨率**，提高圖像分辨率。我們從高分辨率圖像開始，並使用低分辨率圖像作為自動編碼器的輸入。
* **生成模型**。一旦我們訓練了自動編碼器，解碼器部分可以用來從隨機潛在向量開始創建新物件。

## 變分自動編碼器 (VAE)

傳統的自動編碼器以某種方式降低輸入數據的維度，找出輸入圖像的重要特徵。然而，潛在向量通常沒有太多意義。換句話說，以 MNIST 數據集為例，找出哪些數字對應於不同的潛在向量並不容易，因為相近的潛在向量不一定對應於相同的數字。

另一方面，為了訓練*生成*模型，了解潛在空間會更好。這一想法引導我們走向**變分自動編碼器** (VAE)。

VAE 是一種自動編碼器，它學習預測潛在參數的*統計分佈*，即所謂的**潛在分佈**。例如，我們可能希望潛在向量以某種均值 z<sub>mean</sub> 和標準差 z<sub>sigma</sub>（均值和標準差都是某種維度 d 的向量）呈正態分佈。VAE 中的編碼器學習預測這些參數，然後解碼器從該分佈中取隨機向量以重建物件。

總結如下：

* 從輸入向量，我們預測 `z_mean` 和 `z_log_sigma`（我們預測的是標準差的對數而不是標準差本身）
* 我們從分佈 N(z<sub>mean</sub>,exp(z<sub>log\_sigma</sub>)) 中抽樣一個向量 `sample`
* 解碼器嘗試使用 `sample` 作為輸入向量解碼原始圖像

<img src="images/vae.png" width="50%">

> 圖片來源：[這篇博客文章](https://ijdykeman.github.io/ml/2016/12/21/cvae.html) 作者 Isaak Dykeman

變分自動編碼器使用一個由兩部分組成的複雜損失函數：

* **重建損失**是顯示重建圖像與目標圖像有多接近的損失函數（可以是均方誤差，或 MSE）。它與普通自動編碼器的損失函數相同。
* **KL 損失**，確保潛在變量分佈保持接近正態分佈。它基於 [Kullback-Leibler 散度](https://www.countbayesie.com/blog/2017/5/9/kullback-leibler-divergence-explained) 的概念——一種估算兩個統計分佈相似程度的度量。

VAE 的一個重要優勢是它使我們能夠相對容易地生成新圖像，因為我們知道從哪個分佈中抽樣潛在向量。例如，如果我們在 MNIST 上使用 2D 潛在向量訓練 VAE，我們可以改變潛在向量的組件以獲得不同的數字：

<img alt="vaemnist" src="images/vaemnist.png" width="50%"/>

> 圖片來源：[Dmitry Soshnikov](http://soshnikov.com)

觀察圖像如何相互融合，當我們開始從潛在參數空間的不同部分獲取潛在向量時。我們還可以在 2D 中可視化此空間：

<img alt="vaemnist cluster" src="images/vaemnist-diag.png" width="50%"/> 

> 圖片來源：[Dmitry Soshnikov](http://soshnikov.com)

## ✍️ 練習：自動編碼器

在以下筆記本中了解更多關於自動編碼器的內容：

* [TensorFlow 中的自動編碼器](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoencodersTF.ipynb)
* [PyTorch 中的自動編碼器](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoEncodersPyTorch.ipynb)

## 自動編碼器的特性

* **數據特定** - 它們僅適用於訓練過的圖像類型。例如，如果我們在花卉上訓練超分辨率網絡，它在肖像上效果不佳。這是因為網絡可以通過從訓練數據集中學到的特徵中提取細節來生成高分辨率圖像。
* **有損** - 重建的圖像與原始圖像不完全相同。損失的性質由訓練期間使用的*損失函數*定義。
* 適用於**未標記數據**

## [課後測驗](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/209)

## 結論

在本課中，您了解了 AI 科學家可用的各種自動編碼器類型。您學習了如何構建它們，以及如何使用它們重建圖像。您還了解了 VAE 以及如何使用它生成新圖像。

## 🚀 挑戰

在本課中，您學習了如何將自動編碼器用於圖像。但它們也可以用於音樂！查看 Magenta 項目的 [MusicVAE](https://magenta.tensorflow.org/music-vae) 項目，它使用自動編碼器來學習重建音樂。使用此庫進行一些[實驗](https://colab.research.google.com/github/magenta/magenta-demos/blob/master/colab-notebooks/Multitrack_MusicVAE.ipynb)，看看您能創造出什麼。

## [課後測驗](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/208)

## 回顧與自學

作為參考，您可以在以下資源中了解更多關於自動編碼器的內容：

* [在 Keras 中構建自動編碼器](https://blog.keras.io/building-autoencoders-in-keras.html)
* [NeuroHive 博客文章](https://neurohive.io/ru/osnovy-data-science/variacionnyj-avtojenkoder-vae/)
* [變分自動編碼器解析](https://kvfrans.com/variational-autoencoders-explained/)
* [條件變分自動編碼器](https://ijdykeman.github.io/ml/2016/12/21/cvae.html)

## 作業

在 [使用 TensorFlow 的筆記本](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoencodersTF.ipynb) 的末尾，您會找到一個“任務”——將其作為您的作業。

**免責聲明**：  
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原始語言的文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤讀概不負責。