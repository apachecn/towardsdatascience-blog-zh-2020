# 介绍 Company2Vec

> 原文：<https://towardsdatascience.com/introducing-company2vec-helping-company-analysis-with-machine-learning-c6790d7a6bf5?source=collection_archive---------41----------------------->

## 数据科学/机器学习

## 用机器学习帮助公司分析

![](img/2f20fa6a405454111e145b564e9e3305.png)

**TLDR** : *我在 Github 上为数据科学家创建了一个包，可以从公司名称生成一个公司的矢量嵌入图——详情请见* [*此处*](https://github.com/eddiepease/company2vec)

# *开发包装的动机*

*几年前，我在一家做大量简历分析工作的公司担任机器学习的角色。我的任务是编写一个算法，根据一个人的简历预测他的下一个职位(详情见[)。虽然我的算法不包括公司的推荐，但我很好奇它们是如何被包括在内的。我很快意识到这是一个非常困难的问题，公司里与我交谈过的其他人也证实了这一点。](https://github.com/eddiepease/career_path_recommendation)*

*从许多简历来看，原因显而易见。同一个公司可以有多种不同的写法。为巴克莱银行工作的人可以在他们的简历上输入“巴克莱”/“巴克莱银行”/“巴克莱资本”/“巴克莱资本”/“巴克莱银行”等等中的任何一个。但这仅仅是问题的开始。如何处理子公司？如何处理品牌名称与其有限公司名称不同的公司？缩写呢？*

*以类似的方式，过了一段时间，我在一家大型制造公司工作，该公司希望使用机器学习来帮助他们的销售线索生成。当我查看他们的现有客户名单时，我意识到同样的问题也存在。*

# *什么是向量嵌入？*

*在任何下游机器学习任务中分析公司的最佳方式是创建公司向量嵌入。但是什么是向量嵌入呢？*

*嵌入是离散—分类—变量到连续数字向量的映射。例如，单词“book”可以用向量(1，2，3)来表示。这非常有用，因为它最多可以做 3 件主要的事情:*

1.  *识别相似的单词/实体。例如，识别单词“cat”与单词“kitten”非常相似。*
2.  *机器学习任务的输入，特别是自然语言处理*
3.  *对于概念和类别之间关系的可视化——你能在下面的图片中看到相似的单词之间有相似的向量关系吗？*

*那么什么时候公司矢量嵌入会有用呢？下面是一些潜在的用例(当然还有很多)。*

1.  *潜在客户——寻找与你过去的销售对象相似的公司*
2.  *映射不同公司之间的关系(例如，客户-供应商关系)*
3.  *分析同行业公司之间的差异*
4.  *工作推荐*
5.  *…以及许多其他下游机器学习任务！*

# *包装详情*

*为了帮助解决这个问题，我开发了一个 python 包来生成公司矢量嵌入——见这里的[包和如何使用它的详细说明](https://github.com/eddiepease/company2vec)。*

*![](img/8c205c1980fabfe3e142b91e7f3c9f20.png)*

*照片由[克莱门特 H](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄*

*在大多数情况下，你可能会想用这个，我认为你会有一个公司名称。鉴于缩写/首字母缩略词等的所有问题，该软件包使用一个搜索 API(每月最多 1000 次免费请求)来查找给定公司名称的公司网站。然后，该软件包使用 [scrapy](https://scrapy.org/) 对网站进行一次广泛而浅显的搜索。然后，将抓取的文本与预训练的手套向量嵌入相结合，以创建公司嵌入。*

*该软件包有两种用途。首先，有一个“快速启动”功能，可用于快速试验该包。如果你想大规模使用它，有一个 [Klein](https://klein.readthedocs.io/en/latest/) web 应用程序和一个 Dockerfile(顺便说一下，由于 scrapy 的多线程工作方式，必须使用 Klein 而不是 Flask)。这可以用来封装一个 web 应用程序，然后部署到云上。*

*在以下情况下，此软件包工作正常:*

*   *您不想付费访问公司信息数据库/没有时间根据该数据库的公司条目标准化名称*
*   *这些公司通常用缩写形式表示。*
*   *这些公司的网站大部分都是相当静态的内容，并且很好地概述了公司的业务*

# *此包的限制*

*然而，这个包肯定不是完美的，是一个正在进行的工作。在以下情况下，它的效果不太好:*

*   *如果大部分网站内容没有描述该公司，例如新闻网站*
*   *如果没有网站(显然……)*
*   *如果一家大公司使用相同的缩写/名称，使用缩写的小公司可能会很难被选中。*

*同样值得记住的是，如果网站上的大部分文本频繁更新，那么每次运行包时嵌入都会改变，影响您的下游分析。*

# *结论*

*如果你是一名数据科学家，并在过去努力有效地分析公司，希望你会发现这很有用。一定要让我知道你的想法，并为帮助开发这个包做出贡献！*