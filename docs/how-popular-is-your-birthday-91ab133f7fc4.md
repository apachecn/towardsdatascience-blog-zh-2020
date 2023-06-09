# 你的生日有多受欢迎？

> 原文：<https://towardsdatascience.com/how-popular-is-your-birthday-91ab133f7fc4?source=collection_archive---------26----------------------->

![](img/444a2c48fa8780ba71d8ceac7ddc3e69.png)

阿迪·戈尔茨坦在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 房间里的两个人同一天生日的几率有多大？

在 2020 年之前的几年里，大量学生(20-30 或更多)在一起上数学课是很常见的。在许多课堂上，学生们被要求计算其中两人同一天生日的概率。

为了进行这种计算，学生们通常会做一个默认的假设，即每个人在任何给定日期出生的可能性都是相等的(均匀分布)。没有这个假设，问题就变得很难手工做。另一方面，你会经常看到类似于下图的可视化在互联网上流传。

![](img/7d4ef0c24021164a8bfcd08041af597e.png)

生日的相对受欢迎程度

我将在下面更多地讨论用于生成本文中的数字和值的数据。这张图表显示了某人在某一天过生日的相对可能性。

*   值为 1(如 12 月 16 日)意味着一个随机的人在那一天出生的概率与你对均匀分布的预期相同。
*   小于 1 的值(特别是 1 月 1 日、7 月 4 日和 12 月 24-26 日)意味着随机选择的人在那一天出生的可能性比均匀随机选择的人低很多倍。
*   大于 1 的值(特别是 9 月中旬)意味着一个随机的人更有可能在那一天出生，而不是你天真的期望。

请注意，对于大约每 4 年出现一次的 2 月 29 日，均匀分布意味着一个人在 2 月 29 日出生的可能性是在 2 月 28 日出生的可能性的四分之一。这在上面的图表中有所说明(如果不进行修正，与假设均匀分布的一年中其他任何一天出生的概率相比，2 月 29 日生日的相对频率为 0.92/4 = 0.23)。

7 月 4 日是美国的一个重要节日，但它不受欢迎，这应该会提醒你，这个数据只是针对美国的。

在本文的第一部分，我们将重点讨论概率问题，即:一个房间里的两个人同一天生日的几率是多少？首先，我们将使用生日在一年中均匀分布的假设来计算生日问题的解决方案。其次，我们将使用蒙特卡罗方法来计算给定的观察分布的解决方案。

结果将是，即使考虑到经验分布，答案也是不变的(虽然很接近！).对于我们考虑的问题的每一个版本，答案都是 23 刚好可以让两个人同一天生日的概率达到 50%。

在文章的第二部分，我们将进一步探索生日的分布，并建立一个简单的模型来理解出生的变化。

# 制服生日问题

在学校里，这个问题可以这样提出:

> 假设一个房间里有 n 人。假设没有人在 2 月 29 日生日，并且他们的生日是均匀分布在一年中其他 365 天的随机变量。找出 *n* 的最小值，使得至少两个学生同一天生日的概率至少为 50%。

为了解决这个问题，我们改为计算没有两个学生同一天生日的概率。我们把学生编号为 1 到 *n* 。第一个学生不与任何以前的学生共享生日的概率是 365/365=1。对于第二个学生，有 364 天不与以前的学生重叠，所以他们不与以前的学生同一天生日的概率是 364/365。下一个学生是 363/365 等等。

结果是下面的量，我们将把它表示为 *q* 。目标是找到最小的 *n* ，使得 *q ≤0.5。*

![](img/cbe3abbeb64a3cf654a5f927c5c008c9.png)

没有两个学生有相同的生日

在这一点上，大多数人都伸手去拿他们的计算器。但是我们可以通过对数和泰勒展开继续手工估算:

![](img/21ae877d01dfdd97dfa1d46060556e84.png)

用对数的一阶泰勒展开式逼近 ln q

在第一行中，我们取对数，把乘积变成和。我们还将每个分数重写为 1–x 的形式。当 x 较小时，一阶泰勒展开是一个很好的近似，ln(1–x)=–x。这是我们在第二行中应用的内容。第三行使用算术级数求和的公式(我们只是将分子中的 1+2+3+⋯+(n–1)相加)。ln(2)是著名的 0.69。乘法 0.69⨉365≈252(四舍五入)。 *n* 应该比 2⨉252 = 504 的平方根大一点，所以 *n = 23* 是我们基于这些近似值的猜测(在 ln q 近似值的分子中产生 253)。事实上，这是正确答案，如下图所示(精确计算/精确到数字)。代码链接在末尾。

