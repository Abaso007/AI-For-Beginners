<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48fdd704d483e19bc3d7464074c9fcbe",
  "translation_date": "2025-08-24T21:15:13+00:00",
  "source_file": "lessons/3-NeuralNetworks/04-OwnFramework/lab/README.md",
  "language_code": "ja"
}
-->
# MNIST分類を自作フレームワークで実施

[AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners)のラボ課題。

## 課題

1層、2層、3層のパーセプトロンを使用して、MNIST手書き数字分類問題を解決してください。レッスンで開発したニューラルネットワークフレームワークを使用します。

## 開始ノートブック

ラボを始めるには、[MyFW_MNIST.ipynb](../../../../../../lessons/3-NeuralNetworks/04-OwnFramework/lab/MyFW_MNIST.ipynb)を開いてください。

## 質問

このラボの結果として、以下の質問に答えてみてください：

- 層間の活性化関数はネットワークの性能に影響を与えますか？
- このタスクには2層または3層のネットワークが必要ですか？
- ネットワークのトレーニング中に問題が発生しましたか？特に層の数が増えるにつれて。
- トレーニング中にネットワークの重みはどのように振る舞いますか？エポックごとの重みの最大絶対値をプロットして、その関係を理解してみてください。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知おきください。元の言語で記載された文書が公式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤認について、当方は一切の責任を負いません。