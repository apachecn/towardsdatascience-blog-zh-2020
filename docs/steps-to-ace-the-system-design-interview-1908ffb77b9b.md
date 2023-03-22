# 赢得系统设计面试的步骤

> 原文：<https://towardsdatascience.com/steps-to-ace-the-system-design-interview-1908ffb77b9b?source=collection_archive---------33----------------------->

![](img/132f80e11bc0eae37bddea02c734e3ad.png)

约翰娜·布格特在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

(这个帖子也在[我的博客](https://kylelix7.github.io)里)

# 澄清

系统设计面试和编码面试一样，不仅测试候选人的技术技能，还验证候选人是否能解决一个没有很好定义的问题。问题问得模糊笼统。候选人的工作是找出需求并提出合适的设计。应聘者在得到问题后马上投入设计是一个常见的错误。对于 Twitter 上的 design 这样的问题，你可能需要弄清楚需要考虑哪些核心功能，注册？简介？文字推文？视频/图片推文？时间线？其他技术要求可能是每秒读写？请求的峰值/平均值？用户基本位置？

# 工作解决方案的关键组件

一旦你有了需求，你就可以开始考虑系统或者子系统的结构，如果它是针对一个以上的特性的话。首先找出一个可行的解决方案总是好的，而不是试图提出一个完美的最优解决方案。试着想出一个包含所有必要组件的简单系统。在白板上展示系统。组件包括应用服务器、数据存储(SQL 或 NoSQL)、代理、CDN、消息队列、事件总线等。选择基本解决方案所需的组件。解释为什么需要这些组件，它们应该如何连接在一起，以及用户如何与系统交互。

# 列出 API

API 是组件间通信的表达。能够设计一套逻辑 API 是候选人的优势。对于 RESTful API，最好遵循 REST 惯例，使用适合 CRUD 等资源操作的 HTTP 动词。路径应该是代表资源的名词。这也有助于展示您可以在设计中正确地使用查询参数和请求体。

# 最佳化

然后，你需要优化系统。当考虑优化时，你需要优化正确的东西。最好是针对常见用例进行优化。例如，如果从数据库中读取数据比向数据库中写入数据更常见，那么在数据请求者和持久数据存储之间引入缓存是有意义的。它有助于更快地提供热数据，并且缓存失效的频率会降低，因为写操作并不多。但是，为写入密集型系统引入缓存会对性能产生负面影响，因为这将经常导致缓存失效。其他优化可以是根据用户的位置将请求分配到不同的数据中心。将数据库划分为碎片来处理请求。正确设计表中的键，使请求流量均匀分布到分区。

# 可量测性

随着用户群的增长会怎么样？毫无疑问，您将需要设计一个水平可伸缩的系统。水平可伸缩性意味着系统可以通过增加越来越多的商用计算能力来处理更多的请求。这比增加一台服务器的马力更具成本效益。

# 交易

毫无疑问，你听说过很多流行的软件来构建一个分布式系统。比如 MongoDB，ElasticSearch，Memcached，Kafka 等等。然而，随意向面试官抛出这些流行语并不足以打动他们。对你来说，解释选择和为什么不选择另一个是很重要的。比如 MongoDB 给你的好处有哪些是 MySQL 不会的？也许你的应用程序并不关心数据模型之间的关系，比起强一致性，它更喜欢更好的性能。再比如，为什么你会更喜欢用 Kafka 构建事件驱动的系统。也许您的业务逻辑是一个长流程，需要异步完成。也许你有一些子系统需要知道这个事件。

# 错误处理

软件从来都不是完美的，所以作为候选人，你应该解释你的系统是如何处理错误的。一个关键点是，您能够识别单点故障，并提供解决方案来降低整个系统的故障率。另一个常见的错误场景是流量太大，系统无法处理。一种常见解决方案是节流。节流是限制系统请求数量的过程。通过限制每个客户端的请求数量，系统可以具有相对可预测的工作负载。因此，它也有助于计划社交。

# 临终遗言

这些是您在系统设计面试中需要考虑的一些要点。如果您想了解更多关于系统设计的技术细节，我推荐使用[设计数据密集型应用](https://amzn.to/3w3KfLK)和[研究系统设计](https://www.educative.io/courses/grokking-the-system-design-interview?aff=VEzk)作为准备的参考。祝你好运。

![](img/591f0ff43d4d36b3169b36f272d1abd8.png)

以前的帖子:

[我关于 FAANG 访谈的帖子](https://medium.com/@fin.techology/my-posts-about-faang-interview-20e529c5f13f?source=your_stories_page---------------------------)

[我关于金融和科技的帖子](https://medium.com/@fin.techology/my-posts-about-finance-and-tech-7b7e6b2e57f4?source=your_stories_page---------------------------)