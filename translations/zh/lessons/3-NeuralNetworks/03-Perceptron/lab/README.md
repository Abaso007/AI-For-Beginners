<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ba5d1eb353d20d3e7181066b3c424b99",
  "translation_date": "2025-08-31T09:19:26+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "zh"
}
-->
# 使用感知器进行多类别分类

来自 [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) 的实验任务。

## 任务

利用我们在本课中开发的用于 MNIST 手写数字二分类的代码，创建一个能够识别任意数字的多类别分类器。计算训练集和测试集上的分类准确率，并打印出混淆矩阵。

## 提示

1. 对于每个数字，创建一个用于二分类的 "该数字 vs. 其他所有数字" 的数据集。
2. 为二分类训练 10 个不同的感知器（每个数字对应一个）。
3. 定义一个函数，用于对输入数字进行分类。

> **提示**：如果将所有 10 个感知器的权重组合成一个矩阵，我们可以通过一次矩阵乘法将所有 10 个感知器应用到输入数字上。然后，只需对输出应用 `argmax` 操作，就能找到最可能的数字。

## 起始笔记本

通过打开 [PerceptronMultiClass.ipynb](PerceptronMultiClass.ipynb) 开始实验。

---

**免责声明**：  
本文档使用AI翻译服务[Co-op Translator](https://github.com/Azure/co-op-translator)进行翻译。尽管我们努力确保准确性，但请注意，自动翻译可能包含错误或不准确之处。应以原始语言的文档作为权威来源。对于关键信息，建议使用专业人工翻译。因使用本翻译而导致的任何误解或误读，我们概不负责。