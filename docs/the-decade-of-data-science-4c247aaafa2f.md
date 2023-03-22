# 数据科学的十年

> 原文：<https://towardsdatascience.com/the-decade-of-data-science-4c247aaafa2f?source=collection_archive---------13----------------------->

## 从沃森到白宫，看看过去 10 年中最有价值的成就。

![](img/6e961874b1c8dfc5b2408376e220dbd8.png)

对于数据科学来说，这是地狱般的十年——沃森主导了《危险边缘》(Jeopardy)([2011](https://www.nytimes.com/2011/02/17/science/17jeopardy-watson.html))，白宫宣布了第一位首席数据科学家( [2015](https://obamawhitehouse.archives.gov/blog/2015/02/18/white-house-names-dr-dj-patil-first-us-chief-data-scientist) )，Deepfakes 提供了所有我们想要的尼古拉斯·凯奇电影( [2017](https://www.youtube.com/watch?v=_OqMkZNHWPo) )。甚至我们学科的名字，*数据科学*，也是最近 10 年来的。随着 2019 年即将结束，不可避免地会有类似上述日期特定事件的文章和列表。然而，在过去 10 年里，也出现了一些缓慢发展的重要趋势。当我想到现在的数据科学与 2010 年的数据科学相比时，有三个项目引起了我的注意。

# 1.我们自己的语言

数据科学家通常来自各种背景，数学、天文学或医学。这一切都有助于我们的工作，但拥有许多背景的早期缺点之一是，它导致了编程语言的巴别塔。2010 年初，一场语言战争开始了。STATA、SPSS、SAS、Matlab 和 Mathematica 等付费解决方案与 R、C++、Python、Julia、Octave 和 Gretl 等开源工具竞争。

起初，R 似乎有可能获胜。微软甚至通过收购 Revolution Analytics(一家提供 R 增强版的公司)进行了尝试。尽管处于领先地位，但 2015 年标志着向 Python 的转变。它令人印象深刻的软件包库、简单易学的语法和稳定的性能都对它有利。

![](img/65d844bd735d5661d2113781624aee10.png)

来源:[谷歌趋势](https://trends.google.com/trends/explore?date=2010-01-01%202019-12-31&geo=US&q=R%20Data%20Science,Python%20Data%20Science)

快进到今天。战争已经结束，新的边界已经划定，Python 是首选语言。这并不是说所有其他语言都死了。r 仍然在统计学中大量使用，根据您的行业，您可能会使用 SAS 或 Matlab。然而，答案十有八九是 Python。这种共享语言的好处不能被夸大。这使得阅读他人的作品更容易，代码也更容易共享。

# 2.Jupyter 笔记本和 GitHub

搜索任何数据科学主题的教程，你找到的任何文章几乎肯定会包含 GitHub 上托管的 Jupyter 笔记本的链接。这种做法非常普遍，基本上是一种潜规则。理所当然:这是一个强大的组合。Jupyter 笔记本将你的文档和代码合并成一个文件，使得理解*是什么*和*为什么*更加容易。将这与 GitHub 结合起来，你不仅有了一种解释你的作品的方法，也有了一种分享它的方式。GitHub 甚至采取措施支持 Jupyter 笔记本，允许它们直接在浏览器中呈现。

![](img/f58284b2397b4f998da72dfe143a127a.png)

一台托管在 [Github](https://github.com/Sentdex/QuantumComputing/blob/master/Tutorial%201%20Introduction.ipynb) 上的笔记本电脑，来自 Sentdex 的量子计算

Python 给了我们一种共同的语言，Jupyter 和 GitHub 给了我们一种共同的语法和分享的礼仪。

# 3.数据集的激增

10 年前，数据要难得多。即使你找到了你想要的主题的数据集，也很可能是很小的。那里有数据，但是没有组织，格式不一致，人们不太可能分享他们收集的数据。在我有 MNIST 或泰坦尼克号数据集之前，我有来自 STATA 的“汽车”数据集。这是一个 1978 年的车辆收集，包括头部空间和燃油效率等功能，并附有高达 74 项观察。

相比之下，现在，你可以让公司把他们的数据公布给全世界。在某种程度上，Kaggle 已经成为企业数据的火种。各公司不再犹豫不决，而是热情地分享数据，希望能从一个热切的年轻定量分析师那里获得一把。地方政府也加大了行动力度。像芝加哥和纽约这样的城市已经使任何人都有可能获得从路况到啮齿动物观察等主题的数据。搜索数据集的资源也有所改进，比如使用了[r/datasets](https://www.reddit.com/r/datasets/)subredit 和 [Google Dataset Search](https://toolbox.google.com/datasetsearch) 等工具。如果数据是新的石油，那么今天的每个数据科学家可能都有点像*中的丹尼尔·戴·刘易斯*。

数据科学家查看可供他们使用的广阔信息领域

# 共同的线索:开放科学

在上述主题中有一条贯穿的线，它们每一个都代表了向[开放科学](https://en.wikipedia.org/wiki/Open_science)的发展，或者工具、方法和数据应该公开的哲学。我认为，采纳这种理念是我们社区在过去十年中最有利可图的投资之一，有助于我们的成长、扩展我们的能力并提高我们的工作质量。

就增长而言，数据科学的大门现在向所有人开放，而不到十年前，进入数据科学需要付出高昂的代价。在 Python 之前，SAS 是最接近标准语言的东西，在 Jupyter 笔记本之前还有 Wolfram 笔记本。但是这些解决方案不是开放和免费的。根据服务的不同，你可能已经支付了 800-8000 美元，只是为了用“行业标准”工具进行回归。甚至他们的网站也不方便新手使用。访问其中的任何一个网站，你都会看到几十个不同的版本和链接，询问你是否想“获得报价”，这让你的体验不像是一头扎进一个动态学科，而更像是购买一辆二手车。

在过去的十年里，用于数据科学的商业软件已经衰落。我不会声称知道确切的原因，但我会给出我的观点:没有什么比价格标签更能消除好奇心。当我接近本科毕业时，我记得我在想“我喜欢做数值分析，但是我负担不起 STATA。我估计我还是学这个 R 的东西吧。”我不是一个人，有大量的业余爱好者涌入，他们好奇并渴望测试数据科学的水域。

除了容易进入，开放科学还扩展了每个人能力的深度和广度。一个数据科学家不一定是一种资源。有一个巨大的代码库，来自世界各地的贡献者。这可能采取 Python 包、中等教程或堆栈溢出答案的形式。这个代码库使项目更像是混合和匹配乐高积木，而不是从零开始构建。

堆栈溢出是数据科学的难题吗？

这种开放性也有助于保持我们工作的诚实。伴随着数据科学，这十年也给我们带来了短语“复制危机”虽然欺诈性工作没有万灵药，但透明度是一种强有力的预防措施。十年来我最喜欢的文章之一，[科学论文过时了](https://www.theatlantic.com/science/archive/2018/04/the-scientific-paper-is-obsolete/556676/)，引用了 Wolfram 在谈论笔记本时的一句名言:“这里没有废话。它就是它，它做它该做的。你不能篡改数据。”

# 向前看，向后看

在某些方面，这不仅仅是数据科学的好十年，而是数据科学的*十年。我们进入了 2010 年代的时代精神。我们被授予最性感职业的称号，我们得到了布拉德·皮特和乔纳·希尔的电影，数百万人看到 AlphaGO 成为世界冠军。在某些方面，我觉得这十年是我们走向成熟的十年。虽然下一个十年将带来许多改进的工具和方法，但 2010 年将是我带着喜爱和怀旧的感觉回顾的时候。*