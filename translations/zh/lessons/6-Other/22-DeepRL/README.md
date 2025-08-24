<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dbacf9b1915612981d76059678e563e5",
  "translation_date": "2025-08-24T20:36:56+00:00",
  "source_file": "lessons/6-Other/22-DeepRL/README.md",
  "language_code": "zh"
}
-->
# 深度强化学习

强化学习（RL）被认为是机器学习的基本范式之一，与监督学习和无监督学习并列。与监督学习依赖于已知结果的数据集不同，RL基于**通过实践学习**。例如，当我们第一次看到一款电脑游戏时，即使不知道规则，我们也会开始玩，并通过玩游戏和调整行为逐渐提高技能。

## [课前测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/122)

要进行强化学习，我们需要：

* 一个**环境**或**模拟器**，它定义了游戏规则。我们应该能够在模拟器中运行实验并观察结果。
* 某种**奖励函数**，它指示我们的实验是否成功。在学习玩电脑游戏的情况下，奖励可能是我们的最终得分。

基于奖励函数，我们应该能够调整行为并提高技能，以便下次表现更好。强化学习与其他类型的机器学习的主要区别在于，在RL中，我们通常直到游戏结束才知道自己是赢了还是输了。因此，我们无法单独判断某个动作是否是好的——我们只有在游戏结束时才会收到奖励。

在进行强化学习时，我们通常会进行许多实验。在每次实验中，我们需要在遵循迄今为止学到的最佳策略（**利用**）和探索新的可能状态（**探索**）之间找到平衡。

## OpenAI Gym

