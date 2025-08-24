<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd10f434e444bce61b7f97eeb1ff6a55",
  "translation_date": "2025-08-24T20:30:54+00:00",
  "source_file": "lessons/5-NLP/19-NER/README.md",
  "language_code": "zh"
}
-->
# 命名实体识别

到目前为止，我们主要集中在一个自然语言处理任务——分类。然而，还有其他可以通过神经网络完成的自然语言处理任务。其中一个任务是**[命名实体识别](https://wikipedia.org/wiki/Named-entity_recognition)** (NER)，它处理识别文本中的特定实体，例如地点、人物姓名、日期时间区间、化学公式等。

## [课前测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/119)

## 使用 NER 的示例

假设你想开发一个类似于亚马逊 Alexa 或谷歌助手的自然语言聊天机器人。智能聊天机器人的工作方式是通过对输入句子进行文本分类来“理解”用户的需求。分类的结果是所谓的**意图**，它决定了聊天机器人应该执行的操作。

<img alt="Bot NER" src="images/bot-ner.png" width="50%"/>

> 图片由作者提供

然而，用户可能会在短语中提供一些参数。例如，当询问天气时，她可能会指定一个地点或日期。机器人应该能够理解这些实体，并在执行操作之前相应地填充参数槽。这正是 NER 的作用所在。

> ✅ 另一个例子是[分析科学医学论文](https://soshnikov.com/science/analyzing-medical-papers-with-azure-and-text-analytics-for-health/)。我们需要寻找的主要内容是特定的医学术语，例如疾病和医学物质。虽然少量疾病可能可以通过子字符串搜索提取，但更复杂的实体，例如化学化合物和药物名称，则需要更复杂的方法。

## NER 作为标记分类

NER 模型本质上是**标记分类模型**，因为对于每个输入标记，我们需要决定它是否属于某个实体，如果属于——属于哪个实体类别。

考虑以下论文标题：

**三尖瓣返流**和**碳酸锂**在新生儿中的**毒性**。

这里的实体是：

* 三尖瓣返流是一种疾病 (`DIS`)
* 碳酸锂是一种化学物质 (`CHEM`)
* 毒性也是一种疾病 (`DIS`)

注意，一个实体可以跨越多个标记。而且，如本例所示，我们需要区分两个连续的实体。因此，通常为每个实体使用两个类别——一个指定实体的第一个标记（通常使用 `B-` 前缀，表示**开始**），另一个表示实体的延续部分（`I-`，表示**内部标记**）。我们还使用 `O` 作为类别来表示所有**其他**标记。这种标记标注被称为 [BIO 标注](https://en.wikipedia.org/wiki/Inside%E2%80%93outside%E2%80%93beginning_(tagging))（或 IOB）。标注后，我们的标题将如下所示：

标记 | 标注
------|-----
三尖瓣 | B-DIS
返流 | I-DIS
和 | O
碳酸 | B-CHEM
锂 | I-CHEM
毒性 | B-DIS
在 | O
新生儿 | O
中 | O
的 | O
毒性 | O
. | O

由于我们需要在标记和类别之间建立一一对应关系，我们可以从下图中训练一个最右侧的**多对多**神经网络模型：

![展示常见循环神经网络模式的图片。](../../../../../translated_images/unreasonable-effectiveness-of-rnn.541ead816778f42dce6c42d8a56c184729aa2378d059b851be4ce12b993033df.zh.jpg)

> *图片来自 [这篇博客文章](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) 作者 [Andrej Karpathy](http://karpathy.github.io/)。NER 标记分类模型对应于此图片中的最右侧网络架构。*

## 训练 NER 模型

由于 NER 模型本质上是一个标记分类模型，我们可以使用我们已经熟悉的 RNN 来完成这个任务。在这种情况下，每个循环网络块将返回标记 ID。以下示例笔记本展示了如何训练 LSTM 进行标记分类。

## ✍️ 示例笔记本：NER

通过以下笔记本继续学习：

* [使用 TensorFlow 的 NER](../../../../../lessons/5-NLP/19-NER/NER-TF.ipynb)

## 总结

NER 模型是一种**标记分类模型**，这意味着它可以用于执行标记分类。这是自然语言处理中的一个非常常见的任务，帮助识别文本中的特定实体，包括地点、姓名、日期等。

## 🚀 挑战

完成以下链接的作业，训练一个用于医学术语的命名实体识别模型，然后尝试在不同的数据集上应用它。

## [课后测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/219)

## 复习与自学

阅读博客 [循环神经网络的非凡有效性](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)，并按照文章中的进一步阅读部分加深你的知识。

## [作业](lab/README.md)

在本课的作业中，你需要训练一个医学实体识别模型。你可以从本课描述的 LSTM 模型训练开始，然后继续使用 BERT 转换器模型。阅读[说明](lab/README.md)以获取所有详细信息。

**免责声明**：  
本文档使用AI翻译服务 [Co-op Translator](https://github.com/Azure/co-op-translator) 进行翻译。尽管我们努力确保翻译的准确性，但请注意，自动翻译可能包含错误或不准确之处。应以原始语言的文档作为权威来源。对于关键信息，建议使用专业人工翻译。因使用本翻译而引起的任何误解或误读，我们概不负责。