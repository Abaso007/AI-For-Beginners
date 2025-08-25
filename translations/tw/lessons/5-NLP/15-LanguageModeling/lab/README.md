<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5130f01fdc5ebb83032b23d489027aac",
  "translation_date": "2025-08-24T21:47:39+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/lab/README.md",
  "language_code": "tw"
}
-->
# 訓練 Skip-Gram 模型

來自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的實驗作業。

## 任務

在本次實驗中，我們挑戰你使用 Skip-Gram 技術訓練 Word2Vec 模型。訓練一個帶有嵌入層的網絡，來預測 $N$ 個詞範圍內 Skip-Gram 窗口中的相鄰詞。你可以使用[本課程的代碼](../../../../../../lessons/5-NLP/15-LanguageModeling/CBoW-TF.ipynb)，稍作修改即可。

## 數據集

你可以使用任何一本書作為數據集。在 [Project Gutenberg](https://www.gutenberg.org/) 上可以找到許多免費文本，例如，這裡有 Lewis Carroll 的《愛麗絲夢遊仙境》的[直接鏈接](https://www.gutenberg.org/files/11/11-0.txt)。或者，你也可以使用莎士比亞的戲劇，以下代碼可以幫助你獲取：

```python
path_to_file = tf.keras.utils.get_file(
   'shakespeare.txt', 
   'https://storage.googleapis.com/download.tensorflow.org/data/shakespeare.txt')
text = open(path_to_file, 'rb').read().decode(encoding='utf-8')
```

## 探索！

如果你有時間並且想更深入了解這個主題，可以嘗試探索以下幾個方面：

* 嵌入層的大小如何影響結果？
* 不同的文本風格如何影響結果？
* 選擇幾個非常不同類型的詞及其同義詞，獲取它們的向量表示，應用 PCA 將維度降至 2，並在 2D 空間中繪製它們。你能看到任何模式嗎？

**免責聲明**：  
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原文文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或錯誤解釋概不負責。