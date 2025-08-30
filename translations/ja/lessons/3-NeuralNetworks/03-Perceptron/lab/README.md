<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ba5d1eb353d20d3e7181066b3c424b99",
  "translation_date": "2025-08-30T08:44:02+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "ja"
}
-->
# パーセプトロンによる多クラス分類

[AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) のラボ課題。

## 課題

このレッスンで開発したコードを使用して、MNIST手書き数字の二値分類を行い、任意の数字を認識できる多クラス分類器を作成してください。訓練データセットとテストデータセットで分類精度を計算し、混同行列を出力してください。

## ヒント

1. 各数字について、「この数字 vs. 他のすべての数字」の二値分類用データセットを作成する
1. 二値分類用に10個の異なるパーセプトロンを訓練する（各数字に1つずつ）
1. 入力された数字を分類する関数を定義する

> **ヒント**: 10個のパーセプトロンの重みを1つの行列にまとめれば、入力された数字に対して1回の行列積で全てのパーセプトロンを適用することができます。その後、出力に対して `argmax` 操作を適用することで、最も可能性の高い数字を見つけることができます。

## スタートノートブック

[PerceptronMultiClass.ipynb](PerceptronMultiClass.ipynb) を開いてラボを開始してください。

---

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知ください。元の言語で記載された文書が正式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤解釈について、当方は一切の責任を負いません。