![](img/561646d528c04cd1261ecdbe405ce3b6.png)

# 经验生日问题

现在我们转向使用真实数据解决生日问题。这个数据是由 FiveThirtyEight 提供的，是基于社会保障局(政府)从 2000 年 1 月 1 日到 2014 年 12 月 31 日每天的出生人口统计数据。有理由假设这涵盖了那段时间内美国几乎所有的新生儿。

根据给定的数据，我们来估计两个人同一天生日的概率。我们假设我们的 *n* 人的生日根据我们数据的经验分布是 iid 分布的。没有可行的直接方法从数据中计算出来，所以我们求助于蒙特卡罗方法。

具体来说，对于每个 *n* ，我们将从分布中进行抽样，并观察是否有生日相同的。同样，代码(和测试用例)在最后链接的回购中。有点令人惊讶的是，结果基本上没有变化。结果如下图所示，其中还标有统一生日问题的值。经验结果也有 99%的置信区间，这个区间小到你看不到(每个*n*使用 100，000 次模拟)。

![](img/16dfd0a0c1d626f76c58183747b6a41f.png)

这种分布足够接近均匀，以至于结果 *n=23* 继续适用于经验案例！从某种意义上说，事后看来，这是一个不必要的分析。两条曲线之间的差异如下图所示，您可以看到它们在统计上是不可区分的。

![](img/bb3c43e3c93b888f66621319d30a2f3f.png)

要明确的是，分布是不一样的。然而，该模拟是在每个 *n* 值 100，000 次抽取的情况下运行的，没有足够的统计能力来揭示差异。大量的模拟将揭示统计上显著的(但实质上很小的)差异。例如，仅针对 n=23 运行 5，000，000 次抽奖，最终产生足够的统计能力来区分。经验分布有 P=50.786% 0.022%，而均匀分布有 P=50.730%。(误差幅度是 1 个标准差，而不是 95%的置信区间)。

# 一岁生日问题

现在，在任何一个固定的年份，出生分布偏离均匀的程度都应该高于总体水平。我们期望在任何一年看到的许多变化将会被消除。例如:

*   任何给定的日期都将在 14 年的周期中循环通过一周中的每一天，因此由于一周中的每一天(下面讨论)而与统一值的偏差将被隐藏。
*   感恩节(美国 11 月的第四个星期四)并不是每年都在同一天。回顾一下生日的相对流行度表，我们可以看到，在 11 月底有一个下降，但每年精确日期的轻微变化使它变得平滑。

回到生日问题，这可能会让我们担心。如果你问一个典型的 2020 年秋季四年级学生，大多数人会在 2010 年 9 月至 2011 年 8 月出生。我们期望比经验分布更高的可变性，因为他们中的每一个都不太可能出生在某一天，比如说，恰好是 2010 年秋天的劳动节。这可能导致不同的解决方案(也许 n=22？)的生日问题。

为了探索这一点，我们可以如下进行。

1.  我们可以量化这种差异。[kull back–lei bler 散度](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)(KL–div)是两个概率分布之间差异的度量。对于整个数据集和每一年，我们可以计算出均匀分布的变化。
2.  我们可以使用蒙特卡罗方法并从基于 1 年的分布中提取数据来重新解决生日问题。为了简单起见，我们将它保持为一个日历年。

对于第一个，我们在下面的图表中确认了我们的预期。年度基础上(0.021 .006)与统一基础上(0 . 002)的差异约为 10 倍。数据似乎还有一个有趣的趋势。我能想到的唯一可能的解释是日历通过一年中 7 个可能的开始日期逐渐循环。闰年打乱了周期，但粗略地说，我们预计，例如，7 月 4 日会从周一到周二再到周三等等。在 6 到 7 年的时间里。

![](img/feae2ccd3dab46c8c2255757d356b699.png)

在使用年度数据重新估计生日问题方面，我们可以这样做(使用每 n 10000 次运行的较小模拟规模)。曲线略高于均匀分布(以蓝色显示)。解决方案*几乎*改变，但事实上，n=23 仍然适用于一屋子同年出生的人。当 n=22 时，2009 年出生的人出现这种情况的概率高达 49.1%，而均匀分布的概率为 47.6%。