一个非常适合强化学习的工具是 [OpenAI Gym](https://gym.openai.com/)——一个**模拟环境**，可以模拟从Atari游戏到杆平衡物理等许多不同的环境。它是训练强化学习算法最流行的模拟环境之一，由 [OpenAI](https://openai.com/) 维护。

> **Note**: 你可以在 [这里](https://gym.openai.com/envs/#classic_control) 查看 OpenAI Gym 提供的所有环境。

## CartPole 平衡

你可能都见过现代平衡设备，比如 *Segway* 或 *Gyroscooters*。它们能够通过调整轮子来响应加速度计或陀螺仪的信号，从而自动保持平衡。在本节中，我们将学习如何解决一个类似的问题——平衡杆。这类似于马戏团表演者需要在手上平衡杆的情况——但这种杆平衡仅发生在一维空间中。

一种简化的平衡问题被称为 **CartPole** 问题。在 CartPole 世界中，我们有一个可以左右移动的水平滑块，目标是在滑块上方保持垂直杆的平衡。

<img alt="a cartpole" src="images/cartpole.png" width="200"/>

要创建和使用这个环境，我们需要几行 Python 代码：

```python
import gym
env = gym.make("CartPole-v1")

env.reset()
done = False
total_reward = 0
while not done:
   env.render()
   action = env.action_space.sample()
   observaton, reward, done, info = env.step(action)
   total_reward += reward

print(f"Total reward: {total_reward}")
```

每个环境都可以通过以下方式访问：
* `env.reset` 开始一个新的实验
* `env.step` 执行一个模拟步骤。它从**动作空间**接收一个**动作**，并返回一个**观察值**（来自观察空间），以及奖励和终止标志。

在上面的示例中，我们在每一步执行随机动作，因此实验的生命周期非常短：

![non-balancing cartpole](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-nobalance.gif)

强化学习算法的目标是训练一个模型——所谓的**策略** π——它会根据给定状态返回动作。我们也可以将策略视为概率性的，例如，对于任何状态 *s* 和动作 *a*，它会返回概率 π(*a*|*s*)，即我们在状态 *s* 下应该采取动作 *a* 的概率。

## 策略梯度算法

最直接的策略建模方法是创建一个神经网络，该网络以状态作为输入，并返回相应的动作（或所有动作的概率）。从某种意义上说，它类似于普通的分类任务，但有一个主要区别——我们事先不知道在每一步应该采取哪些动作。

这里的想法是估计这些概率。我们构建一个**累计奖励**向量，显示实验中每一步的总奖励。我们还通过乘以某个系数 γ=0.99 对早期奖励进行**奖励折扣**，以减小早期奖励的影响。然后，我们强化实验路径中产生较大奖励的步骤。

> 了解更多关于策略梯度算法的信息，并在 [示例笔记本](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb) 中查看其实际应用。

## Actor-Critic 算法

策略梯度方法的改进版本称为 **Actor-Critic**。其核心思想是神经网络将被训练以返回两件事：

* 策略，决定采取的动作。这部分称为 **actor**
* 对当前状态下可以获得的总奖励的估计——这部分称为 **critic**。

从某种意义上说，这种架构类似于 [GAN](../../4-ComputerVision/10-GANs/README.md)，其中有两个网络相互对抗进行训练。在 Actor-Critic 模型中，actor 提出我们需要采取的动作，而 critic 尝试批判性地估计结果。然而，我们的目标是让这两个网络协同训练。

因为我们知道实验中的真实累计奖励和 critic 返回的结果，因此构建一个损失函数以最小化它们之间的差异相对容易。这将产生**critic 损失**。我们可以使用与策略梯度算法相同的方法计算**actor 损失**。

运行这些算法后，我们可以期望我们的 CartPole 表现如下：

![a balancing cartpole](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-balance.gif)

## ✍️ 练习：策略梯度和 Actor-Critic 强化学习

通过以下笔记本继续学习：

* [TensorFlow 中的强化学习](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb)
* [PyTorch 中的强化学习](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-PyTorch.ipynb)

## 其他强化学习任务

如今，强化学习是一个快速发展的研究领域。一些有趣的强化学习示例包括：

* 教电脑玩 **Atari 游戏**。这个问题的挑战在于我们没有简单的状态表示为向量，而是一个截图——我们需要使用 CNN 将屏幕图像转换为特征向量或提取奖励信息。Atari 游戏可以在 Gym 中找到。
* 教电脑玩棋盘游戏，比如国际象棋和围棋。最近，像 **Alpha Zero** 这样的顶尖程序通过两个代理相互对战并在每一步中不断改进，从零开始进行训练。
* 在工业中，强化学习用于从模拟中创建控制系统。一个名为 [Bonsai](https://azure.microsoft.com/services/project-bonsai/?WT.mc_id=academic-77998-cacaste) 的服务专门为此设计。

## 总结

我们现在已经学习了如何通过提供定义游戏期望状态的奖励函数，并让代理智能地探索搜索空间，来训练代理以获得良好的结果。我们成功尝试了两种算法，并在相对较短的时间内取得了良好的结果。然而，这只是你进入强化学习领域的开始，如果你想深入研究，应该考虑参加专门的课程。

## 🚀 挑战

探索“其他强化学习任务”部分列出的应用，并尝试实现其中一个！

## [课后测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/222)

## 复习与自学

在我们的 [机器学习初学者课程](https://github.com/microsoft/ML-For-Beginners/blob/main/8-Reinforcement/README.md) 中了解更多关于经典强化学习的内容。

观看 [这段精彩视频](https://www.youtube.com/watch?v=qv6UVOQ0F44)，了解计算机如何学习玩超级马里奥。

## 作业：[训练一个山地车](lab/README.md)

在这次作业中，你的目标是训练一个不同的 Gym 环境——[山地车](https://www.gymlibrary.ml/environments/classic_control/mountain_car/)。

**免责声明**：  
本文档使用AI翻译服务 [Co-op Translator](https://github.com/Azure/co-op-translator) 进行翻译。尽管我们努力确保翻译的准确性，但请注意，自动翻译可能包含错误或不准确之处。应以原始语言的文档作为权威来源。对于关键信息，建议使用专业人工翻译。我们对于因使用本翻译而引起的任何误解或误读不承担责任。