<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7765935c35fcee69b9fe2d0cfd6963e2",
  "translation_date": "2025-08-26T09:52:46+00:00",
  "source_file": "lessons/4-ComputerVision/08-TransferLearning/lab/README.md",
  "language_code": "mo"
}
-->
# 使用遷移學習對牛津寵物進行分類

來自 [AI 初學者課程](https://github.com/microsoft/ai-for-beginners) 的實驗作業。

## 任務

假設你需要開發一個寵物托育應用程式，用來記錄所有的寵物。這樣的應用程式其中一個很棒的功能就是能夠透過照片自動辨識寵物的品種。在這次作業中，我們將使用遷移學習來對 [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) 寵物數據集中的真實寵物圖片進行分類。

## 數據集

我們將使用原始的 [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) 寵物數據集，該數據集包含 35 種不同品種的狗和貓。

要下載數據集，請使用以下程式碼片段：

```python
!wget https://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz
!tar xfz images.tar.gz
!rm images.tar.gz
```

## 啟動筆記本

開始實驗，打開 [OxfordPets.ipynb](../../../../../../lessons/4-ComputerVision/08-TransferLearning/lab/OxfordPets.ipynb)

## 重點

遷移學習和預訓練網絡使我們能夠相對輕鬆地解決現實世界中的圖像分類問題。然而，預訓練網絡在處理相似類型的圖像時效果很好，但如果我們開始分類非常不同的圖像（例如醫學影像），結果可能會大幅下降。

**免責聲明**：  
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們努力確保翻譯的準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於關鍵信息，建議使用專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤釋不承擔責任。