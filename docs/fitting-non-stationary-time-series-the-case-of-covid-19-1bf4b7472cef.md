# 拟合非平稳时间序列

> 原文：<https://towardsdatascience.com/fitting-non-stationary-time-series-the-case-of-covid-19-1bf4b7472cef?source=collection_archive---------29----------------------->

## 新冠肺炎的例子

![](img/d99a13fe0b796cefcdd2f44aa49bf01e.png)

杰克·希尔斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

非平稳时间序列是其(统计)特性随时间变化的时间序列。让我们假设我们正在处理一种病毒的传播，例如新冠肺炎病毒，并寻找普遍适用的模型。

大多数教科书都会支持指数模型的应用。每当一个量的变化率取决于该量本身时，这些模型都适用。换句话说，感染的人越多，新感染的人数就会越高。

这种趋势不可能永远持续下去。最终，一旦每个人都被感染，增长率必须为零。考虑人口规模的扩展模型称为逻辑斯蒂增长模型。

本文将展示逻辑建模的一个替代方案。我们将把病毒的传播视为非平稳过程。增长率随时间变化的原因如下:

*   随着越来越多的人被感染，受感染的人群在缩小。
*   如果感染人数变得太多，政府将采取行动，并采取措施，如隔离。
*   一段时间后，可能会发现预防感染的疫苗。

为了对非平稳增长率建模，将在有限的分析时间间隔(这里我们将采用一周-7 天)上拟合指数曲线，并且通过仅采用该时间间隔的数据，在最小二乘法意义上拟合生长参数。分析时间间隔的长度代表了经典的[偏差-方差权衡](/understanding-the-bias-variance-tradeoff-165e6942b229)。间隔太短会导致高方差，间隔太长会违反平稳性假设并导致偏差。

时间序列通过将分析时间间隔的起点滑动(移动)一天来表示。因此，我们每天都可以获得增长率。例如，增长率的变化揭示了哪些措施是有效的。

我们用于分析的数据来自“欧洲疾病预防和控制中心”。

下面是获取数据的 Python 代码片段:

我们在窗口开始日“x 零”采用以下模型:

![](img/803bbb2d17edbb7ac18532f16c7da3f9.png)

并获得线性关系

![](img/96ca6cc1e283c1da6bf7578f4f952fab.png)

通过采用 Moore-Penrose 伪逆(LS 拟合),可以容易地获得参数 log{ *a* 和 *b* 。直接方法的缺点是数据的对数失真。较小的样本比较大的样本权重更大。为了补偿这种影响，可以应用数据点的加权(使用平方根加权)。

为了最终获得不最小化对数距离的最小平方拟合，最初获得的解被馈送到非线性 LS 解算器，例如 Scipy 的曲线拟合工具。初始解确保找到正确的局部最小值。

我们现在来看两个例子——意大利和中国。意大利仍在努力应对指数级增长的人口，而中国的增长已经稳定下来。

![](img/5fb56f0c59179bbefa9d5387b95be73e.png)

7 天滑动分析窗口的指数拟合——意大利案例。滑动窗口的起始位置是彩色编码的(从红色到蓝色的彩虹色图)

![](img/70e4e5f67a7f4804b95c0d96762cd193.png)

7 天滑动分析窗口的指数拟合——以中国为例。

滑动 7 天窗口的每个起点都产生不同的增长率。因此，我们每天得到不同的指数曲线。分析窗口的开始日期通过彩虹色图进行颜色编码。第一次拟合显示，意大利和中国的指数增长更强劲。两国政府都已采取措施防止进一步传播，感染率的下降清楚地表明了这一点。然而，中国采取了更严厉的措施，停止了指数增长；它的曲线已经看起来像逻辑增长。整个时间序列的指数拟合失败，如红色虚线所示。

显示非平稳行为的另一种方式是显示每天的加倍间隔。加倍间隔提供了感染人口加倍前的天数。它直接从拟合的参数中获得。通过解这个方程

![](img/907042dd5a16c33c6694ea78795e325e.png)

对于加倍间隔 *d* 给出

![](img/a8a06c6b616477a2b2695ff1bce8b6ae.png)![](img/e2d0895eeede86f6a7df4471ac46765f.png)

意大利加倍音程。

![](img/a722a640cd699bb06fcf2786c950ad66.png)

中国加倍间隔。

中国的翻倍率几乎比意大利高出一个数量级。这说明了为什么意大利目前遭受新冠肺炎疫情。

要重现数据或说明任何其他国家，可以运行 GitHub 上的代码。

[](https://github.com/ezoechma/corona) [## ezoechma/corona

### 新冠肺炎数据的小型数据科学项目。创建一个帐户，为 ezoechma/corona 的发展做出贡献…

github.com](https://github.com/ezoechma/corona) 

***编者注:*** [*走向数据科学*](http://towardsdatascience.com/) *是一份以研究数据科学和机器学习为主的中型刊物。我们不是健康专家或流行病学家，本文的观点不应被解释为专业建议。想了解更多关于疫情冠状病毒的信息，可以点击* [*这里*](https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports) *。*