![](img/aa328c9c8221174aa63c4c114fd198b8.png)

因此，事实证明，对于这个问题，统一假设已经足够好了，没有必要再烦恼了。

# 生日的分布

既然来了，那就看看我们还能从数据中得到什么其他见解吧。

## 星期几

你可能会惊讶地发现，周末并不是生孩子的好时机。下图显示了在我们的数据集中，一周中任何一天的平均出生人数。显示了 95%的置信区间，该区间很紧，表明周末和工作日之间有统计学上的显著差异，以及周一出生的人数明显较少。

![](img/3cb45474cd52c8836f87f8a775c5b732.png)

你可能需要记住两个假设。让我们称之为消极和积极的假设(因为你可能对原因有什么感觉)

*   根据我之前与医生的交谈，消极的一面是，*产科医生*(接生的医生)在周末分娩不方便。如果你可以去你的避暑别墅，为什么整个周末都要随叫随到呢？如果是真的，这将有点令人难过，因为剖腹产对美国医疗保健系统来说是昂贵的，而且它们将意味着不必要的手术以及随之而来的对母亲的风险。
*   积极的一面是，你可以在这个数据分析中找到，医院在一周内都是满员的，所以那时安排剖腹产更安全也更容易。

你可以在那篇 538 文章中读到更多。

## 回归模型

总的来说，关于这些数据，你可能想问的一般问题是:如何解释任何一天出生人数的变化？以这种方式陈述，我们有一个经典的回归问题。我们想对数据建模，看看我们能学到什么。

