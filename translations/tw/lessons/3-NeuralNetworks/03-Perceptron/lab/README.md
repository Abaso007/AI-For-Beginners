<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7336583e4630220c835335da640016db",
  "translation_date": "2025-08-24T22:10:49+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "tw"
}
-->
# 使用感知器進行多類別分類

來自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的實驗作業。

## 任務

使用我們在本課中為 MNIST 手寫數字的二元分類所開發的程式碼，創建一個多類別分類器，能夠識別任意數字。計算訓練集和測試集的分類準確率，並輸出混淆矩陣。

## 提示

1. 對於每個數字，創建一個二元分類器的數據集，將其定義為「該數字 vs. 其他所有數字」
1. 訓練 10 個不同的感知器進行二元分類（每個數字一個感知器）
1. 定義一個函數來分類輸入的數字

> **提示**：如果我們將所有 10 個感知器的權重組合成一個矩陣，我們應該能夠通過一次矩陣乘法將所有 10 個感知器應用於輸入數字。然後，只需對輸出應用 `argmax` 操作即可找到最可能的數字。

## 起始筆記本

通過打開 [PerceptronMultiClass.ipynb](../../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb) 開始實驗。

**免責聲明**：  
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原始語言的文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對於因使用此翻譯而引起的任何誤解或錯誤解釋概不負責。