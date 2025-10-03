<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0ff47c5596afbd32ef2cb6bd68d08c54",
  "translation_date": "2025-10-03T10:34:27+00:00",
  "source_file": "README.md",
  "language_code": "mo"
}
-->
[![GitHub license](https://img.shields.io/github/license/microsoft/AI-For-Beginners.svg)](https://github.com/microsoft/AI-For-Beginners/blob/main/LICENSE)  
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/AI-For-Beginners.svg)](https://GitHub.com/microsoft/AI-For-Beginners/graphs/contributors/)  
[![GitHub issues](https://img.shields.io/github/issues/microsoft/AI-For-Beginners.svg)](https://GitHub.com/microsoft/AI-For-Beginners/issues/)  
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/AI-For-Beginners.svg)](https://GitHub.com/microsoft/AI-For-Beginners/pulls/)  
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)  

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/AI-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/AI-For-Beginners/watchers/)  
[![GitHub forks](https://img.shields.io/github/forks/microsoft/AI-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/AI-For-Beginners/network/)  
[![GitHub stars](https://img.shields.io/github/stars/microsoft/AI-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/AI-For-Beginners/stargazers/)  
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/microsoft/ai-for-beginners/HEAD)  
[![Gitter](https://badges.gitter.im/Microsoft/ai-for-beginners.svg)](https://gitter.im/Microsoft/ai-for-beginners?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)  

[![](https://dcbadge.vercel.app/api/server/ByRwuEEgH4)](https://discord.gg/zxKYvhSnVp?WT.mc_id=academic-000002-leestott)  

# 人工智慧入門課程 - 教學大綱  

|![Sketchnote by @girlie_mac https://twitter.com/girlie_mac](../../translated_images/ai-overview.0857791951d19500d0ef8b803d77110c738dcafc52306e6d68724742cd4af167.mo.png)|  
|:---:|  
| 人工智慧入門 - _由 [@girlie_mac](https://twitter.com/girlie_mac) 繪製的手繪筆記_ |  

透過我們的 12 週、24 節課程，探索**人工智慧**（AI）的世界！課程包含實用的教學內容、測驗和實驗室練習。這是一個適合初學者的課程，涵蓋了像 TensorFlow 和 PyTorch 等工具，以及人工智慧的倫理問題。  

### 🌐 多語言支援  

#### 透過 GitHub Action 支援（自動化且始終保持最新）  

[法文](../fr/README.md) | [西班牙文](../es/README.md) | [德文](../de/README.md) | [俄文](../ru/README.md) | [阿拉伯文](../ar/README.md) | [波斯文 (Farsi)](../fa/README.md) | [烏爾都文](../ur/README.md) | [中文 (簡體)](../zh/README.md) | [中文 (繁體，澳門)](./README.md) | [中文 (繁體，香港)](../hk/README.md) | [中文 (繁體，台灣)](../tw/README.md) | [日文](../ja/README.md) | [韓文](../ko/README.md) | [印地文](../hi/README.md) | [孟加拉文](../bn/README.md) | [馬拉地文](../mr/README.md) | [尼泊爾文](../ne/README.md) | [旁遮普文 (Gurmukhi)](../pa/README.md) | [葡萄牙文 (葡萄牙)](../pt/README.md) | [葡萄牙文 (巴西)](../br/README.md) | [意大利文](../it/README.md) | [波蘭文](../pl/README.md) | [土耳其文](../tr/README.md) | [希臘文](../el/README.md) | [泰文](../th/README.md) | [瑞典文](../sv/README.md) | [丹麥文](../da/README.md) | [挪威文](../no/README.md) | [芬蘭文](../fi/README.md) | [荷蘭文](../nl/README.md) | [希伯來文](../he/README.md) | [越南文](../vi/README.md) | [印尼文](../id/README.md) | [馬來文](../ms/README.md) | [塔加洛語 (菲律賓)](../tl/README.md) | [斯瓦希里文](../sw/README.md) | [匈牙利文](../hu/README.md) | [捷克文](../cs/README.md) | [斯洛伐克文](../sk/README.md) | [羅馬尼亞文](../ro/README.md) | [保加利亞文](../bg/README.md) | [塞爾維亞文 (西里爾字母)](../sr/README.md) | [克羅埃西亞文](../hr/README.md) | [斯洛文尼亞文](../sl/README.md) | [烏克蘭文](../uk/README.md) | [緬甸文](../my/README.md)  

**如果您希望支持其他語言翻譯，請參考 [此處](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md) 列出的語言。**  

## 加入社群  
[![Azure AI Discord](https://dcbadge.limes.pink/api/server/kzRShWzttr)](https://discord.gg/kzRShWzttr)  

## 您將學到什麼  

**[課程思維導圖](http://soshnikov.com/courses/ai-for-beginners/mindmap.html)**  

在這門課程中，您將學到：  

* 不同的人工智慧方法，包括傳統的符號方法，例如**知識表示**和推理（[GOFAI](https://en.wikipedia.org/wiki/Symbolic_artificial_intelligence)）。  
* **神經網絡**和**深度學習**，這是現代人工智慧的核心。我們將使用兩個最受歡迎的框架 [TensorFlow](http://Tensorflow.org) 和 [PyTorch](http://pytorch.org) 的程式碼來說明這些重要主題的概念。  
* 用於處理影像和文字的**神經網絡架構**。我們將涵蓋一些近期的模型，但可能不包括最前沿的技術。  
* 不太常見的人工智慧方法，例如**基因演算法**和**多代理系統**。  

本課程不會涵蓋以下內容：  

> [在 Microsoft Learn 集合中找到本課程的所有額外資源](https://learn.microsoft.com/en-us/collections/7w28iy2xrqzdj0?WT.mc_id=academic-77998-bethanycheum)  

* **人工智慧在商業中的應用案例**。建議參加 Microsoft Learn 上的 [Introduction to AI for business users](https://docs.microsoft.com/learn/paths/introduction-ai-for-business-users/?WT.mc_id=academic-77998-bethanycheum) 學習路徑，或由 [INSEAD](https://www.insead.edu/) 合作開發的 [AI Business School](https://www.microsoft.com/ai/ai-business-school/?WT.mc_id=academic-77998-bethanycheum)。  
* **經典機器學習**，這部分內容已在我們的 [Machine Learning for Beginners Curriculum](http://github.com/Microsoft/ML-for-Beginners) 中詳細描述。  
* 使用 **[Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=academic-77998-bethanycheum)** 構建的實際人工智慧應用。建議從 Microsoft Learn 的模組開始學習，例如 [vision](https://docs.microsoft.com/learn/paths/create-computer-vision-solutions-azure-cognitive-services/?WT.mc_id=academic-77998-bethanycheum)、[natural language processing](https://docs.microsoft.com/learn/paths/explore-natural-language-processing/?WT.mc_id=academic-77998-bethanycheum)、**[Generative AI with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/paths/develop-ai-solutions-azure-openai/?WT.mc_id=academic-77998-bethanycheum)** 等。  
* 特定的機器學習**雲端框架**，例如 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/?WT.mc_id=academic-77998-bethanycheum)、[Microsoft Fabric](https://learn.microsoft.com/en-us/training/paths/get-started-fabric/?WT.mc_id=academic-77998-bethanycheum) 或 [Azure Databricks](https://docs.microsoft.com/learn/paths/data-engineer-azure-databricks?WT.mc_id=academic-77998-bethanycheum)。建議使用 [Build and operate machine learning solutions with Azure Machine Learning](https://docs.microsoft.com/learn/paths/build-ai-solutions-with-azure-ml-service/?WT.mc_id=academic-77998-bethanycheum) 和 [Build and Operate Machine Learning Solutions with Azure Databricks](https://docs.microsoft.com/learn/paths/build-operate-machine-learning-solutions-azure-databricks/?WT.mc_id=academic-77998-bethanycheum) 學習路徑。  
* **對話式人工智慧**和**聊天機器人**。有一個單獨的 [Create conversational AI solutions](https://docs.microsoft.com/learn/paths/create-conversational-ai-solutions/?WT.mc_id=academic-77998-bethanycheum) 學習路徑，您也可以參考 [這篇部落格文章](https://soshnikov.com/azure/hello-bot-conversational-ai-on-microsoft-platform/) 了解更多細節。  
* **深度學習的數學基礎**。建議閱讀 Ian Goodfellow、Yoshua Bengio 和 Aaron Courville 所著的 [Deep Learning](https://www.amazon.com/Deep-Learning-Adaptive-Computation-Machine/dp/0262035618)，該書也可在線上獲取：[https://www.deeplearningbook.org/](https://www.deeplearningbook.org/)。  

若想輕鬆入門 _AI in the Cloud_ 主題，您可以考慮參加 [Get started with artificial intelligence on Azure](https://docs.microsoft.com/learn/paths/get-started-with-artificial-intelligence-on-azure/?WT.mc_id=academic-77998-bethanycheum) 學習路徑。  

# 課程內容  

|     |                                                                 課程連結                                                                  |                                           PyTorch/Keras/TensorFlow                                          | 實驗室                                                            |  
| :-: | :------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------: | ------------------------------------------------------------------------------ |  
| 0  |                                 [課程設置](./lessons/0-course-setup/setup.md)                                 |                      [設置您的開發環境](./lessons/0-course-setup/how-to-run.md)                       |   |  
| I  |               [**人工智慧簡介**](./lessons/1-Intro/README.md)      | | |  
| 01  |       [人工智慧的簡介與歷史](./lessons/1-Intro/README.md)       |           -                            | -  |  
| II |              **符號人工智慧**              |  
| 02  |       [知識表示與專家系統](./lessons/2-Symbolic/README.md)       |            [專家系統](./lessons/2-Symbolic/Animals.ipynb) /  [本體論](./lessons/2-Symbolic/FamilyOntology.ipynb) /[概念圖](./lessons/2-Symbolic/MSConceptGraph.ipynb)                             |  |  
| III |                        [**神經網絡簡介**](./lessons/3-NeuralNetworks/README.md) |||  
| 03  |                [感知器](./lessons/3-NeuralNetworks/03-Perceptron/README.md)                 |                       [筆記本](./lessons/3-NeuralNetworks/03-Perceptron/Perceptron.ipynb)                      | [實驗室](./lessons/3-NeuralNetworks/03-Perceptron/lab/README.md) |  
| 04  |                   [多層感知器與創建我們自己的框架](./lessons/3-NeuralNetworks/04-OwnFramework/README.md)                   |        [筆記本](./lessons/3-NeuralNetworks/04-OwnFramework/OwnFramework.ipynb)        | [實驗室](./lessons/3-NeuralNetworks/04-OwnFramework/lab/README.md) |  
| 05  |            [框架入門（PyTorch/TensorFlow）及過度擬合](./lessons/3-NeuralNetworks/05-Frameworks/README.md)             |           [PyTorch](./lessons/3-NeuralNetworks/05-Frameworks/IntroPyTorch.ipynb) / [Keras](./lessons/3-NeuralNetworks/05-Frameworks/IntroKeras.ipynb) / [TensorFlow](./lessons/3-NeuralNetworks/05-Frameworks/IntroKerasTF.ipynb)             | [實驗](./lessons/3-NeuralNetworks/05-Frameworks/lab/README.md) |
| IV  |            [**電腦視覺**](./lessons/4-ComputerVision/README.md)             | [PyTorch](https://docs.microsoft.com/learn/modules/intro-computer-vision-pytorch/?WT.mc_id=academic-77998-cacaste) / [TensorFlow](https://docs.microsoft.com/learn/modules/intro-computer-vision-TensorFlow/?WT.mc_id=academic-77998-cacaste)| [探索 Microsoft Azure 的電腦視覺](https://learn.microsoft.com/en-us/collections/7w28iy2xrqzdj0?WT.mc_id=academic-77998-bethanycheum) |
| 06  |            [電腦視覺入門. OpenCV](./lessons/4-ComputerVision/06-IntroCV/README.md)             |           [筆記本](./lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)         | [實驗](./lessons/4-ComputerVision/06-IntroCV/lab/README.md) |
| 07  |            [卷積神經網絡](./lessons/4-ComputerVision/07-ConvNets/README.md) &  [CNN 架構](./lessons/4-ComputerVision/07-ConvNets/CNN_Architectures.md)             |           [PyTorch](./lessons/4-ComputerVision/07-ConvNets/ConvNetsPyTorch.ipynb) /[TensorFlow](./lessons/4-ComputerVision/07-ConvNets/ConvNetsTF.ipynb)             | [實驗](./lessons/4-ComputerVision/07-ConvNets/lab/README.md) |
| 08  |            [預訓練網絡及遷移學習](./lessons/4-ComputerVision/08-TransferLearning/README.md) 和 [訓練技巧](./lessons/4-ComputerVision/08-TransferLearning/TrainingTricks.md)             |           [PyTorch](./lessons/4-ComputerVision/08-TransferLearning/TransferLearningPyTorch.ipynb) / [TensorFlow](./lessons/3-NeuralNetworks/05-Frameworks/IntroKerasTF.ipynb)             | [實驗](./lessons/4-ComputerVision/08-TransferLearning/lab/README.md) |
| 09  |            [自編碼器及變分自編碼器 (VAEs)](./lessons/4-ComputerVision/09-Autoencoders/README.md)             |           [PyTorch](./lessons/4-ComputerVision/09-Autoencoders/AutoEncodersPyTorch.ipynb) / [TensorFlow](./lessons/4-ComputerVision/09-Autoencoders/AutoencodersTF.ipynb)             |  |
| 10  |            [生成對抗網絡 (GANs) 及藝術風格轉移](./lessons/4-ComputerVision/10-GANs/README.md)             |           [PyTorch](./lessons/4-ComputerVision/10-GANs/GANPyTorch.ipynb) / [TensorFlow](./lessons/4-ComputerVision/10-GANs/GANTF.ipynb)             |  |
| 11  |            [物件偵測](./lessons/4-ComputerVision/11-ObjectDetection/README.md)             |         [TensorFlow](./lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)             | [實驗](./lessons/4-ComputerVision/11-ObjectDetection/lab/README.md) |
| 12  |            [語義分割. U-Net](./lessons/4-ComputerVision/12-Segmentation/README.md)             |           [PyTorch](./lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationPytorch.ipynb) / [TensorFlow](./lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationTF.ipynb)             |  |
| V  |            [**自然語言處理**](./lessons/5-NLP/README.md)             | [PyTorch](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-pytorch/?WT.mc_id=academic-77998-cacaste) /[TensorFlow](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-TensorFlow/?WT.mc_id=academic-77998-cacaste) | [探索 Microsoft Azure 的自然語言處理](https://learn.microsoft.com/en-us/collections/7w28iy2xrqzdj0?WT.mc_id=academic-77998-bethanycheum)|
| 13  |            [文本表示. Bow/TF-IDF](./lessons/5-NLP/13-TextRep/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/13-TextRep/TextRepresentationPyTorch.ipynb) / [TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/13-TextRep/TextRepresentationTF.ipynb)             | |
| 14  |            [語義詞嵌入. Word2Vec 和 GloVe](./lessons/5-NLP/14-Embeddings/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/14-Embeddings/EmbeddingsPyTorch.ipynb) / [TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/14-Embeddings/EmbeddingsTF.ipynb)             |  |
| 15  |            [語言建模. 訓練自己的嵌入](./lessons/5-NLP/15-LanguageModeling/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/15-LanguageModeling/CBoW-PyTorch.ipynb) / [TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/15-LanguageModeling/CBoW-TF.ipynb)             | [實驗](./lessons/5-NLP/15-LanguageModeling/lab/README.md) |
| 16  |            [循環神經網絡 (RNN)](./lessons/5-NLP/16-RNN/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/16-RNN/RNNPyTorch.ipynb) / [TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/16-RNN/RNNTF.ipynb)             |  |
| 17  |            [生成型循環網絡](./lessons/5-NLP/17-GenerativeNetworks/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/17-GenerativeNetworks/GenerativePyTorch.ipynb) / [TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/17-GenerativeNetworks/GenerativeTF.ipynb)             | [實驗](./lessons/5-NLP/17-GenerativeNetworks/lab/README.md) |
| 18  |            [Transformer. BERT](./lessons/5-NLP/18-Transformers/README.md)             |           [PyTorch](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/18-Transformers/TransformersPyTorch.ipynb) /[TensorFlow](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/5-NLP/18-Transformers/TransformersTF.ipynb)             |  |
| 19  |            [命名實體識別 (NER)](./lessons/5-NLP/19-NER/README.md)             |           [TensorFlow](https://microsoft.github.io/AI-For-Beginners/lessons/5-NLP/19-NER/NER-TF.ipynb)             | [實驗](./lessons/5-NLP/19-NER/lab/README.md) |
| 20  |            [大型語言模型、提示編程及少樣本任務](./lessons/5-NLP/20-LangModels/README.md)             |           [PyTorch](https://microsoft.github.io/AI-For-Beginners/lessons/5-NLP/20-LangModels/GPT-PyTorch.ipynb) | |
| VI |            **其他 AI 技術** || |
| 21  |            [遺傳算法](./lessons/6-Other/21-GeneticAlgorithms/README.md)             |           [筆記本](./lessons/6-Other/21-GeneticAlgorithms/Genetic.ipynb) | |
| 22  |            [深度強化學習](./lessons/6-Other/22-DeepRL/README.md)             |           [PyTorch](./lessons/6-Other/22-DeepRL/CartPole-RL-PyTorch.ipynb) /[TensorFlow](./lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb)             | [實驗](./lessons/6-Other/22-DeepRL/lab/README.md) |
| 23  |            [多代理系統](./lessons/6-Other/23-MultiagentSystems/README.md)             |  | |
| VII |            **AI 倫理** | | |
| 24  |            [AI 倫理及負責任的 AI](./lessons/7-Ethics/README.md)             |           [Microsoft Learn: 負責任的 AI 原則](https://docs.microsoft.com/learn/paths/responsible-ai-business-principles/?WT.mc_id=academic-77998-cacaste) | |
| IX  |            **額外內容** | | |
| 25  |            [多模態網絡、CLIP 和 VQGAN](./lessons/X-Extras/X1-MultiModal/README.md)             |           [筆記本](./lessons/X-Extras/X1-MultiModal/Clip.ipynb)    | |

## 每節課包含

* 預讀材料
* 可執行的 Jupyter 筆記本，通常針對特定框架（**PyTorch** 或 **TensorFlow**）。可執行的筆記本也包含大量理論材料，因此要理解主題，至少需要通過一個版本的筆記本（PyTorch 或 TensorFlow）。
* **實驗**：部分主題提供實驗，讓您有機會將所學的知識應用於特定問題。
* 部分章節包含指向 [**MS Learn**](https://learn.microsoft.com/en-us/collections/7w28iy2xrqzdj0?WT.mc_id=academic-77998-bethanycheum) 模組的連結，涵蓋相關主題。

## 開始學習

### 🎯 AI 新手？從這裡開始！

如果您完全是 AI 新手，並希望快速上手實例，請查看我們的 [**適合初學者的範例**](./examples/README.md)！這些範例包括：

- 🌟 **Hello AI World** - 您的第一個 AI 程式（模式識別）
- 🧠 **簡單神經網絡** - 從零開始構建神經網絡  
- 🖼️ **圖像分類器** - 帶有詳細註解的圖像分類
- 💬 **文本情感分析** - 分析正面/負面文本

這些範例旨在幫助您在深入完整課程之前理解 AI 概念。

### 📚 完整課程設置

- 我們已創建 [設置課程](./lessons/0-course-setup/setup.md)，幫助您設置開發環境。 - 對於教育工作者，我們也創建了 [課程設置指南](./lessons/0-course-setup/for-teachers.md)！
- 如何 [在 VSCode 或 Codepace 中運行程式碼](./lessons/0-course-setup/how-to-run.md)

請按照以下步驟操作：

Fork 此倉庫：點擊此頁面右上角的 "Fork" 按鈕。

Clone 此倉庫：`git clone https://github.com/microsoft/AI-For-Beginners.git`
別忘了給這個倉庫加星（🌟），以便日後更容易找到。

## 與其他學習者交流

加入我們的[官方 AI Discord 伺服器](https://aka.ms/genai-discord?WT.mc_id=academic-105485-bethanycheum)，與其他正在學習本課程的學員交流並建立聯繫，還可以獲得支持。

如果在構建過程中有產品反饋或問題，請訪問我們的[Azure AI Foundry 開發者論壇](https://aka.ms/foundry/forum)。

## 測驗

> **關於測驗的說明**：所有測驗都包含在 etc\quiz-app 的 Quiz-app 資料夾中，或者可以[在線訪問](https://ff-quizzes.netlify.app/)。測驗在課程中有鏈接，測驗應用可以在本地運行或部署到 Azure；請按照 `quiz-app` 資料夾中的指示操作。測驗正在逐步進行本地化。

## 尋求幫助

您有建議或發現拼寫或代碼錯誤嗎？請提出 Issue 或創建 Pull Request。

## 特別感謝

* **✍️ 主要作者：** [Dmitry Soshnikov](http://soshnikov.com)，博士
* **🔥 編輯：** [Jen Looper](https://twitter.com/jenlooper)，博士
* **🎨 手繪筆記插畫師：** [Tomomi Imura](https://twitter.com/girlie_mac)
* **✅ 測驗創作者：** [Lateefah Bello](https://github.com/CinnamonXI)，[MLSA](https://studentambassadors.microsoft.com/)
* **🙏 核心貢獻者：** [Evgenii Pishchik](https://github.com/Pe4enIks)

## 其他課程

我們的團隊還製作了其他課程！查看以下內容：

- [生成式 AI 入門](https://aka.ms/genai-beginners)
- [生成式 AI 入門 .NET](https://github.com/microsoft/Generative-AI-for-beginners-dotnet)
- [使用 JavaScript 的生成式 AI](https://github.com/microsoft/generative-ai-with-javascript)
- [使用 Java 的生成式 AI](https://github.com/microsoft/Generative-AI-for-beginners-java)
- [AI 入門](https://aka.ms/ai-beginners)
- [數據科學入門](https://aka.ms/datascience-beginners)
- [機器學習入門](https://aka.ms/ml-beginners)
- [網絡安全入門](https://github.com/microsoft/Security-101)
- [Web 開發入門](https://aka.ms/webdev-beginners)
- [物聯網入門](https://aka.ms/iot-beginners)
- [XR 開發入門](https://github.com/microsoft/xr-development-for-beginners)
- [掌握 GitHub Copilot 的智能使用](https://github.com/microsoft/Mastering-GitHub-Copilot-for-Paired-Programming)
- [為 C#/.NET 開發者掌握 GitHub Copilot](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers)
- [選擇你的 Copilot 冒險](https://github.com/microsoft/CopilotAdventures)

## 獲取幫助

如果您遇到困難或對構建 AI 應用有任何疑問，請加入：

[![Azure AI Foundry Discord](https://img.shields.io/badge/Discord-Azure_AI_Foundry_Community_Discord-blue?style=for-the-badge&logo=discord&color=5865f2&logoColor=fff)](https://aka.ms/foundry/discord)

如果在構建過程中有產品反饋或錯誤，請訪問：

[![Azure AI Foundry Developer Forum](https://img.shields.io/badge/GitHub-Azure_AI_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)

---

**免責聲明**：  
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。儘管我們努力確保翻譯的準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於關鍵資訊，建議使用專業人工翻譯。我們對因使用此翻譯而產生的任何誤解或錯誤解釋不承擔責任。