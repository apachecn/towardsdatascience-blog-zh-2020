# 旧金山湾区是在拉平曲线吗？

> 原文：<https://towardsdatascience.com/is-the-sf-bay-area-flattening-the-curve-303419a0011d?source=collection_archive---------34----------------------->

## 开始就地避难已经一个月了。数据告诉我们什么？(更新时间:2020 年 4 月 20 日)

![](img/ef84dcbf860d1b122a2247e10195e949.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Amogh Manjunath](https://unsplash.com/@therealamogh?utm_source=medium&utm_medium=referral) 拍摄的照片

3 月 16 日，旧金山湾区的六个县发布了就地安置避难所的命令。这意味着海湾地区的居民已经在原地躲避了大约一个月。让我们看一下数据，看看结果如何。

# 每日新案件

每天新增病例的数量可以被认为是新冠肺炎增长曲线。在我看来，这是最重要的图表，因为它代表了感染的加速。我会解释——但如果你已经知道这一点，请随意跳过下一段。

> 尽管总速度很重要，加速度(增长曲线)意味着在城市街道上和在高速公路上的区别。

如果你把它想象成开车旅行，感染的传播用行驶的英里数来表示，那么病例总数就像你行驶的速度(速度)，而增长曲线就是汽车加速的速度(加速度)。尽管总速度很重要，加速度(增长曲线)意味着在城市街道上和在高速公路上的区别。也就是说，总病例数代表了一段时间内的变化，但增长曲线显示了病例数的增长速度。

![](img/346a73996a5175bf0307cf9437b7519d.png)

旧金山湾区每日新增病例(更新时间:2020 年 4 月 20 日)。参见[诺维湾区冠状病毒仪表盘](https://www.knowi.com/coronavirus-dashboards/sf-bay-area/)上的实时可视化。

这张图表显示了新冠肺炎病例的增长情况。x 轴显示了湾区开始出现新冠肺炎病例的日期。y 轴表示增量，即病例总数的变化。或者更简单地说，y 轴显示每天的新案例。堆叠条形图中的不同颜色显示了各县的详细情况。但是要看整个湾区的增长曲线，你只需注意条形的总高度。

看这张图表，你可以看到新病例明显趋于平稳。作为对比，这是伊利诺伊州的增长曲线。

![](img/b63fc9981598c15463fe782ca9135eb5.png)

伊利诺伊州每日新病例(2020 年 4 月 20 日更新。点击放大)。来自伊利诺伊州的仪表盘。

根据伊利诺伊州的图表，你可以看到在过去的几天里有稳定的可能，但是最近还没有足够的数据来确定。

所有这些数据需要记住的另一个因素是，这些都是确诊的新冠肺炎病例。所以这些数字会受到测试次数的影响。

# 案件总数

旧金山湾区的总病例数继续上升，但由于增长放缓，这是线性上升，而不是指数上升。这是我们从上面显示的增长曲线中所期望的。

![](img/b413a018046237fbd2140812d062cb45.png)

旧金山湾区新冠肺炎病例的近似线性增长(更新时间:2020 年 4 月 20 日)。从[诺维湾区冠状病毒仪表板](https://www.knowi.com/coronavirus-dashboards/sf-bay-area/)。

# 这对就地安置的功效意味着什么？

有很多其他的变量涉及到这些结果的归属；比如:人口的总体健康状况、原地住所的遵守情况、人口密度、卫生设施的可用性以及文化因素。另一个要考虑的因素是旧金山湾区已经有了一个重要的在家工作的文化，这可能增加了对就地安置令的遵守。

> 我们可以使用旧金山湾区的例子来创建一个粗略的时间表，显示就地避难减少感染率需要多长时间以及减少多少。

也就是说，如果我们假设这种模式对其他地区大致相同，那么我们可以使用旧金山湾区的例子来创建一个粗略的时间表，说明就地避难需要多长时间来降低感染率以及降低多少。

整个加州的就地避难法令于 3 月 19 日生效，纽约的就地避难法令于 3 月 22 日生效。旧金山湾区的就地避难所已于 3 月 16 日生效。因此，如果我们按照这个粗略的模型，加州比湾区晚 3 天，纽约比湾区晚不到一周。

正如本文所预测的那样(在更新之前)，随着其他地区的就地安置时间表赶上来，我们似乎也看到了类似的结果。

# 数据源和参考

这篇文章的所有数据和可视化来自 [Knowi 冠状病毒数据中心](https://www.knowi.com/coronavirus-dashboards/)。那里使用的数据来自约翰·霍普斯金，世卫组织，疾病控制中心。
在这里查看他们的数据来源列表。

各州的避难所订单日期可以在纽约时报页面[这里](https://www.nytimes.com/interactive/2020/us/coronavirus-stay-at-home-order.html)找到。

旧金山官方的就地安置避难所命令可以在这里找到。

# 放弃

***编者按:*** [*走向数据科学*](http://towardsdatascience.com/) *是一份以数据科学和机器学习研究为主的中型刊物。我们不是健康专家或流行病学家，本文的观点不应被解释为专业建议。想了解更多关于疫情冠状病毒的信息，可以点击* [*这里*](https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports) *。*