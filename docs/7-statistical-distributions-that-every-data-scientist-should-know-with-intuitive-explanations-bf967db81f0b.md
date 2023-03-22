# 每个数据科学家都应该知道的 7 种统计分布，以及直观的解释

> 原文：<https://towardsdatascience.com/7-statistical-distributions-that-every-data-scientist-should-know-with-intuitive-explanations-bf967db81f0b?source=collection_archive---------7----------------------->

## 对正态分布、伯努利分布、二项式分布、泊松分布、指数分布、伽玛分布和威布尔分布的直观解释，以及 Python 示例代码

![](img/400bf6882d5a6146059be8375a05d185.png)

每个数据科学家都应该知道的 7 种统计分布。卢克·切瑟在 [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片。

统计分布是数据科学中的一个重要工具。分布通过给我们一个变量最有可能获得的值的概念来帮助我们理解一个变量。

此外，当知道一个变量的分布时，我们可以做各种概率计算，来计算某些情况发生的概率。

在这篇文章中，我分享了 7 种统计分布，并给出了在现实生活中经常出现的直观例子。

# 1.正态或高斯分布

正态或高斯分布可以说是最著名的分布，因为它出现在许多自然情况下。

正态分布的变量有一个平均值，这也是最常见的值。越接近平均值的值越有可能出现，越远离平均值的值越不可能出现。

正态分布的特征还在于平均值周围的对称变化，用标准差来描述。这意味着较高的值和较低的值一样普遍。

![](img/fc95705d16e13f974fbca8a12bb12415.png)

平均值为 0，标准差为 1 的正态分布。

正态分布的例子可以在许多自然的连续变量中找到。例如，动物的体重或身高将遵循正态分布，因为大多数动物都是平均体重，有些稍微偏胖或偏瘦，但没有那么多动物非常瘦或非常胖。

人类的智商也是正态分布的一个非常著名的例子，平均值为 100，标准差为 15。大多数人智力一般，有些人稍聪明或稍不聪明，少数人非常聪明或非常不聪明。

# 2.二项分布

伯努利分布描述了一个概率事件，它只重复一次，并且只有两种可能的结果。这两种结果通常被称为成功，或 1，和失败，或 0(你可以把一切都称为成功或失败，取决于你看什么)。

因此，这种分布非常简单。它只有一个参数，就是成功的概率。

一个著名的例子是掷硬币，我们可以称任何一方成功。成功的概率是 0.5。这将导致下图:

![](img/95ed0217b9ebc686a954db5dc26cb615.png)

成功概率为 0.5 的伯努利分布。

但是 50/50 不是伯努利分布的一部分。伯努利分布的另一个例子是射中靶心的概率。要么在里面，要么不在，所以这是两种结果。对于一个糟糕的飞镖运动员，成功的概率可能是 0.1，给出如下分布:

![](img/7ad16f44a7f3206b12116c149b25beb5.png)

成功概率为 0.1 的伯努利分布。

# 3.二项分布

二项式分布就像伯努利分布的兄弟。它模拟了在重复伯努利实验的情况下成功的次数。因此，我们关注的不是成功的概率，而是成功的次数。

二项式分布的两个参数是实验次数和成功概率。一个抛硬币十次的基本例子是，实验次数等于 10 次，成功概率等于 0.5。这给出了每 10 次成功的概率如下:

![](img/d1edbd5de244c131d1e8b6ecb82a09ae.png)

概率为 0.5 和 10 次重复的二项式分布。

二项式分布的另一个例子是在给定的一周内发生交通堵塞的概率，已知在给定的一天内发生交通堵塞的概率是 0.2。这是在 5 个工作日重复 1 个伯努利是/否变量，因此参数为:实验次数为 5，成功概率为 0.2。下面的结果图显示，最有可能出现 1 次交通堵塞，然后是 0 次，然后分别是 2 次、3 次、4 次和 5 次。

![](img/8a81b0eadf610e18dcf4f40332b4665d.png)

概率为 0.2，重复 5 次的二项分布。

# 4.泊松分布

泊松分布描述了固定时间范围内的大量事件。您可以考虑的事件类型是每 15 分钟进入商店的顾客数量。在这种情况下，我们将 15 分钟作为一个固定值(单位时间)，这样我们就可以在其余的计算中忽略它。

在这种情况下，每个单位时间会有平均数量的顾客进入，这被称为比率。这个速率称为λ，它是泊松分布所需的唯一参数。

在下面的例子中，速率λ是 4，所以平均每单位时间(在这个例子中是 15 分钟)发生 4 个事件。在图中，我们可以看到 3 或 4 个事件是最有可能的，然后计数向两边逐渐减少。任何超过单位时间 12 次的事件都变得不太可能，以至于我们在图上看不到它们的条形。

![](img/4eb1d7b236fd23be15e26f8d1834a1d3.png)

泊松事件的其他例子可以是在特定位置通过的汽车数量。此外，几乎任何具有单位时间计数的事物都可以被认为是泊松分布。

# 5.指数分布

指数分布与泊松分布相关。泊松分布描述单位时间内的事件数量，指数分布描述事件之间的等待时间。

它采用与泊松分布相同的参数:事件率。然而，在某些情况下(尤其是在 Python 的 Scipy 中)，人们更喜欢使用参数 1 /事件率。

![](img/b389df0f009acb8adddf5a023b4b78c9.png)

你应该把 x 轴看做单位时间的百分比。在泊松例子中，我们说单位时间是 15 分钟。现在，如果我们在 15 分钟内有 4 个人，我们最有可能为每个新人等待 0.25 分钟，或这个单位时间的 25%。15 分钟的 25%是 3，75 分钟。

# 6.γ分布

伽马分布是指数分布的变体。它不是描述事件之间的时间，而是描述等待固定数量事件的时间。

它需要两个参数:指数分布的 lambda 参数，加上一个 k 参数，表示要等待的事件数。

举个例子，你可以想到一个景点公园，它只能在满了，比如说 10 个人的时候推出一个景点。如果他们的事件率是平均每 2 分钟有 4 个顾客进来，他们可以使用伽玛分布来描述推出景点的等待时间。

在下图中，我们可以看到顶部大约是 2.5。这意味着，平均下来，10 个人的等待时间是 2 分钟单位时间(即 5 分钟)的 2.5 倍。这是有意义的，因为我们每单位时间有 4 个人，总共需要 10 个人。

![](img/4368cce320e6aaf91d22d9e0c9a6eadc.png)

图表中有趣的是，我们可能要等待 6 倍的单位时间，所以(6 乘以 2 分钟=) 12 分钟。这远远超过了平均 5 分钟的时间，等待最先到达的顾客可能太长了。

伽马分布的其他例子是你必须等待 x 个事件的一切，假设这些事件不一定同时发生。

当 Gamma 分布用于等待时间时，如本例所示，它也称为 Erlang 分布，但我不会在此详述。

# 7.威布尔分布

威布尔分布是另一种分布，它是等待时间问题的变体。它描述了一个事件的等待时间，如果该事件随着时间变得更可能或更不可能。

一个明显的例子是计算机的寿命。你可以等一段时间，直到你的电脑太旧，坏了。你用电脑的时间越长，它就越有可能坏掉。所以失败的概率，或者说比率，并不是恒定的。

威布尔分布有两个参数。首先，泊松和指数分布中的速率参数。其次是 c 参数。c 为 1 意味着存在恒定的事件率(因此这实际上是一个指数分布)。高于 1 的 c 意味着事件率随时间增加。c 低于 1 意味着事件发生率随时间而降低。

如果我们采用与泊松例子中相同的λ值(λ= 4)，并且我们为 c 增加 1.1 的值(因此速率随时间增加)，我们得到以下结果:

![](img/6c681facbf02fc37aaa952ca6e97b5dd.png)

感谢您阅读这篇文章。我希望你喜欢它！