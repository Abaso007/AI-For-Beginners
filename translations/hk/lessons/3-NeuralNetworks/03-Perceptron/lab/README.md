<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ba5d1eb353d20d3e7181066b3c424b99",
  "translation_date": "2025-08-31T09:20:54+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "hk"
}
-->
# 使用感知器進行多類別分類

來自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的實驗課題。

## 任務

利用我們在本課中為 MNIST 手寫數字進行二元分類所開發的程式碼，創建一個多類別分類器，能夠識別任意數字。計算訓練集和測試集的分類準確率，並輸出混淆矩陣。

## 提示

1. 對於每個數字，創建一個二元分類的數據集，將「該數字」與「所有其他數字」進行分類。
1. 訓練 10 個不同的感知器進行二元分類（每個數字對應一個感知器）。
1. 定義一個函數來分類輸入的數字。

> **提示**: 如果我們將所有 10 個感知器的權重組合成一個矩陣，我們應該能夠通過一次矩陣乘法將所有 10 個感知器應用到輸入數字上。最可能的數字可以通過對輸出應用 `argmax` 操作來找到。

## 起始筆記本

通過打開 [PerceptronMultiClass.ipynb](PerceptronMultiClass.ipynb) 開始實驗課題。

---

**免責聲明**：  
本文件已使用人工智能翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。儘管我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於重要信息，建議使用專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或錯誤解釋概不負責。