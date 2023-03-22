# 使用 python 为 NLP 抓取 Twitter 数据

> 原文：<https://towardsdatascience.com/scraping-twitter-data-using-python-for-nlp-d898e14cacfe?source=collection_archive---------30----------------------->

## 了解如何用几行代码从 twitter 创建自己的数据集。

![](img/7f7441933f853d7050559c4c61847cd4.png)

约书亚·阿拉贡在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

> “我们相信上帝。所有其他人都必须带数据。”— [爱德华·戴明](https://www.deming.org/theman/overview)

如果您是从 NLP 这个不可思议的领域开始，那么您会想要接触真实的文本数据，您可以使用这些数据来研究您所学到的概念。Twitter 是这类数据的绝佳来源。在这篇文章中，我将展示一个刮刀，你可以用它来刮你感兴趣的话题的推文，一旦你获得了你的数据集，你就会变得很无聊。

我使用了这个神奇的库，你可以在这里找到。我将介绍如何安装和使用这个库，并建议一些使用并行化使整个过程更快的方法。

# 装置

可以使用 pip3 通过以下命令安装该库

```
pip3 install twitter_scraper
```

# 创建关键字列表

下一个任务是创建一个你想用来抓取 twitter 的关键词列表。你会在 twitter 上搜索这些关键词，因此重要的是你要列出一个你感兴趣的关键词的综合列表。

# 抓取一个关键词的推文

在我们运行程序提取所有关键字之前，我们将用一个关键字运行程序，并打印出我们可以从对象中提取的字段。在下面的代码中，我展示了如何迭代返回的对象并打印出您想要提取的字段。您可以看到，我们提取了以下字段

1.  推文 ID
2.  是转发还是不转发
3.  推文时间
4.  推文的文本
5.  对推文的回复
6.  转发总数
7.  喜欢推特
8.  推文中的条目

# 对所有关键字按顺序运行代码

既然我们已经决定了要从我们的对象中存储什么样的数据，我们将依次运行我们的程序来获取我们感兴趣的主题的 tweets。我们将使用我们熟悉的 *for* 循环来逐个检查每个关键字并存储成功的结果。

# 并行运行代码

从[文档](https://docs.python.org/3/library/multiprocessing.html)中，

> 多重处理是一个支持使用类似于线程模块的 API 生成进程的包。多处理包提供了本地和远程并发，通过使用子进程而不是线程有效地避开了全局解释器锁。因此，多处理模块允许程序员在一台给定的机器上充分利用多个处理器。

首先，我们将实现一个函数来抓取数据。

接下来，我们将创建子流程来并行运行我们的代码。

如您所见，我们将处理时间减少到了顺序执行的 1/4。您可以将此方法用于类似的任务，并使您的 python 代码更快。