<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7bd8dc72040e98e35e7225e34058cd4e",
  "translation_date": "2025-08-24T22:06:42+00:00",
  "source_file": "lessons/6-Other/22-DeepRL/lab/README.md",
  "language_code": "hk"
}
-->
## 環境介紹

Mountain Car 環境由一輛被困在山谷中的車組成。你的目標是跳出山谷並到達旗幟的位置。你可以執行的動作包括向左加速、向右加速，或者什麼都不做。你可以觀察到車在 x 軸上的位置以及速度。

## 開始筆記本

通過打開 [MountainCar.ipynb](../../../../../../lessons/6-Other/22-DeepRL/lab/MountainCar.ipynb) 開始這個實驗。

## 重點

在這個實驗中，你應該學到將 RL 演算法應用到一個新環境通常是相當直接的，因為 OpenAI Gym 的所有環境都具有相同的介面，而演算法本身並不會過多依賴於環境的特性。你甚至可以重新結構化 Python 程式碼，以便將任何環境作為參數傳遞給 RL 演算法。

**免責聲明**：  
本文件已使用人工智能翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原文文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤釋不承擔責任。