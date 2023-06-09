# 面向娱乐和非营利组织的数据堆栈—第一部分

> 原文：<https://towardsdatascience.com/data-warehouse-side-projects-part-1-f7bd74323bd7?source=collection_archive---------44----------------------->

## 为您的副业项目选择数据仓库

![](img/f289c93b1540d84c98c643f9f0c6cf08.png)

萨拉·库菲在 [Unsplash](https://unsplash.com/collections/9698149/data-warehouse?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

驱动几乎所有数据科学团队的引擎是某种形式的数据仓库，它充当组织中各种不同数据源的中央收集点和存储库。这些来源可能包括组织的主要事务性数据库、日志、电子邮件、SaaS API、CRM、ERP 以及各种形式的随机平面文件。数据仓库的目的是将所有这些数据收集到一个真实的数据源中，并通过一个访问点方便用户访问。此工作流中的终端可能是手动 SQL 查询、某个 BI 平台或数据科学家的自动化模型培训工作流。

![](img/ee3e84c45752bd586b7569caf7b5ec7d.png)

图片来自 [dbt，](https://www.getdbt.com)这是一个令人惊叹的开源数据仓库管理框架。

当数据仓库得到组织的财政支持时，它们是一种有用的资源，但是个人数据从业者如何为了个人项目的目的或作为培训资源来模仿这种经验呢？一个人如何用个人预算创建自己的个人数据仓库？这是一个我长期以来一直在寻找满意解决方案的问题，因此这是我将探索现代分析平台产品生态系统中一些可用选项的系列博客帖子中的第一篇。这第一部分将主要集中在想象标准和一些可能的解决方案堆栈可能看起来像什么，然后稍后我将调查和评估不同的选项。

显而易见的初步答案是建立一个本地 PostgreSQL 数据库，并编写一些 Python/R/SQL 代码等。，但这并不完全模拟我们所追求的确切体验。它对学习一些 SQL 和手工 ETL 工作流的痛苦很有用，但它缺乏远程数据存储、灵活的可伸缩性、配置 CI/CD 工作流以及利用互联网可访问的数据存储作为各种 BI 解决方案的中心的能力。在我教的[数据科学课程](https://ep.jhu.edu/programs-and-courses/685.648-data-science)中，学生们经常表示有兴趣将访问大规模数据仓库平台作为课程的一部分，这显然是非常昂贵的，但我可以理解学生们为什么觉得创建玩具 SQLite 数据库并不能满足他们的需求。

理想的个人数据仓库应该是什么样的？嗯，理想情况下，它应该是便宜的，因为我们大多数人可能都希望避免支付与常见的 SaaS 平台相关的高额月费。在可能的情况下，无服务器将比连续服务器更受欢迎。大多数情况下，我们希望数据处于静态(产生最小的费用)，只有在加载和转换操作需要时才会产生计算费用。我们可能还希望尽可能地减少配置和管理负担，因为我们不太可能从系统管理员那里获得支持。任何开源组件可能也是可取的。

因此，在我们探索哪些选项符合这些标准之前，让我们首先简要回顾一下我们寻求利用(廉价)或替换的平台的当前生态系统。为了存储我们的数据，我们有几个仓库平台可供选择，包括亚马逊[红移](https://aws.amazon.com/redshift/)，谷歌[大查询](https://cloud.google.com/bigquery)，以及[雪花](https://www.snowflake.com/)。

ETL (Extract/Transform/Load)传统上是开发和维护数据仓库中最费力的工作之一，通常涉及 SQL、Python 等重要的软件工程。今天，我们有许多可用的商业平台，它们抽象出了 ETL 系统中固有的大量重复逻辑。其中包括[五针](https://fivetran.com/)、[针](https://www.stitchdata.com/)和[针](https://www.matillion.com/)。

在数据可视化方面，我们有 BI 平台，包括 Tableau、Looker、PowerBI 等等。其中一些有免费/公共版本，但是我们也有足够的能力通过 Shiny、Jupyter 和更多我不想列举的技术来制作我们自己的仪表板。出于本系列的目的，我们将主要关注栈的数据存储和 ETL 部分。

我确信我想要包括的一个组件是令人惊奇的开源的 dbt。

> dbt 是一个开发环境，它使用任何地方的数据分析师的首选语言— SQL。借助 dbt，分析师可以掌控整个分析工程工作流程，从编写数据转换代码到部署和文档。
> 
> 使用 dbt，您可以按照最古老的软件工程最佳实践之一来编写数据转换代码:*模块化*。编写模块化 SQL 意味着您的查询更容易更新和故障排除，并且执行速度会大大加快。

简而言之，dbt 是一个强大而方便的框架，用于组织仓库中的所有转换和数据模型。像 Fivetran 和 Stitch 这样的 ETL 平台非常适合将数据加载到您的仓库中，但是生成的数据可能不会按照您希望的方式进行组织，并且您可能还希望集成其中的一些数据源。这就是 dbt 的用武之地。该工具本身是免费的，他们的云部署平台也有一个适合个人项目的免费层，还有一个活跃在 Slack 和 Discourse 上的优秀用户社区。

![](img/09dcd86d3ce004eee52b5b48b46b0d46.png)

**(左)**图片由[雪花](https://www.snowflake.com/) | **(中)**图片由[谷歌— BigQuery](https://cloud.google.com/bigquery) | **(右)**图片由[亚马逊网络服务—雅典娜](https://aws.amazon.com/athena/)

数据存储呢？根据我们的搜索标准，基于传统服务器的平台(如 Redshift)不在选择之列。虽然我很喜欢雪花，但它没有任何适合我们需求的(永久)免费层。这是一个现收现付的平台，所以有可能将[成本降到最低](https://precocityllc.com/blog/snowflake-on-a-shoestring-budget/)，但我不太确定成本会维持在多低的水平。事实上，似乎有一个 25 美元的每月最低限额是不可行的，但我不一定完全排除雪花。

AWS Athena 是一个有趣的选择。它是 Presto 的无服务器部署，位于您自己的 S3 对象之上。您只需为运行查询和低得可以忽略不计的 S3 存储成本付费。Athena 有 event [dbt 支持，但目前还处于早期开发阶段。雅典娜看起来肯定是个不错的选择。](https://github.com/Dandandan/dbt-athena/)

另一个我之前没有考虑过的选项是 Google 的 BigQuery。我总是把 BigQuery 归为 GCP 的红移或雪花，但事实证明，谷歌实际上提供了一个完整的免费 BigQuery 层，只要你在一定的限制内操作。只要您保持 10GB 的加载存储和 1TB 的查询处理，您就可以完全免费使用 BigQuery！

ETL 平台呢？像 Fivetran 和 Stitch 这样的服务对个人来说可能太贵了。Fivetran 最近确实切换到了[基于消耗的定价系统](https://fivetran.com/docs/getting-started/consumption-based-pricing)，因此它的利用率可能会被限制在一个低廉的水平。然而，这些付费平台的大部分价值与忠实地将复杂的内部数据库镜像到仓库的挑战更直接相关，而不是摄取格式或多或少相同的平面文件。因此，我认为我们可以将从 API、电子邮件和类似来源提取的数据抽象到其他未来项目中。这些未来提取服务的基本端点是将平面文件存放到对象存储中(S3 或其他)。

有了基于 Athena 的仓库，人们只需开发工作流，将数据提取到 S3 进行暂存。AWS 还提供 Glue 和其他一些编排服务，这些服务可能会保持在成本之下。BigQuery 有类似的兄弟服务，包括[数据流](https://cloud.google.com/dataflow)和[数据存储](https://cloud.google.com/datastore)，以及直接从 Google Storage 和 Google Drive 加载数据的能力。还可以选择从 S3 将数据[加载到 BigQuery 中。我说过 BI 选择超出了这个搜索的范围，但是同样值得一提的是 BigQuery 直接集成到了](https://cloud.google.com/bigquery-transfer/docs/s3-transfer) [DataStudio](https://datastudio.google.com/u/0/) 中。

至此，我认为我们已经有了三个合理的候选筹码:

1.  BigQuery 数据仓库，使用来自 Google Drive 和 S3 数据传输的数据，用于数据建模的 dbt，以及一些带有 DataStudio 的仪表板。
2.  Athena 数据仓库，使用 S3 分阶段数据，dbt + dbt-athena 插件进行数据建模。
3.  雪花数据仓库，使用外部存储集成和 SnowPipe 进行接收，使用 dbt 进行数据建模，使用 Snowsight 进行仪表板。

我将通过在每个平台上配置帐户并使用 dbt 建立一些简单的数据模型，开始尝试这些选项。在第二部分中，我将分享我对最终架构的想法，该架构似乎最适合低成本的个人项目，并开始深入研究特定于所选平台的仓库设计和工作流编排。

你怎么想呢?你最喜欢的云仓库栈会是什么样子？欢迎在评论中留下你的想法！