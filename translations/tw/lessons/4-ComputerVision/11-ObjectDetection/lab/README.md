<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ad568d55ae65c856fe929fc2b278510a",
  "translation_date": "2025-08-24T21:58:40+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/lab/README.md",
  "language_code": "tw"
}
-->
# 使用 Hollywood Heads 資料集進行頭部檢測

來自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的實驗作業。

## 任務

在監控攝影機的影片流中計算人數是一項重要的任務，這可以幫助我們估算商店的訪客數量、餐廳的繁忙時段等。為了解決這個任務，我們需要能夠從不同角度檢測出人類的頭部。為了訓練能夠檢測人類頭部的物件檢測模型，我們可以使用 [Hollywood Heads 資料集](https://www.di.ens.fr/willow/research/headdetection/)。

## 資料集

[Hollywood Heads 資料集](https://www.di.ens.fr/willow/research/headdetection/release/HollywoodHeads.zip) 包含 369,846 個人類頭部的標註，這些標註來自 224,740 幅好萊塢電影的影格。該資料集以 [PASCAL VOC](https://host.robots.ox.ac.uk/pascal/VOC/) 格式提供，其中每張圖片都有一個對應的 XML 描述檔案，格式如下：

```xml
<annotation>
	<folder>HollywoodHeads</folder>
	<filename>mov_021_149390.jpeg</filename>
	<source>
		<database>HollywoodHeads 2015 Database</database>
		<annotation>HollywoodHeads 2015</annotation>
		<image>WILLOW</image>
	</source>
	<size>
		<width>608</width>
		<height>320</height>
		<depth>3</depth>
	</size>
	<segmented>0</segmented>
	<object>
		<name>head</name>
		<bndbox>
			<xmin>201</xmin>
			<ymin>1</ymin>
			<xmax>480</xmax>
			<ymax>263</ymax>
		</bndbox>
		<difficult>0</difficult>
	</object>
	<object>
		<name>head</name>
		<bndbox>
			<xmin>3</xmin>
			<ymin>4</ymin>
			<xmax>241</xmax>
			<ymax>285</ymax>
		</bndbox>
		<difficult>0</difficult>
	</object>
</annotation>
```

在這個資料集中，只有一種類別的物件 `head`，對於每個頭部，您可以獲取其邊界框的座標。您可以使用 Python 的相關函式庫來解析 XML，或者使用 [這個函式庫](https://pypi.org/project/pascal-voc/) 直接處理 PASCAL VOC 格式。

## 訓練物件檢測模型

您可以使用以下方法之一來訓練物件檢測模型：

* 使用 [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/quickstarts/object-detection?tabs=visual-studio&WT.mc_id=academic-77998-cacaste) 和其 Python API，在雲端以程式化方式訓練模型。Custom Vision 無法使用超過幾百張圖片來訓練模型，因此您可能需要限制資料集的大小。
* 使用 [Keras 教學範例](https://keras.io/examples/vision/retinanet/) 來訓練 RetunaNet 模型。
* 使用 [torchvision.models.detection.RetinaNet](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html) 中的內建模組進行訓練。

## 重點

物件檢測是業界中經常需要的任務。雖然有一些服務可以用來執行物件檢測（例如 [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/quickstarts/object-detection?tabs=visual-studio&WT.mc_id=academic-77998-cacaste)），但了解物件檢測的運作原理並能夠訓練自己的模型同樣重要。

**免責聲明**：  
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原始語言的文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或錯誤解釋概不負責。