<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "032bda5068f543d6c1fcb30c34231461",
  "translation_date": "2025-08-24T21:52:25+00:00",
  "source_file": "lessons/5-NLP/19-NER/lab/README.md",
  "language_code": "tw"
}
-->
# 命名實體識別 (NER)

來自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的實驗作業。

## 任務

在這個實驗中，你需要訓練一個針對醫學術語的命名實體識別模型。

## 數據集

為了訓練 NER 模型，我們需要一個正確標註的醫學實體數據集。[BC5CDR 數據集](https://biocreative.bioinformatics.udel.edu/tasks/biocreative-v/track-3-cdr/) 包含來自超過 1500 篇論文的疾病和化學實體標註。你可以在其網站註冊後下載該數據集。

BC5CDR 數據集的格式如下：

```
6794356|t|Tricuspid valve regurgitation and lithium carbonate toxicity in a newborn infant.
6794356|a|A newborn with massive tricuspid regurgitation, atrial flutter, congestive heart failure, and a high serum lithium level is described. This is the first patient to initially manifest tricuspid regurgitation and atrial flutter, and the 11th described patient with cardiac disease among infants exposed to lithium compounds in the first trimester of pregnancy. Sixty-three percent of these infants had tricuspid valve involvement. Lithium carbonate may be a factor in the increasing incidence of congenital heart disease when taken during early pregnancy. It also causes neurologic depression, cyanosis, and cardiac arrhythmia when consumed prior to delivery.
6794356	0	29	Tricuspid valve regurgitation	Disease	D014262
6794356	34	51	lithium carbonate	Chemical	D016651
6794356	52	60	toxicity	Disease	D064420
...
```

在這個數據集中，第一行和第二行分別是論文標題和摘要，接下來是個別的實體，包含其在標題+摘要區塊中的起始和結束位置。除了實體類型外，你還可以獲得該實體在某些醫學本體中的本體 ID。

你需要撰寫一些 Python 程式碼，將其轉換為 BIO 編碼格式。

## 網絡架構

第一次嘗試 NER 可以使用 LSTM 網絡，就像你在課堂中看到的範例一樣。然而，在 NLP 任務中，[Transformer 架構](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model))，特別是 [BERT 語言模型](https://en.wikipedia.org/wiki/BERT_(language_model))，通常能夠取得更好的結果。預訓練的 BERT 模型能夠理解語言的基本結構，並且可以用相對較小的數據集和計算成本進行特定任務的微調。

由於我們計劃將 NER 應用於醫學場景，因此使用在醫學文本上訓練的 BERT 模型是合理的選擇。Microsoft Research 發布了一個名為 [PubMedBERT][PubMedBERT] 的預訓練模型（[相關論文][PubMedBERT-Pub]），該模型使用 [PubMed](https://pubmed.ncbi.nlm.nih.gov/) 資料庫中的文本進行了微調。

訓練 Transformer 模型的事實標準是 [Hugging Face Transformers](https://huggingface.co/) 庫。該庫還包含一個由社群維護的預訓練模型庫，包括 PubMedBERT。要加載並使用此模型，我們只需要幾行程式碼：

```python
model_name = "microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract"
classes = ... # number of classes: 2*entities+1
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = BertForTokenClassification.from_pretrained(model_name, classes)
```

這段程式碼為我們提供了用於標記分類任務的 `model`（使用 `classes` 數量的類別），以及可以將輸入文本分割為標記的 `tokenizer` 物件。你需要將數據集轉換為 BIO 格式，並考慮到 PubMedBERT 的標記化方式。你可以參考 [這段 Python 程式碼](https://gist.github.com/shwars/580b55684be3328eb39ecf01b9cbbd88) 作為靈感。

## 收穫

這項任務非常接近於你在實際工作中可能遇到的任務，特別是當你希望從大量自然語言文本中獲取更多洞見時。在我們的案例中，我們可以將訓練好的模型應用於 [COVID 相關論文數據集](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge)，看看我們能夠獲得哪些洞見。[這篇部落格文章](https://soshnikov.com/science/analyzing-medical-papers-with-azure-and-text-analytics-for-health/) 和 [這篇論文](https://www.mdpi.com/2504-2289/6/1/4) 描述了可以使用 NER 在這些論文語料庫上進行的研究。

**免責聲明**：  
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原始語言的文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤讀概不負責。