<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "6bbd632dfe6c62e5f66bb51fd78c174a",
  "translation_date": "2025-09-23T12:36:39+00:00",
  "source_file": "lessons/6-Other/21-GeneticAlgorithms/README.md",
  "language_code": "zh"
}
-->
# 遗传算法

## [课前测验](https://ff-quizzes.netlify.app/en/ai/quiz/41)

**遗传算法** (GA) 基于一种**进化式方法**，通过模拟种群的进化过程来为给定问题找到最优解。这种方法由 [John Henry Holland](https://wikipedia.org/wiki/John_Henry_Holland) 于1975年提出。

遗传算法基于以下理念：

* 问题的有效解可以表示为**基因**
* **交叉**允许我们将两个解结合起来，生成一个新的有效解
* 使用某种**适应度函数**进行**选择**，以筛选出更优的解
* 引入**变异**以打破优化过程的稳定性，从而摆脱局部最小值

如果你想实现遗传算法，需要以下步骤：

 * 找到一种方法，用**基因** g&in;&Gamma; 编码问题的解
 * 在基因集合 &Gamma; 上定义**适应度函数** fit: &Gamma;&rightarrow;**R**，函数值越小表示解越优。
 * 定义**交叉**机制，将两个基因结合生成一个新的有效解 crossover: &Gamma;<sup>2</sub>&rightarrow;&Gamma;。
 * 定义**变异**机制 mutate: &Gamma;&rightarrow;&Gamma;。

在许多情况下，交叉和变异是操作基因的简单算法，比如处理数字序列或位向量。

遗传算法的具体实现可能因情况而异，但总体结构如下：

1. 选择初始种群 G&subset;&Gamma;
2. 随机选择将在此步骤执行的操作：交叉或变异
3. **交叉**：
  * 随机选择两个基因 g<sub>1</sub>, g<sub>2</sub> &in; G
  * 计算交叉结果 g=crossover(g<sub>1</sub>,g<sub>2</sub>)
  * 如果 fit(g)<fit(g<sub>1</sub>) 或 fit(g)<fit(g<sub>2</sub>)，用 g 替换种群中的对应基因。
4. **变异** - 随机选择一个基因 g&in;G，并用 mutate(g) 替换它
5. 从步骤2开始重复，直到适应度函数值足够小，或达到步骤数限制。

## 常见任务

遗传算法通常解决以下任务：

1. 排程优化
1. 最优装箱
1. 最优切割
1. 加速穷举搜索

## ✍️ 练习：遗传算法

通过以下笔记本继续学习：

访问[这个笔记本](Genetic.ipynb)，查看两个使用遗传算法的示例：

1. 公平分配宝藏
1. 八皇后问题

## 总结

遗传算法被用于解决许多问题，包括物流和搜索问题。这个领域的灵感来源于心理学和计算机科学的交叉研究。

## 🚀 挑战

“遗传算法易于实现，但其行为难以理解。” [来源](https://wikipedia.org/wiki/Genetic_algorithm) 进行一些研究，找到一个遗传算法的实现，例如解决数独问题，并以草图或流程图的形式解释其工作原理。

## [课后测验](https://ff-quizzes.netlify.app/en/ai/quiz/42)

## 复习与自学

观看[这个精彩视频](https://www.youtube.com/watch?v=qv6UVOQ0F44)，了解计算机如何通过遗传算法训练的神经网络学习玩超级马里奥。我们将在[下一节](../22-DeepRL/README.md)中学习更多关于计算机学习玩游戏的内容。

## [作业：丢番图方程](Diophantine.ipynb)

你的目标是解决所谓的**丢番图方程**——一个具有整数根的方程。例如，考虑方程 a+2b+3c+4d=30。你需要找到满足该方程的整数根。

*此作业的灵感来源于[这篇文章](https://habr.com/post/128704/)。*

提示：

1. 可以考虑根的范围为 [0;30]
1. 作为基因，可以使用根值列表

使用 [Diophantine.ipynb](Diophantine.ipynb) 作为起点。

---