我的目标是做一个快速简单的模型。例如，我们可以使用复杂的时间序列/预测工具，如脸书的[预言家](https://github.com/rcharan/birthdays)记录各种各样的假期以及假期的临近，每个假期都可以作为回归变量输入。我不想搞得这么花哨，所以对于协变量我们就用:

1.  月份。
2.  年份(考虑出生的长期趋势/变化)。
3.  一周中的某一天。
4.  通过查看图表和思考美国的主要节日，非科学地选择了一些节日。完整的清单在下面的附录中。总共有 17 个假日协变量。

同样，更复杂的分析将使用地理分类数据，并考虑各种因素，如天气、当地运动队的 performance⁴、(当地)经济，以及任何广泛影响人们并使他们和他们的伴侣(我猜是代理人)决定怀孕(或意外怀孕)的因素。

得到的模型非常好，R 为 94%。⁵这意味着 94%的出生率变化可以用这个模型来解释。以下是系数:

![](img/3e324e48b8e210c594ec5206f1ffcc7e.png)

出生回归模型的系数

每个系数代表了在其他因素不变的情况下，出生人数的预期变化。你可以在最后链接的 GitHub repo 中找到确切的系数。橙色条显示 95%的置信区间。例如，在圣诞节，系数约为–5300 意味着在考虑月份(12 月)、星期几(变化)和年份后，在我们的数据集中，圣诞节出生的婴儿比我们预期的要少 5300 人。

对于月份表，系数表示相对于一月份的变化。因此，如果我们选择 9 月的某一天与同年 1 月的某一天进行对比，并保持其他所有因素不变(星期几、节假日)，我们预计在 9 月的某一天会多出生 1140 人。同样，对于一周中的某一天，一切都与星期一相比。

截距(未示出)是一月份的一个普通星期一的出生人数，大约每天 12，000。随着时间的推移，出生率也略有下降，2000 年后，每天的出生率约减少 33 人，尽管进一步的研究(未显示)表明，这种影响不是线性的，不应过度解读。

情人节是生孩子的好时机，而阵亡将士纪念日周末似乎和其他周末一样好。剩下的假期，感恩节、圣诞节、劳动节、阵亡将士纪念日都相当冷门。我们看到，在主要节假日的其他日子里，影响很大，但较小。

就月份而言，我们看到一个明显的趋势，即出生从春季开始，到夏末初秋，在 9 月达到高峰。据推测，这代表了父母在前一个冬天选择做的事情。星期分析与我们之前看到的非常相似。

我们想问的下一个问题是，我们还错过了其他日子吗？下面显示的是模型的残差，按日期平均。你应该把这解释为之后的某一天*的相对受欢迎程度，考虑到一周中的某一天、一个月中的某一天以及有限的假日选择。*

具体来说，它显示了每天出生/未出生婴儿的异常平均数。这些残差都四舍五入到最接近的 10。

![](img/f3937c67c8730799e549de9aa79d87d8.png)

按日期分列的每日出生人数无法解释的变化

几件事立刻跳了出来。万圣节(10 月 31 日)是一个不受欢迎的生孩子的日子，我们忘了把它包括在内。7 月 5 日不受欢迎。在我的假日快速编码中，7 月 4 日周末之后的星期一(通常是庆祝这一天的日子)不会被包括在内，这可能解释了这一点。12 月 23 日也不受欢迎。

13 号的垂直蓝色条纹表明，在其他条件相同的情况下，人们也不喜欢在 13 号生孩子！他们也不喜欢在 9 月 11 日分娩(至少从 2001 年开始)。看看 12 月，我们发现人们更喜欢在月末生孩子:要么是圣诞节前的一周，要么是圣诞节和新年之间的一周。

# 结论

人们能够以某种方式控制何时生育，这非常令人着迷。很难说这是一种潜意识现象，是不同程度的压力，还是有意的医疗干预，还是其他什么。

我们已经看到，总的来说，出生的分布非常接近均匀(接近到生日问题的解决方案仍然是 *n* =23 *)。*另一方面，我们在更小的时间尺度上看到了重大变化:在一周的几天中，以及当以年度为基础进行检查时。但是，即使以年度为基础来看，这仍然不足以改变生日问题的解决方案。

最后，我们研究了出生率变化的模型，发现它主要是由假期、月份和一周中的天数来解释的。对于剩余的无法解释的差异，我们可以指出我们忘记建模的几天:13 号，万圣节，7 月 4 日周末，9 月 11 日，以及圣诞节前后的几天。

# 附录:假期列表

共有 17 个由节假日引入的协变量。对于每一个，如果包括任何相关联的周末，则所有周末的编码都是相同的。例如，劳动节有两个指示变量:一个是劳动节本身，另一个是劳动节周末。

1.  新年、除夕和后天(3)
2.  情人节(1)
3.  闰日(1)
4.  阵亡将士纪念日及其前一个周末(2)
5.  7 月 4 日和相邻的周末，如果有的话(2)
6.  劳动节和劳动节周末(2)
7.  感恩节，前一天，和 Fri-太阳之后(3)
8.  圣诞节、平安夜和后天(3)

# 参考

所有的数字和计算都是我自己的，尽管第一个数字在概念上并不新颖。提供的数据基于社会保障管理局的数据。复制数字和计算的代码可以在 [Github](https://github.com/rcharan/birthdays) 上获得。

# 笔记

[1]这是一个有时被遗忘的事实，闰年每四年发生一次*，除非*这一年能被 100 整除*但是*有一个警告，如果这一年能被 400 整除，这个例外就不适用。这意味着 1900 年和 2100 年不是闰年，但是 2000 年和通常的年份:1996 年、2004 年、2008 年等在一起。目前已知的活着的人中，没有一个人在其一生中没有经历过每四年一次的闰年(数据来自 2000 年至 2014 年)，因此为了我们的分析目的，我们可以安全地将闰年视为每四年发生一次。我们肯定会忽略像[闰秒](https://en.wikipedia.org/wiki/Leap_second)这样不会对我们的分析产生实质性影响的深奥的东西。

[2]我不打算给出一个非均匀分布应该给出不同曲线的正式证明。但是，直觉上，在一年中的每一天支持的所有分布中，均匀分布最小化了两个人生日相同的概率。任何偏离这一点(由[kull back–lei bler-divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)量化)必然导致两个人同一天生日的概率上升。在回购中，你可以找到一个例子，我们越来越多地扭曲数据，差异最终变得肉眼可见。

[3]从技术上讲，我们应该在分配 p 值时考虑多重比较。然而，很明显，仅从数据来看，结果将具有统计学意义。

[4]就我个人而言，在明尼苏达双子队赢得世界冠军 252 天后，我出生在明尼阿波利斯(人类的标准怀孕期是 280 天)。

[5]有关拟合优度的更多数据，请参见 Github repo。拟合的 RMSE 大约是每天 550 个新生儿，尽管分布有厚尾。