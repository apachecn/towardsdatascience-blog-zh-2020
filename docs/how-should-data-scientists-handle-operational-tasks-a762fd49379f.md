# 数据科学家应该如何处理运营任务？

> 原文：<https://towardsdatascience.com/how-should-data-scientists-handle-operational-tasks-a762fd49379f?source=collection_archive---------32----------------------->

![](img/1cc56973d135d9f5e4374f9cdfee58a2.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Franck V.](https://unsplash.com/@franckinjapan?utm_source=medium&utm_medium=referral) 拍摄的照片

## 处理短期和长期的权衡

# 介绍

作为数据科学家，我们看到许多文章解释人工智能，机器学习或强化学习的先进方法。然而，在现实生活中，我们经常不得不处理较小的操作任务，这些任务不一定处于科学的边缘，例如构建简单的 SQL 查询来生成电子邮件地址列表，以作为 CRM 活动的目标。理论上，这些任务会分配给更合适的人，比如业务分析师或数据分析师，但公司并不总是有专门负责这些任务的人，特别是如果是较小的公司。

在某些情况下，这些活动可能会消耗我们太多的时间，以至于我们没有太多的时间去做重要的事情，最终可能会在这两方面都做得不够好。也就是说，我们应该如何处理这些任务？一方面，不仅我们通常不喜欢做操作任务，而且他们也是一个昂贵的专业人员的糟糕使用。另一方面，必须有人去做，而且不是每个人都具备必要的 SQL 知识。在这篇文章中，我将向你展示一些处理这些问题的方法，以优化你的时间。

# 减少

第一个也是最明显的减少操作性任务的方法是简单地拒绝去做。我知道这听起来有点苛刻，根据你的公司和它的等级制度，这可能不切实际，但在某些情况下值得一试。通过“拒绝”，我的意思是质疑这项任务是否真的有必要，并试图找到最好的方法去完成它。比方说，每个月你必须为不同的领域准备三份不同的报告，包含相似的信息。您已经成功地实现了 SQL 查询的自动化，但是您仍然需要仔细检查结果，并最终根据用户的请求添加/删除一些信息，或者更改图表布局中的一些内容。在本例中，您可以查看 3 个不同的报告是否都是必要的，或者您是否可以调整它们，使它们成为一个报告，发送给 3 个不同的用户。不管怎样，想办法减少完成这些任务的必要时间，或者，理想的情况是，完全停止执行这些任务。

# 授权

有时，花时间让用户自己执行这些任务是值得的。当 CRM 要求你生成无止境的电子邮件地址列表时，也许教或鼓励他们学习 SQL 的基础知识(或雇佣一些已经知道的人)，这样他们可以更加自主，从长远来看会有回报。如果这听起来过于雄心勃勃，那么为他们提供工具，使他们不用编码，只使用拖放功能就能生成这些列表，这可能是您的解决方案。您可以使用现有的解决方案，如 Adobe Campaign，也可以自行开发(作为一名数据科学家，这可能是培养您的应用程序构建技能的绝佳学习机会)。

# 使自动化

如果你注意到这是一项你无法摆脱又无法委派的任务，那么就尽可能地让它自动化。对于报告，尝试将它们迁移到 dataviz 工具，如 Tableau 或 Google Data Studio。您可以将这些工具与您的数据库同步，它们将始终保持最新，因此您不必再更新报告。如果它与 CRM 电子邮件列表相关，请尽量使您的 SQL 查询灵活，使用可变的日期和名称，这样您就不必每次都修改它们。

此外，试着写下你对数据做了什么样的检查，并用编程逻辑将它们形式化。这使您甚至可以自动执行手动检查，因此您不必再做这些工作。老实说，这一步无论如何都是一个很好的实践，但是它肯定会帮助你完成操作任务。

# 组织

特别是当你是一名经理时，你必须分清主次，这样你和你的团队才不会淹没在无休止的运营任务中。为了做到这一点，在你的一周中留出一两天来做这类工作，在剩下的 3-4 天里不要去看它。要做到这一点，你必须按照前面的步骤来调整你的工作负荷，并且在设定截止日期时通过减少工作时间来管理期望。这也意味着向你的内部客户解释范式的转变，以便他们能够适应这些新的截止日期。这一步可能意味着做一些内部政治，与你的上级和其他部门协商。你必须证明你的团队的时间可以更好地用于高价值的任务，而不是操作性的任务。

另一个可能有所帮助的组织变革是聘用一名数据分析师或业务分析师，全职处理这些需求，以减轻高级分析师或数据科学家的负担。请记住，该解决方案还需要管理层的认可。

# 结论

一旦你绘制了所有的操作活动，你就要开始尽可能地从你的管道中删除，首先永久地删除不必要的活动，然后将它们委派给请求它们的团队。然后，无论剩下你要做什么，你都要最大限度地自动化(无论如何，自动化应该是任何重复性任务的优先事项)，并组织自己，以确保你有时间做你必须做的相关工作。这样，你不仅能从工作中获得更多乐趣，还能确保你昂贵的时间得到合理利用，最大化公司的利益。