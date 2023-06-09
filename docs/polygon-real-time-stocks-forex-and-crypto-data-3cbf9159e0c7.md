# 多边形:实时股票，外汇和加密数据。

> 原文：<https://towardsdatascience.com/polygon-real-time-stocks-forex-and-crypto-data-3cbf9159e0c7?source=collection_archive---------50----------------------->

## 一个激动人心的历史和实时财务数据平台

![](img/0264f71b36e900ae9aeb38b84f0c3b8c.png)

你可能听过这句名言“数据是新的石油”太多次了。不管你对这一论断的看法如何，人们普遍认为数据对每个行业的创新过程都至关重要。特别是金融行业，鉴于该行业的高度动态性，访问高质量和最新数据是至关重要的。最近，我一直在研究一个需要实时数据(股票、外汇和加密货币数据)的交易机器人，我碰巧选定了一个名为 Polygon 的非常好的平台，它以一种漂亮、实惠和记录良好的服务提供了我所需要的一切。

## 引入多边形

我从事的项目需要在一段时间内实时加密货币数据。在谷歌搜索并询问了各种平台后，我最终选择了 Polygon。我发现这项服务价格有竞争力，稳定，文档也很好。由于我对这个平台的积极体验，我决定通过这篇文章分享我的经验和代码给任何可能有同样遭遇的人。

Polygon 通过 WebSockets 或 RESTful APIs 提供流客户端，用于访问大多数流行编程语言 Python to Go 中的实时数据。他们甚至有一个专用的 Python 包，用于更直接的访问。因为这个项目需要 Python，所以我选择了他们的 Python 包。

说够了，让我们进入正题，在安装了[这个 python 包](https://github.com/polygon-io/client-python)之后，开始玩一些实时加密货币数据:

```
**pip install polygon-api-client**
```

> **注意**:为了简洁起见，这篇文章将专注于加密货币，但代码将包括对实时股票/股票、外汇数据感兴趣的读者的评论。访问需要一个 API 密钥，所以请前往[https://polygon.io/signup](https://polygon.io/signup)获取密钥。

## 实时加密数据

该项目的目标是在特定时期内收集一些选定加密货币的实时数据。在下面相对简单的脚本中，我演示了如何使用 Polygon 的 Python 客户端与实时流数据进行交互。

该脚本的设计考虑了平台支持的其他类型的资产，因此应该很容易针对各种用例进行调整。该平台提供的广泛且用户友好的文档将比每个定制场景所需要的更多。

## 摘要

在这篇短文中，我介绍了 Polygon，它是一个可行的优秀平台，适用于需要使用 Python 客户端的各种实时财务数据的项目或产品。我推荐对这类服务感兴趣的读者访问他们关于 [WebSockets](https://polygon.io/sockets) 和[RESTful API](https://polygon.io/docs/#getting-started)的文档，探索他们为加密货币/股票/外汇数据提供的大量产品。直到下一个帖子，编码快乐！

一如既往的期待反馈(好的坏的)！这篇文章的代码和所有其他文章一样，可以在这个 [GitHub 库](https://github.com/PyDataBlog/Python-for-Data-Science)上找到。