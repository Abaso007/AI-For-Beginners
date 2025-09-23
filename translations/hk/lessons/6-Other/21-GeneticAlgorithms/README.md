<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "6bbd632dfe6c62e5f66bb51fd78c174a",
  "translation_date": "2025-09-23T12:45:16+00:00",
  "source_file": "lessons/6-Other/21-GeneticAlgorithms/README.md",
  "language_code": "hk"
}
-->
# 遺傳算法

## [課前測驗](https://ff-quizzes.netlify.app/en/ai/quiz/41)

**遺傳算法** (GA) 是基於一種**進化式方法**的人工智能技術，通過模仿群體進化的方式來尋求某個問題的最佳解。該算法由 [John Henry Holland](https://wikipedia.org/wiki/John_Henry_Holland) 在1975年提出。

遺傳算法基於以下理念：

* 問題的有效解可以表示為**基因**
* **交叉**允許我們將兩個解結合起來，生成新的有效解
* 使用某種**適應度函數**進行**選擇**，以篩選出更優的解
* 引入**突變**以打破優化的穩定性，幫助跳出局部最小值

如果你想實現遺傳算法，需要以下步驟：

* 找到一種方法，用**基因** g&in;&Gamma; 來編碼問題的解
* 在基因集合 &Gamma; 上定義**適應度函數** fit: &Gamma;&rightarrow;**R**，函數值越小表示解越好
* 定義**交叉**機制，將兩個基因結合生成新的有效解 crossover: &Gamma;<sup>2</sub>&rightarrow;&Gamma;
* 定義**突變**機制 mutate: &Gamma;&rightarrow;&Gamma;

在很多情況下，交叉和突變是相對簡單的算法，用於操作基因的數字序列或位向量。

遺傳算法的具體實現可能因情況而異，但其整體結構如下：

1. 選擇初始群體 G&subset;&Gamma;
2. 隨機選擇本步驟要執行的操作：交叉或突變
3. **交叉**：
   * 隨機選擇兩個基因 g<sub>1</sub>, g<sub>2</sub> &in; G
   * 計算交叉 g=crossover(g<sub>1</sub>,g<sub>2</sub>)
   * 如果 fit(g)<fit(g<sub>1</sub>) 或 fit(g)<fit(g<sub>2</sub>)，則用 g 替換群體中的相應基因
4. **突變** - 隨機選擇一個基因 g&in;G，並用 mutate(g) 替換它
5. 從第2步開始重複，直到適應度函數值足夠小，或者達到步驟數限制。

## 常見任務

遺傳算法通常用於解決以下任務：

1. 排程優化
1. 最佳打包
1. 最佳切割
1. 加速窮舉搜索

## ✍️ 練習：遺傳算法

繼續學習以下筆記本：

前往[這個筆記本](Genetic.ipynb)，查看使用遺傳算法的兩個例子：

1. 公平分配寶藏
1. 八皇后問題

## 結論

遺傳算法被用於解決許多問題，包括物流和搜索問題。這一領域的靈感來自心理學和計算機科學的交叉研究。

## 🚀 挑戰

「遺傳算法易於實現，但其行為難以理解。」[來源](https://wikipedia.org/wiki/Genetic_algorithm) 請進行一些研究，找到一個遺傳算法的實現，例如解數獨問題，並以草圖或流程圖的形式解釋其工作原理。

## [課後測驗](https://ff-quizzes.netlify.app/en/ai/quiz/42)

## 回顧與自學

觀看[這段精彩視頻](https://www.youtube.com/watch?v=qv6UVOQ0F44)，了解計算機如何通過遺傳算法訓練的神經網絡學習玩《超級瑪利歐》。我們將在[下一節](../22-DeepRL/README.md)中學習更多有關計算機學習玩遊戲的內容。

## [作業：丟番圖方程](Diophantine.ipynb)

你的目標是解決所謂的**丟番圖方程**——一種具有整數根的方程。例如，考慮方程 a+2b+3c+4d=30。你需要找到滿足該方程的整數根。

*此作業的靈感來自[這篇文章](https://habr.com/post/128704/)。*

提示：

1. 你可以考慮根的範圍為 [0;30]
1. 作為基因，可以考慮使用根值的列表

使用 [Diophantine.ipynb](Diophantine.ipynb) 作為起點。

---

