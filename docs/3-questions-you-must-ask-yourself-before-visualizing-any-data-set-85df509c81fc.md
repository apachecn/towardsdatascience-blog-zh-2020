# 通过问自己以下三个问题，轻松完成任何数据可视化项目

> 原文：<https://towardsdatascience.com/3-questions-you-must-ask-yourself-before-visualizing-any-data-set-85df509c81fc?source=collection_archive---------46----------------------->

![](img/2d62249cd211e26be7160f06c594d171.png)

Metis 设计师在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的[照片](https://unsplash.com/@metisdesigner?utm_source=medium&utm_medium=referral)

作为一名数据分析师，我的大部分时间都用来为不同的利益相关者可视化数据集。数据可视化可以采取多种形式。它们可以是简单的 Google Sheets 图表、Python 笔记本上的一些可视化内容，或者是复杂的 Tableau 仪表板。在可视化任何数据集之前，我总是会问自己以下三个问题。

# 你的目标受众是谁？

这无疑是问自己最重要的问题。涉众是技术还是非技术受众？他们对您要可视化的数据的熟悉程度如何？他们是你的同事还是管理层的经理？您是否为不同的受众群体或特定团队可视化数据？在考虑可视化数据之前，充分了解你的目标受众有助于你取得一半的成功。

我经常通过回答上面的所有问题来记录我的观众档案。我有不同的可视化方法来适应不同的观众类型。例如，如果我的读者是要求我做一些探索性分析的非技术人员，我会想到一些 Google Sheets 图表，而不是 Tableau 仪表板。这样，我也可以轻松地与他们共享数据集。他们可以根据需要调整图形或图表。例如，他们可能后来意识到，他们只对上个月的数据感兴趣，而不是最初询问的 6 个月的数据。

如果我知道我将要向一个庞大而多样化的群体展示一些视觉化的东西，我会更加注意在视觉化的东西中加入更多的解释。例如，“日活跃用户”或“留存率”可能一开始听起来微不足道。然而，这些指标在不同的业务或行业中可能有非常不同的定义。我会在我的图表下面添加一个简短的标题来解释我是如何计算这些指标的。

# 这种可视化的目的是什么？

在了解了我的听众之后，我通常会和他们展开一个简短的讨论，以了解他们的期望。简单地问“你的目标是什么？”可能行得通，但并不总是像看起来那么容易。然而，我仍然建议非常直截了当地询问他们的需求和期望。然后，我问一些试探性的问题，归结为我需要满足的最重要的需求。

例如，客户成功团队希望更多地了解客户投诉及其团队绩效。在最初的对话中，我会核实他们是否需要临时分析或深入的仪表板。在第一种情况下，一些 Excel 图表应该足以解决他们的燃眉之急。在第二种情况下，我需要构建一个显示各种指标的仪表板，以帮助他们全面了解历史数据、当前性能和未来趋势。

假设他们想要一个仪表板。然后，我们一起集思广益，列出他们希望看到的指标。在头脑风暴阶段，我与我的利益相关者分享，他们不应该担心可行性或优先级。让我们考虑尽可能多的指标。之后，我们根据优先级对指标进行排序。如果我们确切地知道什么应该放在优先列表的首位，这个任务就很容易。否则，我们会为每个指标分配相对分数，然后选择前三名或前五名。一旦确定了优先级，我们就开始讨论可行性。有些指标很容易构建，有些则不容易，主要是因为用于构建这些指标的相关数据还不可用。

我提到的过程可能需要一到两次 30 分钟的会议。排名指标的列表保存在一个共享的 Google Docs 文件中，该文件是可共享的，并允许其他人进行评论。对于如何理解他们的期望和需求有一个清晰的结构有助于您更容易地浏览数据可视化过程。

# 数据背后有什么故事？

如果这些数据没有引起你的注意，也许你需要花些时间更深入地思考。例如，您可能会对显示按类别细分的客户投诉数量的堆积条形图感到非常自豪。图表看起来很清晰，有所有必要的标题。调色板看起来很棒。然而，通过查看这个图表，您发现了哪些真知灼见？你可能会意识到一个类别可能会支配其他类别。在这种情况下，按降序对字段进行排序是最有帮助的操作。当查看您的图表时，观众可以很容易地在第一时间发现主导类别。

一些类型的数据可视化在开始时看起来是最好的选择，但是直到你思考数据背后的故事时才知道。当您处理时间序列数据时，很容易认为折线图是一个显而易见的答案。然而，你认为有时条形图是更好的候选吗？条形图不仅能帮助你看到趋势，还能帮助你更快地发现异常值，这要归功于这些条形图相对于其他条形图的突出优势。

让我们回到客户成功仪表板的例子。假设您正在可视化一段时间内客户服务票据的数量，x 轴是周期，y 轴是票据的数量。折线图强调你对整体趋势的关注。然而，条形图可能会将您的注意力转移到 8 月份门票数量出现峰值的几周。在做了一些研究后，你可能会发现根本原因是在那几周有新产品发布。由于顾客对新产品不熟悉，他们问了很多问题，这增加了门票的数量。因此，团队意识到他们应该添加更多关于新产品的说明，以减少该产品的标签数量。

# 结论

这三个问题是我在做任何数据可视化项目之前的自制清单。这帮助我非常有效地浏览流程，为每个人节省时间，并使我的工作流程更加结构化。我给你的建议是创建你的清单。如果您觉得有帮助，请随意添加更多步骤。我希望您在交付任何数据可视化时能够更加自信。

*原载于 2020 年 10 月 16 日*[*【http://baovinhnguyen.com】*](https://baovinhnguyen.com/2020/10/16/3-questions-you-must-ask-yourself-before-visualizing-any-data-set/)*。*