# 营销分析的 3 个最重要的技能

> 原文：<https://towardsdatascience.com/the-3-most-critical-skills-for-marketing-analytics-e68e254908de?source=collection_archive---------27----------------------->

## 数字营销是所有业务中数据最丰富的领域，也是陷阱最多的领域。

也许比任何其他领域，营销，尤其是数字营销，几乎完全围绕着数据。这使得作为分析师或数据科学家，这是一项丰富且值得支持的业务，因为数据的数量和效用可能非常高，增加了分析专业人员的需求和潜在项目的范围。

然而，营销数据有一些重要的陷阱，会使营销分析程序脱轨:

*   从广告平台、社交和点击流数据到 CRM 和 CDP 数据，营销数据分散在众多来源中。
*   如果没有分析团队和营销团队都理解的有凝聚力的标记和跟踪策略，整合点击流和营销数据是一项挑战。整合销售和营销数据，尤其是在 B2B 中，很少能正确完成。
*   营销团队有十几种不同的方法来衡量营销绩效，这意味着创建仪表板和分析是一项挑战。

在这篇文章中，我将解释 3 个关键技能，它们将帮助你克服这些陷阱。

## 1.使用 API

SQL 和数据操作技能不足以有效地获得衡量营销计划所需的所有数据——除非您想每天手动下载 excel 电子表格。您需要学习如何使用 REST APIs 编码，以自动获取广告平台/点击流/和其他营销数据。

你可能听过的最大的谎言是，你需要成为一名开发人员来使用 API。事实是:你不知道。这里有一些提示和技巧，可以帮助你达到 80%的目标:

*   阅读我关于如何使用 Python 请求从 API 中提取数据的文章[](/how-to-pull-data-from-an-api-using-python-requests-edcc8d6441b1)**。*本文回顾了如何使用 Python 请求包从 Microsoft Graph API 中提取电子邮件数据。那篇文章中的方法将扩展到使用广告平台 API，如脸书图形 API 或 Linkedin 广告 API。*
*   *了解 PYODBC 包。PYODBC 允许您使用 Python 编写 SQL 语句和处理数据库。我使用 PYODBC 将从各种 API 提取的数据插入到数据库中。*
*   *使用邮递员。Postman 是一个使用 API 的 GUI 应用程序。Postman 允许您在 GUI 中输入值，并以拖放/点击的方式与 API 交互。一旦在 Postman 中成功提取了数据，就可以在 Python 中导出 API 调用，然后将代码片段放入脚本中。*
*   *如果你不想处理任何编码，并且有多余的预算，我推荐你使用 Stitch 或者 Xplenty。这些 ETL 平台内置了与大多数主要 API 的集成，允许您无需任何代码就可以将数据移入数据库。这些平台的缺点是成本——但是如果你有预算，我强烈推荐这些平台作为维护 ETL 管道的替代方案。*

## *2.了解网络分析、点击流数据和标签*

*你的网站很可能是你营销活动中发送流量和点击量的主要地方。随后，要讲述一个完整的营销故事，你需要了解网络分析、点击流数据，以及这些数据如何与你正在制作的广告联系起来。*

*下面是一些原始点击流数据的简单示例:*

*![](img/754085a63e891fbea869a3f8761e19e3.png)*

*您可以看到有一个时间戳、一个唯一标识符、URL 和一个 SDID 列，其中包含来自 URL 跟踪参数的唯一活动标识符(跟踪参数是“？”后面的值)在 URL 中)。*

*当在广告平台(脸书、Linkedin、Twitter 等)上创建活动时。)—来自这些活动或广告的信息需要与定向流量的 URL 联系起来。这通常发生在 URL 跟踪参数上，但是你会惊讶有多少营销团队要么 a)没有标记任何东西，要么 b)不一致或不正确地标记广告。标签和分析之间的任何差异都将意味着你试图收集的数据存在巨大差距，这将使有效衡量营销活动变得极具挑战性或不可能。*

*由于这一过程的复杂性，我总是建议分析师/数据科学家/任何将负责营销计划衡量的人，参与或创建自己的跟踪和标记策略。通常，营销团队或代理会创建标记策略，但由于对数据收集和清理流程的误解，这往往会遗漏有价值的数据(例如，在多个广告上使用相同的唯一标识符将导致无法判断哪个广告对流量/转化/等负责)。).当分析师自己拥有这一过程时，最终获得干净的数据将会容易得多。*

*![](img/ceeadde45533bb877083b4965a7f35e2.png)*

*作者图片*

*上述过程很少发生，即使是在最大的高科技公司的营销团队中。通常，营销人员会使用 Adobe Analytics 或 Google Analytics 仪表盘，或者默认使用特定平台的分析。这有时会奏效——尤其是如果你主要是一家电子商务公司。当您希望将所有数据捆绑在一起时，问题就出现了——目前这只能由理解我上面讨论的动态的分析专家来完成。B2B 业务尤其容易受到这个问题的影响，因为许多 B2B 销售是在会议室而不是网上进行的。因此，要真正衡量营销对销售的影响，你必须以某种方式将营销数据与 CRM 数据联系起来——如果没有合适的分析人才，这是非常具有挑战性的——也就是说，有人已经学会了这些关键技能。*

## *3.丰富的商业和营销领域知识*

*一旦编译和集成了干净的数据，就可以让营销和销售团队消化这些数据了。这可能是所有技能中最困难和最微妙的，因为它要求你跳出技术分析和数据工作，花时间与业务和营销从业者在一起。在创建能够有效传达营销绩效的仪表板或报告之前，您需要明确一些事情:*

*   *营销团队实际关心的是什么？永远不要假设你的营销团队的优先事项是什么。你需要非常清楚和你一起工作的营销人员的成功标准是什么。如果他们不知道，那么你就必须创造他们，这意味着充分了解营销计划和业务，以说服 KPI 团队有意义。*
*   *他们认为什么是成功？即使您的营销团队已经向您提供了他们想要查看的成功指标，他们也总是希望将其与某些指标进行比较，无论是行业标准的绩效指标还是时间驱动的指标(例如，去年这个时候、去年至今，等等)。)永远不要创建不允许与标准或时间序列进行比较的仪表板。*
*   *失败可以吗？这很不幸，但是我合作过的几个营销团队只关心那些让他们的项目看起来不错的数据。您需要从一开始就知道这一点——团队的目的是测量和改进还是仅仅呈现信息？许多团队只是想向利益相关者展示他们花了预算，带来了大量流量——他们并不真正关心如何制作更好的广告。根据你所合作的营销团队的类型，你将制作两个完全不同的仪表板/报告。*

## *营销人员最好的朋友*

*我上面概述的三个技能对于做好营销分析是绝对重要的。没有它们，你将无法有效地衡量和报告公司的营销计划。有了它们，你将成为一笔不可多得的财富，迅速成为营销人员最好的朋友。*

*有问题或意见吗？你可以给我发电子邮件，地址是 cwarren@stitcher.tech，或者在 Linkedin 上关注我，地址是[https://www.linkedin.com/in/cameronwarren/](https://www.linkedin.com/in/cameronwarren/)*

*我还提供营销分析服务。如果您想了解更多信息，请直接发邮件至 cwarren@stitcher.tech 或前往 http://stitcher.tech/contact/。*

*如果你想要帮助连接你的点击流和客户关系管理数据，看看 https://stokedata.com/的。*