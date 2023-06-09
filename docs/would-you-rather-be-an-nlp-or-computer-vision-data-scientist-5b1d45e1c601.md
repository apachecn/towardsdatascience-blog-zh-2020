# 你更愿意成为 NLP 还是计算机视觉数据科学家？

> 原文：<https://towardsdatascience.com/would-you-rather-be-an-nlp-or-computer-vision-data-scientist-5b1d45e1c601?source=collection_archive---------14----------------------->

## 意见

## 深入了解这些受欢迎的数据科学家角色。

![](img/b64ed947abfe4dd005d9c2366e94092e.png)

[JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/occulus?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【1】上的照片。

# 目录

1.  介绍
2.  数据科学
3.  自然语言处理
4.  计算机视觉
5.  摘要
6.  参考

# 介绍

在申请数据科学家的职位时，您可能会在职位描述部分看到各种所需的技能。向下滚动，你会发现不同职位所要求的教育程度也是不同的。最重要的是，您会看到一个概述，概述了该角色，尽管职位的标题是相同的，但部分却有很大的不同。这种变化是由于不同类型的数据科学职位。然而，我注意到，随着公司了解他们在数据科学方面的专长，这些角色有了新的名称。数据科学的这两个热门分支是自然语言处理(NLP)和计算机视觉。根据你最终将为之工作的公司，或者目前为之工作的公司，一些职位仍将被称为数据科学，但重点是 NLP 或计算机视觉，而一些职位将是全面的数据科学。我将重点介绍 NLP 和计算机视觉，以便您可以找到更多信息，了解这两者的含义，以及各自的预期工资，以及哪个角色最终更适合您。

# 数据科学

数据科学是一个非常宽泛的术语，经常在人们中间引起争议，尤其是在技术领域。当前的数据科学家可能会根据他们在第一份工作中的经历，对他们认为数据科学真正是什么有一些偏见，但后来会意识到数据科学实际上是几个学科的总称。这些学科包括或围绕自然语言处理、计算机视觉、机器学习、统计学、数学、编程、数据分析、产品管理和商业智能。这真的取决于你和你工作的公司来决定你想要走什么样的道路，或者成为所有这些方面的多面手。专攻 NLP 或计算机视觉的一个好处是，你将知道你将进入什么领域，并可以专注于学习和提高每个职位所需的特定技能。

# 自然语言处理

有时，专门从事 NLP 的数据科学家也被称为 NLP 工程师。这种专业化专注于人类的自然语言，以及计算机如何参与消化这种非结构化的输入，然后输出结构化的、有用的意义。虽然这种类型的数据科学有无数的定义和例子，但我想给出我个人在 NLP 方面的专业经验。我主要参与过三种类型的 NLP 项目。*这三个项目包括:*

*   情感分析
*   主题建模
*   文本分类

这些项目有主要的概念，这些概念也可以应用于其他形式的 NLP。他们都共享相似的工具和代码来创建有益的输出。具体来说，我在 Python 编程语言中使用 NLP 最多。

**情感分析** —这种形式的自然语言处理关注给定文本的情绪或情感、极性和主观性。情感分析的典型工作流程是收集数据，对其进行预处理，然后对其进行表征。本质上，在这一点上，你将有你正在分析的每一个词，清理，并剥离，以便这些词可以被标记。下一部分通常被称为词性标注。一旦你确定了你所拥有的词的类型，比如形容词、名词和动词，你就可以很容易地应用一个库的功能，为每个文本分配一个极性分数。一些流行的情感 NLP 库是 TextBlob 和 Vader perspection。我在这里不会讲得太深入，但是如果你想写一篇关于 NLP 和这两个流行的库的文章，我很乐意这样做(*请在下面*评论)。情感分析可以被大多数企业广泛使用。*这里有一些可以应用情感分析的例子:*

—客户评论

—客户细分

—异常检测

—产品改进

*下面是情感分析的总结流程:*

```
gather datapreprocesstokenizePOS tagscoring
```

**主题建模** —这种形式的自然语言处理属于无监督学习的一个分支，帮助你找到由文本组成的文档的主题。在文档中查找主题最流行的方法之一是利用 LDA 或潜在 Dirichlet 分配。这是一种技术，最终输出的主题总结了流行的和重要的，关键短语从你的文本。*这里有一些可以应用主题建模的例子:*

—从课文中提出新的话题

—使用这些主题来分配新的监督学习标签

—通过手动搜索很难找到的见解

**文本分类** —这种形式的 NLP 是一种监督学习技术，有助于对新的数据实例进行分类，这些数据实例不一定只包含文本，也可以包含数值。比这两种 NLP 形式更广泛的是，您可以将文本分类视为一种典型的分类算法，其中标签是文本，一些特征也是文本。您将使用上述相同的技术对文本进行预处理、清理和提取含义。*这里有一些可以应用文本分类的例子:*

—对特殊动物进行分类

—将假新闻分类

—对银行交易进行分类

最流行的 Python 包是[nltk](https://www.nltk.org/)【2】，它代表自然语言工具包。它包含了几个库，这些库对于你用 NLP 技术解决问题是必不可少的。

[](https://www.nltk.org/) [## 自然语言工具包- NLTK 3.5 文档

### NLTK 是构建 Python 程序来处理人类语言数据的领先平台。它提供了易于使用的…

www.nltk.org](https://www.nltk.org/) 

***一个 NLP 工程师挣多少钱？***

> 根据[glass door](https://www.glassdoor.com/Salaries/nlp-engineer-salary-SRCH_KO0,12.htm)【3】统计，美国一名 NLP 工程师的平均工资为 114121 美元/年。

# 计算机视觉

我相信这个数据科学领域甚至比 NLP 更专业。计算机视觉关注图像和视频数据，而不是数字或文本数据。对我来说，计算机视觉的风险更大，因为它可以用于更多不一定依赖于洞察力，但需要安全措施到位的行业。想想 NLP 和情感分析如何分析某人评论的快乐，这种洞察力是有用和强大的，但不如计算机视觉那样有影响力或有害。下面我将重点介绍一些类型的计算机视觉。

**面部识别** —当你拿起手机时，你很可能会有一个安全功能，它会分析你的面部，看看是否真的是你试图访问你的手机。一个有益于面部识别项目的流行 Python 库被恰当地命名为 *face_recognition* 。您处理的由面组成的图像被编码为一个特征。基于面部的共同特征，您可以将(*或*)个别面部与相同或不同的面部进行匹配，以便最终“识别”面部。

**物体检测** —使用来自物体的信息，这种形式的计算机视觉可以帮助检测物体。OpenCV 是程序员和数据科学家使用的流行工具，他们希望专注于对象检测。

*你可以期待在*中找到计算机视觉的例子

—图像检测

— iPhone Face ID

—脸书照片标签

—特斯拉行人和汽车检测

***一个计算机视觉工程师挣多少钱？***

> 据[glass door](https://www.glassdoor.com/Salaries/nlp-engineer-salary-SRCH_KO0,12.htm)【4】报道，美国一名 NLP 工程师的平均工资为 99619 美元/年。

虽然这两个工资都很高，但我个人从招聘信息中看到，不仅计算机视觉工程师的工资高于报道的平均工资，NLP 工程师也是如此。因为数据科学中的这两个角色越来越专业化，我相信这就是为什么你可以期望有更高的工资。

# 摘要

![](img/7f16bab179eaf45fda01e6fc34ae6bde.png)

安妮·斯普拉特在[Unsplash](https://unsplash.com/s/photos/document?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【5】上的照片。

大多数数据科学家可能研究过某种形式的 NLP 或计算机视觉，无论是来自大学还是在线教程。数据科学中的这两个专业角色都非常受尊重，可以让无数行业受益。在回答“*你更愿意做 NLP 工程师还是计算机视觉工程师”这个问题时，最终取决于你的偏好和职业目标。*’。想一想你想从事什么类型的项目，想为哪个行业工作，想和哪个公司合作。数据科学领域的这两个职位都能给你的工作带来巨大的影响，所以这两个职位都会给你一次激励的经历。

*我希望你觉得这篇文章有趣并且有用。请随意在下面评论您作为一名普通数据科学家、NLP 工程师或计算机视觉工程师的经历。*

*感谢您的阅读！*

# 参考

[1]照片由[JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/occulus?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)(2018)拍摄

[2] NLTK 项目，[自然语言工具包](https://www.nltk.org/)，(2020)

[3] Glassdoor，Inc .，[NLP 工程师工资 T25，(2008-2020 年)](https://www.glassdoor.com/Salaries/nlp-engineer-salary-SRCH_KO0,12.htm)

[4] Glassdoor，Inc .，[计算机视觉工程师工资](https://www.glassdoor.com/Salaries/computer-vision-engineer-salary-SRCH_KO0,24.htm)，(2008–2020)

【5】安妮·斯普拉特在[Unsplash](https://unsplash.com/s/photos/document?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)(2020)上拍摄的照片