# 仪表板没有死

> 原文：<https://towardsdatascience.com/why-dashboards-are-not-dead-cdc996e99ac6?source=collection_archive---------31----------------------->

## 有很多很棒的新工具。为什么仪表板还挂着？

![](img/ff56c2e98cecd95eb51bca04b2c37c03.png)

原始数据。去那里找点理智吧！(照片由克林特·王茂林在 [Unsplash](https://unsplash.com/s/photos/connection?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄)

我刚刚在 Medium 上读到一篇关于仪表板之死的好文章。它认为专门版本的 Jupyter 笔记本比传统的商业智能仪表盘要好得多。我必须承认，我立刻爱上了这个想法！

如果你不知道这些笔记本是什么:它们基本上是一种用嵌入的代码块编写格式化文档(想想:MS Word)的方法，这些代码块可以直接在页面上执行，并在页面上显示结果。这使您可以漂亮地记录和解释整个过程，还可以直接对代码进行更改和试验，直接在页面上看到更改后的结果。这种方法在机器学习应用程序中变得非常流行，在这些应用程序中，实验确实是获得好结果的最重要的步骤之一。

如果我认为自己是一个仪表板用户，我肯定会喜欢这种方法，原因正如文章中所述:笔记本让你清楚地看到过程，并有机会玩它。

当然，我现在可能是一名管理用户，但我有 IT 和设计背景，我喜欢数学。为了让笔记本电脑方法为你的非工厂标准 CEO 工作，我认为首先需要解决一些挑战。

# 实际的数据源

这个总是房间里最大的。即使在这些当前的笔记本电脑出现之前，自助报告也不是什么新鲜事。it 的主要挑战过去是，现在仍然是让最终用户可以使用正确的数据源。典型的事件链是:首先，将报告工具直接附加到日常工具的生产实例中。这为用户提供了最新状态的所有数据。显而易见的缺点是，其中一个用户会通过创建非常苛刻的(或简单错误的)数据请求而使您的生产系统瘫痪。然后，将您的报告工具附加到生产系统的每日拷贝中。不错的选择。用户试图愉快地挖掘，但有些人实际上需要接近实时的数据，并对每天的转储感到不满。这可能没问题，我们不必让每个人都开心。然而，更重要的是，许多用户会发现他们不理解源系统中的数据结构。您的后端系统的关系数据库在设计时并没有考虑到报告！用户可能需要构建复杂的连接来理解数据，在许多情况下，这可能并不明显。他们可能认为他们正在按地区汇总一个月的所有汽车销售，而实际上是在汇总销售和取消的优惠。最重要的是，我们也突然开始碰到讨厌的数据保护法，并需要确保个人数据不会被大多数报告用户接触到。因此，你开始用漂亮的 OLAP 立方体构建老式的数据仓库结构，或者开始创建业务视图，使用户更容易选择正确的数据。由于对原始数据进行操作时，性能也可能会有问题，所以您也开始对其进行一些整合。

这是一项繁重的工作，但它确实允许管理用户执行自助报告。在某种程度上，他们面临着与使用准备好的仪表板时相同的困境。他们需要信任准备好的数据源。

# 访问权限

当谈到数据源时，我想到的是至少知道自己在做什么以及为什么做的用户。我的经验告诉我，这些不是唯一的用户类型。

![](img/2edb6a3976d747387d6def5c5d0f5093.png)

我真的要看手册才能了解这个吗？—[与 Raj](https://unsplash.com/@roadtripwithraj?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/decision?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 的公路旅行照片

进入通常使用仪表板的职位的人可能有一些很好的资格，但数据科学通常不是其中之一。通常他们喜欢玩所有的开关，并会很快对结果形成强烈的意见。因此，通过提供所有工具的笔记本风格的方法，准备好快速找到数据科学家们调整得面目全非的工作。因此，即使您打开了处理数据的可能性，您仍然希望保持一个基本的工作流程，即有人请求一个关键绩效指标(KPI ),有人创建一个不会被实验覆盖的有效且安全的版本。

# 仪表板的用例

虽然许多经典的仪表板可能只是因为有人说 KPI 对于执行管理评审很重要而创建的，但是一些仪表板实际上有定义的用例。它们要么显示一些由多名经理监控和讨论的商定 KPI，因此只要小组没有就新定义达成一致，就应该始终保持不变。或者用于监控外部合同中的服务级别协议(SLA)。这些类型的仪表板应该非常简洁、清晰和简单地显示所需的信息。其中一些甚至可以提供给外部供应商，所以这里没有游乐场。

# 斗争是真实的

虽然所有这些都与笔记本背道而驰，但到目前为止，我仍然是这个想法的忠实粉丝。

仪表板需要做好。最重要的是，一定数量的文档必须对每个用户可用。如今，利益相关者有时交换得如此之快，以至于数据人员可能永远也不会了解每一个路人。前一天你和一位首席财务官一起定义了一个 KPI，第二天另一位首席财务官就来曲解它。在我们公司制作的仪表板上，通常每个 KPI 都有一个折线图，在每个图表的一角总是有一个小问号。如果您单击它，就会看到文档。根据您的访问权限，您甚至可以直接编辑它或发出变更请求。这已经一次又一次地被证明是有价值的。

仪表板也需要是活的。如果你的目标是了解公司的内部运作，然后迭代地做得更好，你需要不断地调整你的仪表板来反映变化。此外，每次查看您的仪表板都会让您对新的 KPI 有新的想法。因此，你需要它建立在一个灵活的平台上，你需要可用的人力来实施变革。好的仪表板需要数据探索和迭代方法。在某种程度上，注定是一个笔记本。

总之:我相信仪表板在商业环境中有它的位置，并且会一直存在下去。同时，如果它们的基础是笔记本式的技术，我会很高兴。数据科学家将使用笔记本来构建流程。然后，他会将一些结果分配给仪表板视图中的插槽。然后将这种观点与人分享。根据他们的访问权限，他们的仪表板上可能有一个详细信息按钮，将他们带到笔记本。这可以是只读访问，也可以允许编辑或衍生工作。

如果这就是未来，我爱它！谁在研究它？我想跟着去！