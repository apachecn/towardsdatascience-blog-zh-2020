# 人工智能的下一步:抽象和推理

> 原文：<https://towardsdatascience.com/ais-next-step-abstraction-reasoning-db2d90e82799?source=collection_archive---------39----------------------->

## 用演示测试你的一般智力

![](img/b72681c992664dad5d537cddf5065788.png)

抽象和推理语料库中包含的 600 个任务的一个小样本。

> 如果你想直接试一试: [ARC 测试界面](https://apple-lemon-fighter.glitch.me/apps/testing_interface.html)。

人工智能在过去十年取得了突飞猛进的发展，解决了许多我们认为不可能完成的任务，但我们离类人智能还很远。最重要的是，创造人工智能的领先方法不像我们在自然界中看到的那样，使用庞大的数据库来学习模式识别。这与人类形成对比，人类拥有灵活的智力，允许我们只用少量样本就能胜任。为了帮助推动世界向前发展，一个新的挑战——抽象和推理语料库(ARC)——已经提出，它可能会取代图灵测试，成为人工智能的目标。除此之外，随着全球工程师在在线平台 Kaggle 上争夺奖项，对人工智能社区的挑战正迅速接近尾声。

## 弧形

2019 年 11 月发表的名为“**论智力的衡量标准**”的 [64 页研究论文](https://arxiv.org/abs/1911.01547)，概述了人工智能研究的历史，一个新的视角和抽象与推理语料库(ARC)。它是由资深深度学习研究员兼谷歌工程师弗朗索瓦·乔莱(Franç ois Chollet)提出的。在书中，他认为:

> “ARC 可用于测量类似人类形式的一般流体智能，它可以在人工智能系统和人类之间进行公平的一般智能比较。”

这很重要，因为就像正在构建的人工智能一样，人类是非常面向目标的。通过提供一个单一的努力目标，我们可以衡量我们的表现，迭代，改进并努力超越基准。我们已经在人工智能的其他领域看到了非常相似的结果；当 MovieLens 数据集发布时，推荐系统实现了飞跃；图像识别社区随着 MNIST 和随后的 ImageNet 的发展而繁荣。希望 ARC 可以成为更普遍的智能人工智能系统的火花。

本文的另一个重要成果是系统智能的定义(如下所示)。这个等式在这里有点难以解释，但它可以解释为"*智力是学习者在涉及不确定性和适应性的有价值的任务中将其经验和先验知识转化为新技能的速度。因此，最智能的系统只需要少量的经验，并根据这些经验猜测在许多不同的情况下会有什么样的结果。*

![](img/60c02f6f566490d355ab684dd6b23547.png)

乔莱对智力的定义。有趣的是，公式本身就需要很高的智力门槛来处理！

让我们通过一个来自 ARC 的例子更容易地看到这一点。作为 ARC 中所有任务的标准，我们从一些必须理解的例子开始，然后归纳为一个测试用例。

![](img/79fa2479fdcca484e62c4b3e8b93754c.png)

任务 11:星际飞船建造者(好吧，他们并没有真正的名字，但这更有趣)。这里的目标是采用基本模式并围绕它建造一艘“星际飞船”。这是通过将外部部分从中心向外延伸一个方块，将中心部分向对角线方向延伸两个方块来实现的。

在这个例子中，你必须用基本的图案围绕它们建造一艘“星际飞船”,注意基本的颜色。对于测试用例，只提供给你一张图片(比如说，最左边的那张)，你必须猜测相邻的那张。对于我们来说，看到这种模式并假设(猜测)创建解决方案的下一步是什么是相对简单的，但建立一个人工智能来为一般情况做这件事是我们目前非常非常远的事情。

> 上面的例子相对简单，但是肯定有更复杂的。点击这里提供的链接选择“随机任务”来尝试一些挑战: [**电弧测试界面**](https://apple-lemon-fighter.glitch.me/apps/testing_interface.html) 。如果你发现任何问题特别难，请在下面分享你的结果！感谢论文作者准备了这个界面并允许它自由发表。或者，在这里查看所有示例。

## 似乎很容易

但是是什么让人工智能变得如此困难呢？我们可以考虑像这里的[和](https://www.kaggle.com/nagiss/manual-coding-for-the-first-10-tasks)一样手动编程每种情况。只需要一行日常语言就能表达的东西，却需要几十行代码。

![](img/36c5cef2225abb4d3109be9ca003e061.png)

任务 1:打开门户。用英语直截了当表达的东西，例如“用黄色填充绿色物体”，用代码来表达相对复杂。

“用黄色填充绿色对象”的示例变为:

```
def task_train001(x):
    green, yellow = color2num["green"], color2num["yellow"]

    def get_closed_area(arr):
        *# depth first search*
        H, W = arr.shape
        Dy = [0, -1, 0, 1]
        Dx = [1, 0, -1, 0]
        arr_padded = np.pad(arr, ((1,1),(1,1)), "constant", constant_values=0)
        searched = np.zeros(arr_padded.shape, dtype=bool)
        searched[0, 0] = True
        q = [(0, 0)]
        while q:
            y, x = q.pop()
            for dy, dx **in** zip(Dy, Dx):
                y_, x_ = y+dy, x+dx
                if **not** 0 <= y_ < H+2 **or** **not** 0 <= x_ < W+2:
                    continue
                if **not** searched[y_][x_] **and** arr_padded[y_][x_]==0:
                    q.append((y_, x_))
                    searched[y_, x_] = True
        res = searched[1:-1, 1:-1]
        res |= arr==green
        return ~res

    y = x.copy()
    y[get_closed_area(x)] = yellow
    return y
```

但这只是问题的一面。如果需要，我们可以编写任意长的代码，但我们在这里试图解决的问题是编写可以解决各种问题的代码，而不仅仅是我们手动编程的问题。

总的来说，对我们来说似乎简单的东西来源于论文所描述的“人类先天的先验”。这种先验知识指的是我们用来处理概念的东西，比如物体是什么，对称性是什么，或者排序什么东西意味着什么。任何系统都必须能够学习这些，或者至少将它们预先编程，然后开始将它们缝合在一起以找到解决方案。例如，我们可以编写关于对称性意味着什么的函数，或者我们可以创建一个能够学习对称特征的二维过滤器。

> 值得注意的是，在 ARC 的情况下，先验的数量保持在绝对最小值，这是使该数据集真正伟大的另一个因素。你可以将这与原始的图灵测试进行对比，在原始的图灵测试中，计算机必须模仿人类。要做到这一点，计算机必须对人类文化有充分的理解才能通过，这与智力没有直接关系。

让这项任务变得非常棘手的另一个原因是，输入量非常小，这意味着系统必须能够从少量训练样本中学习复杂的行为。出于这个原因，像深度学习这样最受欢迎的技术并不适合这个问题，因为它们通常需要数百万个训练样本。最重要的是，它们需要用于训练它们的数据和它们必须解决的问题之间的共性，这对于 ARC 来说并不成立。

这就是 ARC 真正有趣的地方。它正在推动边界，迫使研究人员提出创新的系统来解决前所未有的普遍问题。

## 一个解决方案？

论文发布后，在线平台 Kaggle 发布了一个竞赛:抽象和推理挑战。在这场比赛中，工程师们面临的挑战是在 ARC 中描述的任务上获得尽可能好的分数。我们不太可能在剩下的一个月里解决人工智能问题，但我们正在探索一些有趣的问题。迄今为止的主要尝试包括:

*   [卷积神经网络](https://www.kaggle.com/tarunpaparaju/arc-competition-eda-pytorch-cnn):乍看之下，CNN(处理图像以告诉你是否有猫的同一个[系统](https://github.com/fdalvi/cat-detector))很适合这个问题，因为它们是为处理二维图像数据而建立的，可以建立强大的模式检测器。但是如前所述，这些系统不能很好地解决问题，性能也很差。
*   细胞自动机:通过定义一套简单的规则，我们可以使用细胞自动机产生复杂的行为。如果你从未听说过它们，一定要查一下——它们超级酷！虽然到目前为止的探索大多是好玩的，但思考和触及智能的核心是很有趣的。
*   [决策树](https://www.kaggle.com/meaninglesslives/using-decision-trees-for-arc):ML 工程师的另一个拿手好戏是决策树。通过一些聪明的特征工程，有可能产生一些正确的答案，但是很难看出它如何一般化。
*   [遗传算法](https://www.kaggle.com/zenol42/dsl-and-genetic-algorithm-applied-to-arc):从一些关于如何转换图像的函数(特定领域语言，DSL)开始，遗传算法采用一些随机函数并进化这些函数，类似于(在某种意义上)地球上生命的进化。有了一个定义良好的函数列表和一个关于什么“看起来不错”的强烈想法，这种方法似乎可以很好地执行。

您可以在 [Kaggle 论坛](https://www.kaggle.com/c/abstraction-and-reasoning-challenge/notebooks)上关注所有这些解决方案的更新，或者等到比赛结束后查看顶级选手的评论。

## 展望未来

这并不是贬低当前技术的力量。深度学习给了我们像自动驾驶汽车和象棋大师这样令人惊叹的技术。所有这些都是在一个庞大的经济体的背后发展起来的，这个经济体渴望通过能够像人类一样完成非常具体的任务的系统来实现自动化。经济需求和强大的社区解释了为什么这些系统如此流行和被大量研究。这篇论文提醒我们的是，还有其他值得探索的方向。让我们开始吧！

![](img/b27617af27c831e0ec3cbfb5a822f3fd.png)

元胞自动机求解门户打开任务。信用: [arseny-n](https://www.kaggle.com/arsenynerinovsky/cellular-automata-as-a-language-for-reasoning) 。