<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "6bbd632dfe6c62e5f66bb51fd78c174a",
  "translation_date": "2025-09-23T08:04:56+00:00",
  "source_file": "lessons/6-Other/21-GeneticAlgorithms/README.md",
  "language_code": "mo"
}
-->
# 基因演算法

## [課前測驗](https://ff-quizzes.netlify.app/en/ai/quiz/41)

**基因演算法** (GA) 是基於一種**演化式方法**的人工智慧技術，透過模仿族群的演化過程來尋找特定問題的最佳解。此方法由 [John Henry Holland](https://wikipedia.org/wiki/John_Henry_Holland) 在1975年提出。

基因演算法的核心概念包括：

* 問題的有效解可以用**基因**來表示
* **交叉**允許我們將兩個解結合，生成新的有效解
* 使用某種**適應度函數**進行**選擇**，以篩選出更優的解
* 引入**突變**以打破局部最小值的限制，促進全局最佳化

若要實現基因演算法，需具備以下條件：

* 找到一種方法，使用**基因** g&in;&Gamma; 來編碼問題的解
* 在基因集合 &Gamma; 上定義**適應度函數** fit: &Gamma;&rightarrow;**R**，函數值越小表示解越好
* 定義**交叉**機制，用於結合兩個基因以生成新的有效解 crossover: &Gamma;<sup>2</sub>&rightarrow;&Gamma;
* 定義**突變**機制 mutate: &Gamma;&rightarrow;&Gamma;

在許多情況下，交叉和突變通常是操作基因（如數字序列或位元向量）的簡單算法。

基因演算法的具體實現可能因案例而異，但其基本結構如下：

1. 選擇初始族群 G&subset;&Gamma;
2. 隨機選擇本步驟要執行的操作：交叉或突變
3. **交叉**：
  * 隨機選擇兩個基因 g<sub>1</sub>, g<sub>2</sub> &in; G
  * 計算交叉結果 g=crossover(g<sub>1</sub>,g<sub>2</sub>)
  * 如果 fit(g)<fit(g<sub>1</sub>) 或 fit(g)<fit(g<sub>2</sub>)，則用 g 替換族群中的相應基因
4. **突變** - 隨機選擇一個基因 g&in;G，並用 mutate(g) 替換
5. 從第2步重複，直到適應度函數值足夠小，或達到步驟數限制為止。

## 常見任務

基因演算法通常用於解決以下任務：

1. 排程最佳化
1. 最佳化打包問題
1. 最佳化切割問題
1. 加速窮舉搜索

## ✍️ 練習：基因演算法

繼續學習以下筆記本中的內容：

前往[此筆記本](Genetic.ipynb)，查看基因演算法的兩個應用範例：

1. 公平分配寶藏
1. 八皇后問題

## 結論

基因演算法被廣泛應用於解決各種問題，包括物流和搜索問題。這一領域的靈感來自心理學與計算機科學的交叉研究。

## 🚀 挑戰

「基因演算法易於實現，但其行為難以理解。」[來源](https://wikipedia.org/wiki/Genetic_algorithm)  
進行一些研究，找出基因演算法的實現範例，例如解數獨問題，並以草圖或流程圖的形式解釋其工作原理。

## [課後測驗](https://ff-quizzes.netlify.app/en/ai/quiz/42)

## 回顧與自學

觀看[這部精彩影片](https://www.youtube.com/watch?v=qv6UVOQ0F44)，了解如何使用基因演算法訓練的神經網絡讓電腦學習玩《超級瑪利歐》。我們將在[下一節](../22-DeepRL/README.md)中深入探討電腦學習玩遊戲的相關內容。

## [作業：丟番圖方程](Diophantine.ipynb)

你的目標是解決所謂的**丟番圖方程**——一種具有整數根的方程。例如，考慮方程 a+2b+3c+4d=30，你需要找到滿足此方程的整數根。

*此作業的靈感來自[這篇文章](https://habr.com/post/128704/)。*

提示：

1. 可以考慮根的範圍為 [0;30]
1. 作為基因，可以使用根值的列表

使用 [Diophantine.ipynb](Diophantine.ipynb) 作為起點。

---

