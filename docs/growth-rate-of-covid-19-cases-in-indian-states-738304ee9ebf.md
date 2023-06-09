# 印度各邦新冠肺炎病例的增长率

> 原文：<https://towardsdatascience.com/growth-rate-of-covid-19-cases-in-indian-states-738304ee9ebf?source=collection_archive---------58----------------------->

## 自 2020 年 4 月 22 日以来，印度各邦新冠肺炎病例增长率的简单、易于解释的可视化图。这将让我们了解哪些州在控制方面做得很好，哪些州在未来几天处于危险地带。

***编者按:*** [*走向数据科学*](http://towardsdatascience.com/) *是一份以数据科学和机器学习研究为主的中型刊物。我们不是健康专家或流行病学家，本文的观点不应被解释为专业建议。想了解更多关于疫情冠状病毒的信息，可以点击* [*这里*](https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports) *。*

# 这个想法

由于新冠肺炎造成的全球疫情现在已经延伸到 2020 年上半年之后，几个国家仍然每天报告数千例病例。世界各地的数据科学爱好者已经提出了一些预测、仪表盘和可视化方法，其中许多方法在这个前所未有的时代非常有用。

在这里，我尝试对阳性病例的比率进行州级比较，即 ***，以尝试检测哪些州正在从相对安全的区域发展到危险的区域(潜在的热点)，反之亦然。***

# 我们如何比较？

重要的第一步是选择准确的比较标准。简单地说，每个州的病例数没有意义:

1.  每个州进行的检测数量很可能影响报告的阳性病例数量。更多的检测几乎肯定会导致更多的病例报告。因此，阳性百分比(即阳性病例数/100 次检测)是一个合适的指标。
2.  各州的人口也不能被视为无用的因素。你只会认为马哈拉施特拉邦或更远的地方会发生比果阿更严重的事故。阳性病例数/100K 人口是我们的第二个选项(*选择 100K 也确保了结果缩小到与前面变量类似的范围*)

然而，我们不应忽视这样一种可能性，即一个人口较多的国家正在进行与一个小得多的国家类似数量的检测，因此很可能也有类似数量的病例。在这种情况下，每 100，000 人口的病例数将不是一个非常合适的代表真实情况的指标，特别是***，因为不同州的检测存在显著差异的情况在我国非常相关。***

# 最终选择的指标

我上面所讨论的仅仅是我的直觉，仅仅基于此来选择或放弃影响变量是不公平的。为此进行了回归分析:

“每日测试次数”和“人群”是两个回归变量，而每日报告的病例数是预测变量。**在单独和共同考虑变量后，比较 R 平方值**显示“日常测试次数”占变异的大约 *63%，而“总体”占变异*的大约*11%。这清楚地证明了**“每日测试次数”是更有影响力的变量**(我的直觉:D 也是如此)。然而，最好不要完全抛弃另一个因素。相反， ***给两者适当的权重是最好的办法:分别为 0.84 和 0.16****(基于 R 平方比较)，从而将它们组合成一个新的变量。**

*此外，我将执行 3 个不同的可视化(每个基于独立的可视化)和最后一个使用加权变量。*

# *数据*

*我们的数据来源于下面的 GitHub 存储库，它致力于定期更新有关印度新冠肺炎的记录:[https://github.com/imdevskp/covid-19-india-data](https://github.com/imdevskp/covid-19-india-data)*

*然而，*并非所有的州都有足够的关于检测和报告的信息*。因此，我只选择了 16 个州，这些州有严格的信息和足够的案例来进行研究。即使在过滤后的数据中，一些值也是不准确或荒谬的(例如，负数的情况；尽管测试为 0，但仍有阳性病例，等等)。它们已经被插值技术所取代。*

*包括可视化在内的整个过程的代码(将在下面显示)已记录在此:[https://github . com/viper ville 007/Growth-rate-of-Indian-cases-in-States](https://github.com/ViperVille007/Growth-rate-of-Covid-19-cases-in-Indian-states)*

# *可视化和解释:*

*日期的选择:4 月 22 日被选为起点。从此，我们可以通过 ***获得*** 有关检测和确诊病例的具体信息。此外，封锁已经实施了一个月，到那时，几乎所有被选中的州都有足够的设施进行测试，从而确保了同质性。*

***平滑:**提供了近 90 个时间戳，绘制所有时间戳会使事情看起来 ***不必要的笨拙和难以解释*** *。*同样，如果我们关注每一天，一些 ***异常值是很有可能的*** 。我添加了 ***均值平滑到一个 7 天窗口的数据*** 来照顾这些问题。7 似乎是一个合理的选择，因为你会期望季节性每周都存在，如果它真的存在的话。*

***注:**点击图片，您可以选择以更高的清晰度观看。*

*[![](img/a1053704d0a151c41562b0c545ede3f0.png)](https://github.com/ViperVille007/Growth-rate-of-Covid-19-cases-in-Indian-states/blob/master/download%20(3).png)

来源:自创* 

*这是我们所做的 3 个可视化中的第一个(第一个*仅基于与进行的测试*相关的阳性案例的百分比)。*

*基于配色方案的随附图例很好地总结了这一点:通俗地说，**越接近黑色，该状态在该时间点的条件**越安全(参考图下方的轴),黄色表示高危险。*

*[![](img/d140cfe682f9391d8245a3d687d523e1.png)](https://github.com/ViperVille007/Growth-rate-of-Covid-19-cases-in-Indian-states/blob/master/download%20(2).png)

来源:自创* 

*所以，这是单纯根据每个州 **的病例数/10 万人口得出的*。****

*正如你可能已经猜到的，这个情节本身**并不是一个非常恰当的事情指标**(它*仅仅解释了我们之前看到的关系*的 11%)。*

*在不强调这一点的情况下，让我们快速进入最后的情节(基于我创建的修改变量)。*

*[![](img/4f65118bcadb874607ee3fa8ad11c284.png)](https://github.com/ViperVille007/Growth-rate-of-Covid-19-cases-in-Indian-states/blob/master/download%20(1).png)

来源:自创* 

*这是基于*修改变量的最终可视化图(带有前两个变量的适当权重)。**

*现在，让我们试着从中得出一些结论:*

1.  *理想的情况是，截止到最新时间戳的颜色方案接近黑色(非常低的增长率)*
2.  *从黄色到紫色的趋势表明，该州的传播曾经非常高，但正在逐渐放缓。*
3.  *相反的趋势(从紫色到黄色)表明存在风险——在接下来的几天里，情况只会变得更糟。基本上，麻烦。*
4.  *综上所述，德里正显示出放缓的迹象(从曾经非常糟糕的状态)。古吉拉特邦和哈里亚纳邦在某种程度上显示出类似的模式。*
5.  *这是西孟加拉邦、安得拉邦、比哈尔邦和卡纳塔克邦关注的问题。这种趋势非常令人担忧。*
6.  *泰米尔纳德邦和马哈拉施特拉邦没有任何值得注意的巨大差异——但是%仍然是最高的。*
7.  *其他州(大部分在黑色地带)已经能够应付事情，或者没有像上面讨论的那样严重地成为病毒的牺牲品。它们也没有显示出很快会突然爆炸的迹象。*

# *编辑 1:*

*我现在已经为选定的州制作了一个条形图比赛，以视频的形式显示进度。你可以在这里查看:[https://app.flourish.studio/story/489625/edit](https://app.flourish.studio/story/489625/edit)
这里有一个相同的快照:*

*![](img/408b60d1a996bed901f5806f17b5a7fa.png)*

*来源:自创*

*我们只能希望越来越多的地区开始出现与上述第二点类似的趋势。*

*非常感谢你，如果你有足够的耐心通读整篇文章。请随时留下您的真实反馈，指出这篇文章中存在的技术或印刷错误，或者在评论部分澄清您的疑问和疑问。干杯:)*