# 用遗传算法打破俄罗斯方块世界纪录

> 原文：<https://towardsdatascience.com/beating-the-world-record-in-tetris-gb-with-genetics-algorithm-6c0b2f5ace9b?source=collection_archive---------16----------------------->

## 使用 PyBoy 和 Python

![](img/7f14908448bf8e1f6be46cf57cfc3fbf.png)

你好，我是尼克🎞 on [Unsplash](https://unsplash.com/@helloimnik?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

几周前，我发现了这个用 Python 写的支持人工智能/机器人的很棒的游戏模拟器。我非常兴奋，因为现在我可以使用我的机器学习知识来创建困扰我童年的游戏代理。

在本文中，我将展示我们如何使用遗传学算法和神经网络的简单实现来创建一个代理，它可以在 Game Boy 上非常好地玩原版俄罗斯方块，并能够打破根据[twin galaxy](https://www.twingalaxies.com/game/tetris/game-boy-game-boy-color/points/)创下的 999999 和 523 行的世界纪录。

俄罗斯方块是最畅销的视频游戏系列之一，是一款益智游戏，主要目标是通过清除**俄罗斯方块**(是的，这些方块就是这么叫的)的线条来获得尽可能高的分数。游戏的规则非常简单，然而，它实际上是一个 [NP 完全](https://www.britannica.com/science/NP-complete-problem)问题[1]。这意味着编码一个基于规则的代理可能不是最明智的方法，启发式算法，如遗传算法，将是一个更好的选择。

遗传算法(GA)是一组受达尔文进化论启发的算法。这些算法用于解决优化问题。这意味着我们可以使用遗传算法来优化神经网络的权重(他们也可以做得很好)。在这篇文章中，我不会深入讨论什么是神经网络，因为已经有很多关于它的资源，比如这里的。

总的想法是，我们将创建一个神经网络(NN ),它将为代理所做的每个动作生成一个分数。对于每个新的 tetromino，代理将尝试所有可能的动作，并选择得分最高的动作。使用遗传算法，我们希望通过*进化优化网络，使其收敛到最佳状态。*

![](img/c7fd3ddee9b806bb7964e42cce973cc8.png)

评估可能行动的网络

在 GA 中，我们有一些关键的概念:**适应度**、**精英主义**、**交叉**和**变异**。

*   适应度是我们如何衡量网络的能力，以将其输出与移动的好坏相关联。
*   精英主义是指一定比例的高性能网络被带到新一代。
*   交叉是使用另外两个网络的基因(权重)创建新网络的过程。
*   变异包括随机修改网络的权重。

步骤如下:

1.  生成具有随机初始权重的神经网络群体。
2.  对于每个网络，一直玩到游戏结束。
3.  计算每个网络的**适应度**得分。
4.  把表现最好的网络带给下一批人(**精英主义**)。
5.  从当前群体中随机选择 2 个网络(父代)并执行**交叉**以产生一个新的网络(子代)。
6.  以 x%的概率突变新的网络权重。
7.  继续，直到我们达到所需的世代数。

像许多其他机器学习问题一样，我们需要做的第一步是收集数据，或者在这种情况下，从环境中收集状态数据。这里有一个快速的[例子](https://github.com/Baekalfen/PyBoy/blob/master/examples/gamewrapper_tetris.py)展示了如何快速初始化环境。

这个脚本本身是不言自明的。开发者通过`tetris.game_area()`很容易获得游戏的状态。然后，我们可以创建一个稀疏矩阵，其中 0 是空白瓦片，1 是碎片:

```
area = np.asarray(tetris.game_area())area = (area != 47).astype(np.int16)
```

![](img/e7158eaf83d92fda6abb781814003ed3.png)

棋盘的矩阵表示

使用上面的矩阵，我们可以定义许多特性，如[2]所示:

**合计高度** 计算所有列高度的总和。在上面的例子中，总和是 16。

**孔数
棋盘上的孔数。下面的板上有 6 个孔:**

![](img/65627b09cc7082c9420de3d0107fba2c.png)

**至少有一个孔**
的列数，在上例中为 5。

**凹凸度** 各列之间的绝对高度差之和。在下面的棋盘中，它是:`1 + 0 + 2 + 2 + 0 + 0 + 1 + 0 + 0 = 7`

![](img/4be50e76785a66a4a892ae36c7af20ac.png)

**行转换** 每一行中从被占用到未被占用的瓦片的转换数量相加。下图中的每个红点算作一个过渡:

![](img/c55b45fd22ad7dda12e034ddb8647581.png)

**列转换**
与上面类似，但按列进行。

**凹坑数量**
凹坑被定义为没有任何块的列。下面的板上有 3 个坑:

![](img/82ca014b408ef4652d1dd36535bf186f.png)

**最深的井** 一口井可以通过下面的图片得到最好的解释。在这种情况下，最深的井的高度为 2。

![](img/0dd7eb5207e7086296ec153adb928505.png)

**清除的行数** 移动时清除的行数。

让我们使用矩阵表示来实现这些功能:

现在，让我们实现算法:

首先，我们为网络创建一个类

我们的模型是一个简单的网络，输入层大小为 9，输出层大小为 1。这个简单的网络将使我们能够轻松地解释权重，并且可以表示如下:

![](img/c29b3720739e726dac6218641d6d8eb5.png)

我使用 PyTorch 来创建网络，但是您可以随意使用任何其他库或实现您自己的库。利用这一点，我们可以创建一个实现了交叉和变异的种群类:

对于每一代新人，我们将带来前 20%的网络。

对于交叉，我们用从群体适应度产生的概率分布对父母进行采样(网络适应度越高，它被选择的可能性就越大)。每个体重都是随机选择的，父母双方各有 50%的机会。

![](img/29c621945cc11b56a8fc00fc0cbc8eb4.png)

交叉

随后，权重有 20%的机会随着乘以因子 0.5 的随机高斯噪声的增加而变异。

下一步是编写一些逻辑来玩这个游戏。首先，让我们定义一些助手函数来移动块:

对于每一个新的作品，我们会尝试所有可能的动作。我们需要检查的转身和横向移动的次数取决于积木的类型。我们可以使用这三个函数来确定它们:

现在我们有了开始模拟网络所需的一切。对于每一个新的棋子，我们将棋盘信息传递给`get_score()`以获得每个可能动作的网络输出。我们选择输出最高的动作。一旦游戏结束，我们返回网络的**适应度**也就是游戏的分数。

由于游戏的随机性，网络不会为每次运行产生相同的结果。我们可以通过`run_per_child`评估每个网络的多次运行，以更好地估计网络的适应性。

随着代理在游戏中变得更好，培训时间会变得更长。为了加快训练速度，我们在代理达到最高分数(999999)时停止游戏，并使用多重处理。生成多个进程来并行评估网络非常简单，如下所示:

现在你知道了，我们已经实现了一个遗传算法来创建一个可以玩俄罗斯方块的简单代理。这里有一个例子，在人口规模为 50 的情况下，仅经过 10 代就获得了最佳模型:

```
Scores: [999999.0, 999999.0, 729892.0, 372490.0, 999999.0, 296117.0, 299328.0, 533870.0, 282609.0, 525193.0]
Average: 603949.6Lines: [1031, 1002, 825, 415, 935, 393, 364, 622, 389, 582]
Average: 655.8
```

然而，由于代理的简单性，它肯定有一些限制。由于代理人只考虑当前的奖励，而忽略未来的奖励，这很可能会出现这样的情况:放置一个方块可以清除线，但会恶化棋盘的位置。此外，由于棋盘尺寸较小(18x10)，如果代理连续获得多个坏块，则很有可能会输。这导致运行之间的标准偏差非常高，如上例所示，在最佳运行中，代理清除了 1031 行，在最差运行中清除了 364 行。

就这样，我希望你在阅读我对这个项目的方法时感到有趣。请随意查看完整的源代码，并根据您的意愿进行任何改进:[https://github.com/uiucanh/tetris](https://github.com/uiucanh/tetris)

参考资料:

[1]埃里克·德梅因、苏珊·霍恩伯格、戴维·李奔-诺埃尔。 [*俄罗斯方块比较硬，甚至可以近似*](https://arxiv.org/abs/cs/0210020) *。*

[2]雷南·萨缪尔·达席尔瓦，拉斐尔·存根帕皮内利。 [*玩原版游戏《男孩俄罗斯方块》用的是实数编码的遗传算法*](https://www.researchgate.net/publication/322321608_Playing_the_Original_Game_Boy_Tetris_Using_a_Real_Coded_Genetic_Algorithm)