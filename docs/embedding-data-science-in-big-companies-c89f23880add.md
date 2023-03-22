# 在大公司中嵌入数据科学

> 原文：<https://towardsdatascience.com/embedding-data-science-in-big-companies-c89f23880add?source=collection_archive---------64----------------------->

## 在初始阶段应该关注什么，避免什么。

![](img/c6641656ac5e0848439fd10aeabc274d.png)

肖恩·波洛克通过 [Unsplash](https://unsplash.com/photos/PhYq704ffdA)

# 介绍

随着大型*非科技*组织开始投资开发机器学习和数据分析能力，未能达到管理层的期望和数据科学家的沮丧正变得司空见惯。

数据科学家和数据工程师是科技行业薪酬最高的专业人士之一。他们通常在数学、统计学和计算机科学方面有很强的背景。他们非常积极:大多数人是通过自学进入该领域的，因为“数据科学”领域没有多少大学学位，他们投入大量时间来跟上该领域的最新发展。

然而，对于大公司来说，将这些功能集成到旧的遗留系统中正在成为一个巨大的挑战。对高质量数据的有限访问、数据科学家和业务利益相关者之间缺乏理解以及技术差距是造成这一挑战的主要原因。

我已经在供应链行业做了几年的数据科学家。在做了多年的顾问后，我加入了一家国际零售公司的全新团队，开始在供应链的不同领域应用机器学习和数据分析，最终目标是降低成本和改善服务。

在这篇文章中，我总结了这些年来我学到的一些经验。这些经验并不是特定于业务的，尽管它们更适用于不存在数据文化或处于早期阶段的大组织，并且像机器学习这样的概念对许多人来说仍然是陌生的。

# 1.提高团队的意识

你的商业利益相关者需要了解你做什么，以及你如何在他们的日常斗争中帮助他们。他们不需要知道什么是逻辑回归或随机森林，但是他们需要理解底层的概念和限制，例如，部署一个模型来自动化某个任务。

这是开始时非常重要的一步。与您的利益相关者召开研讨会，确保您的数据科学家了解业务问题，并且您的利益相关者了解您所能提供的潜力和限制。

如果你是这家公司的新人，利用创业阶段来确定可以帮助你建立信誉的速赢，并建立一个盟友网络，这些盟友将支持你的工作。如果你在你的团队中缺少某些能力，确保与那些能帮助你的人联系。在 It 部门之外创建数据科学团队以使他们更接近业务是非常常见的。与 IT 团队联系并获得他们的支持，没有他们你不会走得太远。

# 2.(有时)少即是多

发现规划过程中的一个缺陷可以节省数百万美元。你不需要部署神经网络来开始带来价值。纯数据分析在发现非最佳流程、了解客户行为、检测欺诈或改善激励方面已经非常强大。

提出*可行的见解*可能会让你的团队免于经历一个部署过程，而他们在开始时可能没有准备好，同时为公司增加巨大的价值。

历史操作和计划数据是很好的起点。深入其中，你一定会找到改善运营的方法，让计划更接近现实。

# 3.自动化作为起点

一般来说，机器学习可以应用于(I)自动化现有任务或(ii)执行新任务。一开始，关注自动化有几个好处。业务流程已经存在并且广为人知，这限制了不确定性和风险的空间。此外，可以更准确地估计收益:节省时间、提高质量等。

在这些项目中，挑战通常在于你被要求交付的准确性。如果你正在自动化一个已经存在的过程，人们可能期望 100%的准确性。以下是一些原因:如果你正在自动化的过程没有被监控，没有基线来比较你的结果，你可能会被要求交付一个完美的过程，因为到目前为止，它最有可能被视为一个完美的手工过程。让您的模型标记不确定的情况以便手动修改，尽管这是一个明智的想法，但可能会伤害对模型的信任，并质疑自动化的好处。为了克服这个挑战并且不危及你的信誉，在你的估计中要保守，但是要清楚自动化的好处。

总是在谈论自动化的时候，小心你如何呈现项目。有些人可能会担心你试图用“机器人”来取代他们，并且不愿意合作。

总的来说，试着从已经测量了当前性能的自动化任务开始，这样你就有了一个清晰的基线。从与将自动化视为机遇而非威胁的团队合作开始。

# 4.不要滥用仪表板

仪表盘很棒。它们可以提供非常丰富的信息，有助于监控业务运营或支持决策制定。此外，它们易于开发和共享。

然而，经常发生的是，数据科学团队是大公司中少数拥有广泛和自由访问数据的特权的团队之一。这很容易导致团队被视为公司数据的入口点。人们希望以一种易于理解的方式消费数据，很快团队就被开发和共享仪表板的请求淹没了，或者仅仅是进行数据提取。

虽然仪表板通常受到企业的青睐，但过于关注简单的报告可能会耗尽数据科学家的动力，因为他们通常会面临不同的挑战。除此之外，组织中肯定有人有足够的技能来开发可视化解决方案，只是他们没有访问数据的权限。尝试保持平衡，明智地使用仪表盘来报告你的结果，或分享相关的见解，但避免被视为公司数据仓库的友好连接器。

# 5.创建数据文化

努力使数据可用，并围绕数据创造一种文化。为数据质量、元数据和文档而战。一个数据有记录、可追踪、可**访问的组织能够更加敏捷地发现和诊断问题，找到解决方案，并在数字世界中茁壮成长。此外，数据科学项目的启动成本也将大幅降低。**

推进开放和记录数据仓库的计划，并与数据所有者建立联盟，以便他们能够支持您的项目。让管理层相信数据可用性在支持决策方面的价值**。首席执行官的承诺对于创建数据文化至关重要。如果董事会和首席执行官接受了你处于有利地位的观点，如果他们还没有接受，试着把你的信息一直传递下去。**

促进大众对数据的需求，而不是自上而下的强加，这将有助于数据的民主化和建立热情。最后，帮助培养和提高有效处理数据所需的技能。对这一领域人才的搜索是不懈的，但幸运的是，你不需要一大群数据科学家来建立一个数据驱动的公司。使用那些你已经拥有的来提升你当前的劳动力。

我希望上述原则能够帮助您将数据科学有效地引入您的组织。

[1] Alejandro Díaz、Kayvaun Rowshankish 和 Tamim Saleh，[为什么数据文化很重要？](https://www.mckinsey.com/~/media/McKinsey/Business%20Functions/McKinsey%20Analytics/Our%20Insights/Why%20data%20culture%20matters/Why-data-culture-matters.ashx) (2018)麦肯锡季刊