<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "31b46ba1f3aa78578134d4829f88be53",
  "translation_date": "2025-08-24T21:47:26+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/README.md",
  "language_code": "hk"
}
-->
# 語言建模

語義嵌入（例如 Word2Vec 和 GloVe）實際上是邁向**語言建模**的第一步——創建某種*理解*（或*表示*）語言特性的模型。

## [課前測驗](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/115)

語言建模的核心概念是以無監督的方式在未標籤的數據集上進行訓練。這一點非常重要，因為我們擁有大量未標籤的文本，而標籤文本的數量則始終受限於我們能投入的標籤工作量。通常，我們可以構建能夠**預測文本中缺失單詞**的語言模型，因為隨機遮蔽文本中的某個單詞並將其作為訓練樣本是一件相對簡單的事情。

## 訓練嵌入

在之前的例子中，我們使用了預訓練的語義嵌入，但了解這些嵌入是如何訓練的也非常有趣。有幾種可能的想法可以用於訓練：

* **N-Gram** 語言建模，通過查看前 N 個標記（N-gram）來預測當前標記。
* **連續詞袋模型**（CBoW），在標記序列 $W_{-N}$, ..., $W_N$ 中預測中間的標記 $W_0$。
* **Skip-gram**，從中間標記 $W_0$ 預測一組相鄰的標記 {$W_{-N},\dots, W_{-1}, W_1,\dots, W_N$}。

![來自論文的將單詞轉換為向量的算法示例](../../../../../translated_images/example-algorithms-for-converting-words-to-vectors.fbe9207a726922f6f0f5de66427e8a6eda63809356114e28fb1fa5f4a83ebda7.hk.png)

> 圖片來源：[這篇論文](https://arxiv.org/pdf/1301.3781.pdf)

## ✍️ 範例筆記本：訓練 CBoW 模型

繼續學習以下筆記本中的內容：

* [使用 TensorFlow 訓練 CBoW Word2Vec](../../../../../lessons/5-NLP/15-LanguageModeling/CBoW-TF.ipynb)
* [使用 PyTorch 訓練 CBoW Word2Vec](../../../../../lessons/5-NLP/15-LanguageModeling/CBoW-PyTorch.ipynb)

## 結論

在上一課中，我們看到詞嵌入的效果就像魔法一樣！現在我們知道，訓練詞嵌入並不是一件非常複雜的事情，如果需要，我們應該能夠為特定領域的文本訓練自己的詞嵌入。

## [課後測驗](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/215)

## 回顧與自學

* [PyTorch 官方語言建模教程](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html)。
* [TensorFlow 官方訓練 Word2Vec 模型教程](https://www.TensorFlow.org/tutorials/text/word2vec)。
* 使用 **gensim** 框架僅需幾行代碼即可訓練最常用的嵌入，詳情請參閱[此文檔](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html)。

## 🚀 [作業：訓練 Skip-Gram 模型](lab/README.md)

在實驗中，我們挑戰你修改本課的代碼來訓練 Skip-Gram 模型，而不是 CBoW。[閱讀詳情](lab/README.md)

**免責聲明**：  
本文件已使用人工智能翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。原始語言的文件應被視為具權威性的來源。對於重要資訊，建議使用專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或錯誤解釋概不負責。