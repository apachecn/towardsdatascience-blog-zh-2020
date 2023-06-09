# 武装匪徒:强化学习的入门课

> 原文：<https://towardsdatascience.com/the-k-armed-bandit-an-introductory-lesson-to-reinforcement-learning-4d51f5e71fdd?source=collection_archive---------25----------------------->

## 一个简单的例子很好的演示了 RL 的基本词汇。

# 指导性和评估性反馈

在监督学习中，你的算法/模型会得到有益的反馈。这意味着它被指示它应该做出的正确选择是什么，然后它更新自己以减少它的错误并使它的预测更准确。在强化学习中，你给出一个算法评估反馈。这告诉你的算法一个动作有多好，但不是最好的动作是什么。行为的好坏被称为奖励。RL 算法通过模拟来学习如何最大化该奖励。

# RL 的最佳应用

RL 的最佳应用是当您可以很好地模拟它运行的环境时。如果我们想教一个 RL 程序开车，我们可以让它开车，这将是一个完美的模拟。如果我们想教它在美式足球比赛中叫牌，我们会让它玩一堆 Madden 的游戏，这不是一个完美的模拟，因为我们使用视频游戏来代表现实世界。理解我们如何在这两种情况下设计 RL 算法中的反馈可能相当复杂，因此我将在一个称为 K 臂土匪的简单情况下介绍 RL 的一些基本概念。

# K 臂大盗的模拟

![](img/eb815e32f29c00cae1d2ee50ded08400.png)

图片由[龙翔钱](https://www.pexels.com/@longxiang-qian-834017?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)从[派克斯](https://www.pexels.com/photo/inside-the-casino-2110357/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

想象一下，你在一个有 1000 台老虎机的房间里，每台老虎机都是免费供你玩的(这使你成为一个土匪，因为你不会输掉任何钱)。这种情况下，有 1000 个兵种供你拉，那么这种情况下，你就是一个 1000 兵种的土匪。每台吃角子老虎机都会给你一笔正态分布的支出，每笔支出都有不同的平均值和方差。如果你有无数次拉杠杆的机会，你可以从每台吃角子老虎机中获得大量样本，找到最大化你的预期支出值的那个，然后一次又一次地拉杠杆。为了让事情变得有趣，假设你有一个 5000 次拉杆的极限。在这种情况下，你会如何优化你的支出？这很难说，你会慢慢实验并发现，因为拉动每个杠杆并记录信息需要时间，这是强化学习机器人的一个很好的应用。

# 勘探与开发

机器人首先拉动其中一个杠杆。结果是 500 美元，太好了！机器人目前对机器的看法是，它们都支付 0 美元，除了这台支付 500 美元。机器人决定留在这台机器上，等待机器人 1999 年剩余的拉杆。这被称为一种剥削方法，因为 bot 利用其当前对支出的了解。如果机器人决定切换到一台新机器，这将被称为探索性的，因为机器人正在收集如何最大化奖励的信息。剥削策略也被称为贪婪策略。

# 量化贪婪

相反，你可以建立一个系统，在这个系统中，机器人将总是利用它当前的知识(例如，选择当前支付最大的机器)，但在一定比例的时间里，你随机决定选择另一台机器来拉。这个时间百分比通常用变量ε来表示。ε为 0.1 的机器人会探索 10%的时间，这个机器人比ε为 0.5 的机器人更贪婪，后者只探索一半的时间。然后，你可以用许多不同 epsilon 的机器人来模拟你的环境，以找到最大化回报的最佳 epsilon。然后你可以模仿现实世界中最好的机器人。当单个吃角子老虎机的支出差异很大时，探索更有帮助。当每台机器每次支付完全相同的金额时(支付的差异为 0)，更贪婪的 epsilon 是首选。在第一次拉动控制杆之前，由于对所有机器有着完美的了解，epsilon 为 0 的机器人是最好的，因为它已经知道最好的机器，并且探索没有任何好处。

# 乐观的期望

即使在贪婪的机器人中，鼓励探索的一个好方法是改变机器人对它没有尝试过的机器的期望。早些时候，我将我们的机器人描述为，如果机器上没有任何信息，它的预期支出为 0 美元。我们可以改变这一点，使最初的期望是一台机器有 25 美元的支出。现在，如果我们第一次拉动杠杆，我们有 5 美元的支出，即使是贪婪的机器人也会想切换到另一台机器，因为另一台机器会使回报最大化。

# 支出漂移

以前，我们的机器人会跟踪每台机器的平均奖励，除非被随机告知要探索，否则就会拉走那台机器。如果每台机器的支出随着时间的推移开始变化，这意味着其正态分布的平均值增加或减少，有两种简单的方法来调整我们的机器人。首先是探索更多，所以只要选择一个更大的ε，我们就可以改进机器人。这不需要你修改任何代码，只需要重复模拟并挑选出新的最佳机器人。一个更好的方法是，我们可以制作一个线性回归模型，显示机器支出如何随着时间的推移而变化，而不是将我们关于机器的信息仅仅保存为平均值和方差。这将阻止贪婪的机器人利用不再有最高支付的机器。