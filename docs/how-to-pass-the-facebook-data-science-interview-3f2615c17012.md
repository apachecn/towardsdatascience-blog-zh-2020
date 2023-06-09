# 如何通过脸书数据科学面试

> 原文：<https://towardsdatascience.com/how-to-pass-the-facebook-data-science-interview-3f2615c17012?source=collection_archive---------5----------------------->

![](img/498379b48e53bebf291a287204fd04a5.png)

## 赢得面试的 4 个技巧

本周早些时候，我完成了作为脸书数据科学家的第一年绩效总结周期(PSC)。我们利用 PSCs 来收集关于我们的影响力、技能和发展领域的反馈，我再次发现，最重要的技能与面试过程中测试的技能相同——正如您可能希望的那样！

这些技巧也不是脸书面试所独有的。我所有的数据科学面试都集中在同一套简短的技能上，以评估我推动影响的能力。

因此，我认为与其他正在寻找数据科学工作的人分享这些技能会很有用。

当然，我不能分享我在脸书面试时收到的确切问题，反正它们现在已经改变了。但是技巧本身并不保密，短短一年肯定也没变。

所以没有特别的顺序，他们在这里。

# 1.流畅的 SQL

如果你一直在工作中编写 SQL，你会发现基础知识涵盖了你在实践中要处理的 90%的问题。

最重要的概念是各种类型的`JOIN`语句是如何工作的。例如，您肯定需要理解这样一个事实，即`INNER JOIN`将删除没有出现在两个表中的记录，而`LEFT JOIN`将保留出现在左表中的所有记录。

*中情局分析师吉姆·哈尔珀特解释 SQL 连接*

您还需要习惯使用`WHERE`子句过滤数据，使用`sum`之类的函数使用`GROUP BY`子句聚合数据。

因此，这实际上是实现 90%的方法所需要的全部:主 SQL 连接、过滤器和聚集。

但是剩下的 10%让我在面试中更容易通过 SQL 测试。

> SQL 基础知识将帮助您完成 90%的工作，但最后 10%是您需要通过的

这 10%包括理解较少使用的技术，比如像这样的子查询。

在我的 SQL 编码测试中，我使用了几个更“高级”的概念，包括窗口函数、命名子查询、self `JOIN`和 join 的`ON`子句中的条件。

*使用更高级的 SQL 特性可能会使您更容易解决 SQL 问题。*

# 2.概率论

我从未经历过评估我的直觉概率的面试，但我的现场展示了一个相当深入的案例研究。

幸运的是，我没有被要求写下任何公式，因为大学毕业后我已经把它们都忘了。

但我确实需要对我所学的关键概念有很强的理解:像中心极限定理、事件的独立性，以及选择合理的概率空间来建模问题的能力。

> 练习解释概率的关键概念，比如中心极限定理，不要使用任何技术词汇

我还被要求评估概率模型的输出，并根据这些输出提供业务建议。

数据科学家 Pam Halpert 评估了她同事的机器学习模型

最终，我能够给出一个明智的建议，因为我对这些概念建立了一种实用的直觉，即使我不记得量化模型拟合度的确切公式。

你不用任何技术词汇解释技术概念的能力是通过面试技术部分的关键技能。

# 3.沟通

在我看来，沟通技能比 SQL 或概率论等技术技能更重要。

![](img/59c6d088eacbc49c17eca3849948edc0.png)

用幻灯片演示死亡

就像技术技能一样，沟通不是你在使用手机屏幕前一周就能提升的。

但是你可以在面试前做一些简单的事情，这些事情将会对获得工作机会产生巨大的影响。

1.  **练习讲述你的“故事”:**你工作经历背后的历史，你申请这家公司的原因，以及你最引以为豪的项目。每个面试官都会要求你讲述你的故事来介绍你自己，所以有一个清晰易懂的故事会给你留下深刻的第一印象。
2.  **写下你从沟通中学到的经验:**对我来说，那就是讨论一种叫做“直接沟通”的表达方式，这是我在当时的工作中学到的。它只是意味着“从结论开始”，并且它通常比以您的方法或模型参数开始更有效。
3.  **了解你在沟通中看重什么:**你最认同哪种风格？你认为什么最有效？有个例子可以说说。对我来说，这是有逻辑的组织和术语自由。

对一般的面试问题有一个排练好的答案会对你的面试结果产生最大的影响。

# 4.分析判断

大多数公司向数据科学家候选人提出的标准面试问题之一是:“你将如何衡量 ***X*** ”？

脸书以间接的方式问了这个问题，但回答这个问题仍然需要同样的两个技巧:

1.  **能够解释你如何权衡不同方法**之间的*权衡*。所有的决策都有权衡，选择一个度量标准也不例外。在选择 KPI 或成功指标时，明确列出权衡，同时用可靠的判断进行权衡尤为关键。
2.  **理解测量*对业务*的价值，而不仅仅是它可能有多“准确”**。有些模型相当不准确，但非常有价值(例如，预测用户是否会关注他们新闻订阅中的帖子)。了解您的工作如何影响业务是您分析判断的最重要部分。

> 想想你将如何评估你的商业模型的价值，而不仅仅是它与数据的吻合程度

正是由于这四项技能，我才得以在一年多前获得了脸书的工作机会。它们当然不容易开发:我在各种分析工作中工作了近四年，才提高到让我得到这份工作的水平。

但我不认为发展这些技能需要我有任何特殊的天赋或才华。我确信任何花时间提高这四项技能的人都能在数据科学领域找到工作。

感谢阅读！如果您觉得这很有帮助，我写的是关于数据科学和 Medium 编程的文章，所以请关注我，获取更多类似本文的文章。

[](/how-find-a-job-at-a-tech-start-up-bde5ae7f1b9c) [## 如何在科技初创公司找到一份数据科学的工作

### 帮助你获得更多面试机会的三步系统

towardsdatascience.com](/how-find-a-job-at-a-tech-start-up-bde5ae7f1b9c)