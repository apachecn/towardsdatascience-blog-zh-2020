# 比较最佳免费金融市场数据 API

> 原文：<https://towardsdatascience.com/comparing-the-best-free-financial-market-data-apis-158ae73c16ba?source=collection_archive---------9----------------------->

## 作为一名数据科学家、交易员或投资者，如果你想分析金融市场数据——股票市场或加密数据，从这里开始吧。

![](img/3a0b02e2620e5b527ac538f65f191bab.png)

克里斯·利维拉尼在 [Unsplash](https://unsplash.com/s/photos/finance?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

在我们的世界里，很少有东西像金融市场和数据这样紧密相连。金融市场的整个功能是基于其参与者对可用信息和从所述信息中综合的知识采取行动；目标是以他们认为有利的价格购买或出售资产。

这种机制设定了市场价格，进而赋予市场另一个关键属性——数据来源。不管有效市场假说的有效性，以及价格的客观正确性，很少有东西能像市场数据那样捕捉到集体情绪。

此外，可用数据的粒度随着时间的推移而增加，现在可以捕捉个人情绪以及集体情绪。其结果是，如此丰富、如此广泛、拥有如此多市场历史的任何数据源都很少有相似之处。

![](img/506e10246df475e660cf785967fb5f28.png)

照片由 [Aditya Vyas](https://unsplash.com/@aditya1702?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/financial-market?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄

例如，纽约证券交易所自 1792 年就已经成立了。)而如今，据说仅美国的纽约证券交易所这样的主要交易所平均每天就产生大约 300 亿个市场事件。

鉴于这些市场涉及大量资金，以及不断寻求优势的猫鼠游戏，寻求更多更好的数据并不奇怪。

虽然这些天来市场通过销售其数据产品获得了可观的收入，但市场数据分析领域仍然有许多优秀的、免费的切入点。这些 API 中的一些还提供关于加密资产以及来自股票市场的信息。

因此，在本文中，我比较了几个顶级金融市场数据 API 的自由层。我希望它们对你有用。

# API 比较—概述

## IEX 云

IEX 是一家初创股票交易所，其联合创始人布拉德·山因迈克尔·刘易斯的书《闪光男孩》而出名

IEX 的价值主张是，它的目标是成为一个交易所“*，消除行业中一些最糟糕的做法“* ( [文章](https://www.theverge.com/2016/6/17/11957258/iex-sec-approves-stock-exchange)濒临破产)*。* IEX 云([网站](https://iexcloud.io))是 IEX 的数据 API 分支，提供如下免费层:

![](img/65e6b4aaaea935f37babd54b62b41258.png)

IEX 云免费层(截至 2020 年 3 月 9 日)

## 廷戈

它们从 2014 年就已经存在了(见[这篇关于 2015 年 HackerNews 的讨论](https://news.ycombinator.com/item?id=10762913))，如果没有别的，存活这么久可能是其可靠性和可行性的一个好迹象。

他们的自由层功能概述如下:

![](img/c52c12fb56f43f10221688c6d83963b6.png)

Tiingo 自由层(截至 2020 年 3 月 9 日)

## Quandl

Quandl 自 2013 年以来一直存在，现在是纳斯达克的一部分。

他们的使命不仅仅是收集股票市场数据，因此他们从大量广泛的来源提供各种不同领域的数据集。虽然不是所有的数据产品都是免费的，但是他们的财务数据 API 是免费的，有以下限制:

![](img/dc6540a1a0e036c9925113fc14439793.png)

Quandl 自由层(截至 2020 年 3 月 9 日)

有趣的是，Quandl 似乎还提供了为 R、Python 和 Excel 编写的原生工具，旨在使下载数据更容易。

## 阿尔法优势

除了这种相对宽泛的简介，Alpha Vantage 网站上关于他们成立的时间、他们是谁以及该组织代表什么的信息相对较少。

![](img/faa19e4bd5cf7bba08e25d0094be9bb1.png)

关于 Alpha Vantage ( [链接](https://www.alphavantage.co/#about))

尽管如此，他们确实提供了一个如下的免费层，并且看起来使用相对广泛。

![](img/d78a422a9560d81c7c46df4ad4243ef3.png)

Alpha Vantage 自由层(截至 2020 年 3 月 9 日)

## WorldTradingData

他们的网站([链接](https://www.worldtradingdata.com))同样包含很少的关于他们是谁的信息，但与其他网站类似，他们提供一个免费层，并因此相对知名。

# 详细的自由层比较

每个网站上的信息布局使得产品比较非常困难，所以下面是我的尝试:

## 有用数据

幸运的是，所有这些 API 似乎都提供了**历史**和**当日**美国股票价格，以及**外汇**数据。因此，就数据可用性而言，任何这些服务都可能满足您的大部分需求。

对于**加密货币**数据，IEX、Quandl 和 Tiingo 提供这些数据，而 Alpha Vantage 和 WorldTradingData 则没有。

如果你在 API 访问额外(非价格)信息后，IEX 也提供 API 访问**基本面**和**新闻**数据。Quandl 的部分数据源也是免费的。

## 自由层数据限制

因为它有点复杂，让我们把 IEX 留到最后，看看其他的:

*   **Tiingo** :每月 500 个唯一符号，500 个请求/小时，20000 个请求/天，5gb/月([来源](https://api.tiingo.com/about/pricing))。
*   **Quandl** : 300 个请求/10 秒，2000 个请求/10 分钟，50000 个请求/天，如果经过认证([来源](https://help.quandl.com/article/68-is-there-a-rate-limit-or-speed-limit-for-api-usage))。(每 10 分钟 20 个电话，如果匿名，每天 50 个电话)
*   Alpha Vantage : 5 个请求/分钟，500 个请求/天([来源](https://www.alphavantage.co/support/#support))。
*   **WorldTradingData** : 250 个请求/天(25 个当天请求/天)([来源](https://www.worldtradingdata.com/pricing))。

现在，让我们来看看 IEX。他们有每月 50，000 条核心“消息”的自由层限制。每种类型的请求将使用不同数量的消息，因此数据越多，使用的消息就越多。

50，000 条消息并不是一个很大的数目。平均来说，不太可能有 Tiingo 和 Quandl 那么多数据(虽然这取决于使用情况)，所以我会建议明智地使用它们。

该计算器将为您提供使用特定数据端点的每个月将使用多少“消息”的估计。

[](https://iexcloud.io/calculator/) [## 定价计算器| IEX 云

### IEX 云是构建金融科技应用最简单、最容易实现的方式。

iexcloud.io](https://iexcloud.io/calculator/) 

令人高兴的是，IEX 是唯一一个提供**沙盒测试模式**的公司，这种模式将返回“虚拟”或随机数据。沙盒模式可以用来测试和优化你的代码，看看你在真实的、实时的模式下会使用多少消息，对个人来说这是一个很大的好处。

## 证明文件

总的来说，我发现 IEX 云文档是我看过的所有文档中最全面的。

以下是他们文档的链接:

[](https://iexcloud.io/docs/api/) [## IEX 云 API | IEX 云

### IEX 云是构建金融应用程序最简单的方式。

iexcloud.io](https://iexcloud.io/docs/api/) 

例如，IEX 文档清楚地显示了历史价格请求的响应属性:

![](img/0b2bd9a9d753d002e446985ccfb54377.png)

IEX 文档—响应属性([链接](https://iexcloud.io/docs/api/#historical-prices))

IEX 文档包括请求示例、参数列表、响应示例和属性，以及版本、错误代码和安全说明等其他方面。

据我所知，IEX 是名单中最大的组织，这在这里的全面性上得到了体现。

这并不是说其他人的文件是缺乏的，更多的是 IEX 的文件是非常全面的。

Tiingo 的文档在这里:

 [## 股票市场工具| Tiingo

### 一个金融研究平台，致力于为所有人创造创新的金融工具，同时采用座右铭…

api.tiingo.com](https://api.tiingo.com/documentation/general/overview) ![](img/b3a1756e2571977f5688025773d65961.png)

Tiingo 文档—响应属性([链接](https://api.tiingo.com/documentation/end-of-day)

Quandl 在这里:

 [## Quandl 文档

### 获取您的免费 API 密钥，开始使用我们的数据。开始使用我们强大的数据 API 分析所需的一切…

docs.quandl.com](https://docs.quandl.com) ![](img/628a2c1c6ee9a186724e8b195890569c.png)

Quandl 文档—响应属性([链接](https://docs.quandl.com/docs/parameters-2))

这两个都非常详细，有示例请求和参数，以及响应示例和参数。虽然可能不如 IEX 文档那样令人印象深刻，但这些仍然相当可靠。

最后，我将把 Alpha Vantage 和 WorldTradingData 文档放在最后一层。

[](https://www.alphavantage.co/documentation/) [## Alpha Vantage API 文档

### Alpha Vantage 的 API 文档。Alpha Vantage 为实时和历史股票和权益提供免费的 JSON APIs

www.alphavantage.co](https://www.alphavantage.co/documentation/)  [## API 文档|世界贸易数据

### 我们的 API 通过我们的 API 提供对 JSON 或 CSV 格式的实时和历史股票数据的有效访问…

www.worldtradingdata.com](https://www.worldtradingdata.com/documentation) 

虽然它本身没有*遗漏*任何信息，但它们显然不像其他的那样完整或有解释力。

根据你对编程和 API 的经验水平，你可能会从 IEX / Tiingo 和 Quandl 的更全面的文档中获益更多。

# 结论

我试图在这里给出顶级免费金融市场数据 API 的简要概述。

上面列出的五个 API 都是非常惊人的数据服务，尤其是考虑到它们的运行是免费的。如上所述，历史数据或当天数据等常见数据类型可从所有提供商处获得，选择哪种服务在很大程度上取决于个人选择。

说到这个，作为金融界的爱好者，我个人更喜欢 IEX。对于像我这样的临时用户，我希望学习曲线越浅越好，他们的大量文档会非常有帮助，就像他们的沙盒模式一样。不过，如果我需要更多的数据，Quandl 或 Tiingo 似乎也是不错的选择。

不过，总的来说，我(非专家)的观点是，所有这些似乎都是进入金融市场数据分析世界的非常可靠的切入点，您可能希望选择一个最适合自己的。

我希望你觉得这是有用的，如果你有任何意见，或者我犯了什么错误，请告诉我！

在接下来的几周里，我将使用来自一个或多个 API 的数据进行分析。

(如果你想知道为什么我没有包括雅虎！，这是因为它已被官方弃用——尽管许多人似乎仍在使用它)

*   *注意:这篇文章包含一个亚马逊联盟链接，这意味着在你没有额外费用的情况下，如果你购买，我会得到一小笔佣金。*

如果你喜欢这个，比如说👋/关注[推特](https://twitter.com/_jphwang)，或点击此处获取更新。如果你错过了，看看这篇关于可视化时间序列数据的文章。

[](/effectively-visualize-data-across-time-to-tell-better-stories-2a2c276e031e) [## 随着时间的推移有效地可视化数据，以讲述更好的故事

### 使用 Python 和 Plotly 构建清晰易读的时序数据可视化，以支持您的叙述。

towardsdatascience.com](/effectively-visualize-data-across-time-to-tell-better-stories-2a2c276e031e) 

这是关于用 Plotly Dash 建立一个网络数据仪表板。

[](/build-a-web-data-dashboard-in-just-minutes-with-python-d722076aee2b) [## 使用 Python 在几分钟内构建一个 web 数据仪表板

### 通过将您的数据可视化转换为基于 web 的仪表板，以指数方式提高功能和可访问性…

towardsdatascience.com](/build-a-web-data-dashboard-in-just-minutes-with-python-d722076aee2b)