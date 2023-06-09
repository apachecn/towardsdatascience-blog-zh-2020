# 将数据仓库迁移到云时需要考虑什么

> 原文：<https://towardsdatascience.com/why-you-are-throwing-money-away-if-your-cloud-data-warehouse-doesnt-separate-storage-and-compute-65d2dffd450f?source=collection_archive---------23----------------------->

## 要让您的数据仓库和数据湖面向未来，需要考虑什么&雪花、亚马逊、谷歌、SAP 和 IBM 是如何实现存储和计算分离的

![](img/b5b3bbd4dc7e0b56ca9efa3523198f5f.png)

约翰·施诺布里奇在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

不久以前，建立一个企业数据仓库需要几个月甚至几年的时间。如今，有了云计算，您可以很容易地注册一个由云供应商提供的 SaaS 或 PaaS 产品，并且很快就可以开始构建您的模式和表。在本文中，我将讨论将数据仓库迁移到云时要考虑的关键特性，以及为什么选择一个将存储和计算分开的数据仓库是明智的选择。

# 将存储和计算分开意味着什么？

## 从单个服务器到数据仓库集群

归结起来就是**向外扩展&向内扩展**与**向上扩展&向下扩展**之间的差异。在旧的数据库和数据仓库解决方案中，存储和计算驻留在单个(*通常很大&强大*)服务器实例中。这可能会很好地工作，直到这个服务器实例达到其最大计算或存储容量。在这种情况下，为了适应增加的工作负载，您可以**纵向扩展**，即将 CPU、RAM 或存储磁盘换成容量更大的，对于云服务，这意味着要切换到更大的实例。类似地，如果你的单个实例太大，为了省钱，你可以把它换成一个更小的，也就是**缩减**。这个过程有两个主要缺点:

*   向上扩展和向下扩展的过程非常耗时，并且通常意味着您的数据仓库将在一段时间内不可用
*   由于单个服务器实例的自然限制，您可以纵向扩展的范围是有限的。

## 大规模并行计算

为了缓解这个问题，数据仓库供应商开始使用 MPP ( *大规模并行计算*)范例，允许您的数据仓库一次使用整个实例集群。这样，如果您开始达到最大容量限制，您可以简单地**向集群**添加另一个具有更多存储和计算容量**的服务器实例**(即**横向扩展**)。

MPP 可以在很大程度上解决最初的可扩展性问题。然而，这也要求您的**存储和计算能力在集群中的节点之间紧密结合**。这意味着，如果你想在晚上关闭一些计算能力(即**扩展**，因为*几乎*没有人在这段时间查询数据，你不能这样做，因为终止实例将意味着要么丢失数据，要么必须创建备份并在早上从它恢复。**如果您的架构不允许您轻松扩展** **闲置的计算资源，您只需扔掉您的钱**。

这里讨论的范例通常被称为**无共享架构**。维基百科[1]是这样定义的:

> **无共享架构** ( **SN** )是一种[分布式计算](https://en.wikipedia.org/wiki/Distributed_computing)架构，其中每个更新**请求由单个节点**(处理器/内存/存储单元)满足。目的是**消除节点**之间的争用。

## 如何才能把 SN 架构的 MPP 做的更好？

我们可以清楚地看到，瓶颈在于存储和计算紧密耦合，无法相互独立地扩展。理想情况下，我们希望获得一种架构，在这种架构中，我们可以根据查询工作负载按需扩展计算能力，并且在所有计算节点之间共享存储。存储应该具有无限的容量，以使架构经得起未来的考验，并且随着时间的推移，随着我们存储越来越多的数据，存储应该自动扩展。

> 所以我们想实现 **SD-MPP** — **共享数据大规模并行处理**集群，而不是 SN-MPP。

这正是许多云供应商所做的。他们的实现有一些不同，但他们的目标是相同的:一个**弹性计算层**和一个独立且可无限扩展的**共享存储层**。

# 为什么存储和计算的分离非常适合分析查询？

Hadoop 最初设计用于分析数据(*，即运行查询以检索&流程数据*，尽可能接近其存储位置。这意味着，如果您的*销售*数据存储在节点 A 上，那么您检索销售数据的查询也可能在节点 A 上执行，以提高性能。总的来说，获取数据进行处理的最快方式是(*按此顺序*):

*   来自 RAM，
*   然后从固态硬盘
*   然后从硬盘和对象存储。

因此，将存储和计算分开可能看起来违反直觉，因为我们将数据(*存储*)移动到离处理数据的地方更远的地方。

然而，对于高性能列数据库，**云供应商将许多优化技术** **应用于存储和计算** ( *例如。AWS Redshift 应用 AQUA [4]* )，因此存储与计算的分离不会对性能产生任何负面影响。这些优化技术涉及压缩、编码、缓存以及在对象存储和 SSD 之间内部移动数据的组合。

当您在一个列式内存数据库中运行一个查询时，在**的掩护下，您只从一个共享存储层** ( *比如说从对象存储* ) **将该数据的一小部分加载到内存** ( *中，同时还对该数据应用字典编码和压缩以减小其大小*)。然后，可以用与从具有块存储的本地磁盘加载时相同的方式处理这些数据。

Spark 等分布式计算引擎也支持直接从对象存储加载数据[2]，这是分析数据处理的计算和存储分离的又一个例子。

# 在数据仓库中分离存储和计算有什么好处

*   **没有闲置的计算资源** —存储和计算可以相互独立地扩展和缩减
*   如果与*对象存储*一起使用(例如。AWS S3)或与*网络文件系统* (es。AWS EFS)，我们以低成本获得无限的**高可用性和容错存储**
*   **没有存储节点管理** ( *这是您通常需要用 ex 维护的。Hadoop 集群节点或 Amazon 红移密集型存储节点)—使用 SD-MPP* ，您(*通常是*)只需监控和扩展您的计算节点
*   **大幅降低成本—** 能够在夜间、季节性高峰过后或不需要时关闭一些计算节点，可以节省大量资金
*   **让您的架构在数据增长方面面向未来** —随着我们这些天经历的数据增长，我们的数据量不可避免地会随着时间的推移而增加。通过使用 **SN-MPP** ，仍然有可能**适应这种**增长，但价格是许多公司无法承受的。
*   **灵活性** —能够将**季节性**考虑到您的架构中。在一年中的特定时间需要更多计算，例如黑色星期五、圣诞节或您发布新产品的时间
*   **更高的性能**——你可以**在你的时间内做更多的事情**:例如。如果您有一些计算成本更高的作业，您可以启动一个具有更多 RAM 和 CPU 容量的额外计算节点，以更快地完成计算密集型作业，之后，您可以终止该节点，而不必重新设计整个数据仓库
*   **容错:**如果由于某种原因，您的所有计算节点都停止运行，您不会丢失数据——您可以简单地启动一个新的计算实例，并立即恢复对您的模式和表的访问
*   横向扩展时，**无需对集群中的数据进行重新分配、重新分区或重新索引** —借助紧密耦合的 SN-MPP 架构，需要重新分区或重新索引来防止某些特定节点过度燃烧，即防止一个节点占用所有存储或所有计算工作，而其他节点保持空闲。简而言之，在节点间均匀分布存储和计算。
*   **将不同团队的计算分开**，同时仍然将您的数据(*共享存储*)保存在一个每个人都可以访问的中心位置。例如，您可以将单独的“虚拟”计算能力分配给数据科学家，以便他们对 ML 的计算开销很大的查询不会影响其他用户。这个特性并不是所有云厂商都支持的(*只从雪花那里听说过【10】*)。

# 云供应商如何实现存储和计算的分离

在下文中，我只列出了利用 SD-MPP 架构的云数据仓库服务，该架构将存储与计算分开。由于这些云产品互不相同，我简要描述了它们是如何将共享数据范式整合到服务中的。

## 雪花

雪花首创，营销(*他们好像有很扎实的营销预算！*)多集群共享数据架构的概念( *SD-MPP* )。他们进一步将其分为[3]:

*   **数据库存储层** —在我们将任何数据加载到 Snowflake 之后，这是数据被持久化和优化的地方(*变成柱状形式并被压缩*)。这种存储对用户来说是抽象的，数据只有在运行查询时才可见。
*   **查询处理层** —决定数据在*虚拟仓库内部如何处理。*这是我们可以主动管理的计算层。我们可以为特定的团队创建几个仓库。
*   **云服务层** —包括元数据&基础设施管理、认证&访问控制以及查询优化。

雪花的最大卖点之一是他们的 SD-MPP 产品是云不可知的——你可以在亚马逊网络服务、Azure 或谷歌云平台上设置它[9]。

## 亚马逊红移

直到 2019 年 12 月，红移将被视为 SN-MPP 架构的典型例子。Redshift 是首批云数据仓库解决方案之一，自 2012 年 10 月上市。

AWS 可能注意到其他云供应商正在提供具有 SD-MPP 架构的竞争服务(*由于存储和计算分离而大幅降低成本*)，或者他们可能听取了客户的意见。起初，AWS 实现了**红移光谱**——一种提供额外计算层以直接从 S3 查询数据的服务。这个特性允许我们创建**外部表** ( *外部，因为它们不存在于数据仓库中——它们是从 S3* ) **中检索的，并将它们与数据仓库**中的现有表连接起来。它提供了数据仓库和数据湖之间的无缝数据集成，但它没有解决红移所基于的 SN-MPP 架构的问题。

**2019 年 12 月，AWS 发布:**

*   **亚马逊红移托管存储**，它允许我们在计算节点之间使用共享存储，可自动扩展至 8.2 PB。这种存储基于 S3 和固态硬盘的组合。AWS 完全管理数据在 S3 和 SSD 之间的存储和移动方式。
*   **面向红移的 AQUA(高级查询加速器)** —在托管存储层中包含硬件加速缓存，以加快操作速度。根据 AWS 的说法，这使得 Redshift 比任何云数据仓库快 10 倍[4]。[这是来自 re:Invent [5]的幻灯片](https://d1.awsstatic.com/events/reinvent/2019/NEW_LAUNCH_Amazon_Redshift_reimagined_RA3_and_AQUA_ANT230.pdf)，他们声称这种速度提升——然而，他们“*忘记”*链接他们性能基准的来源，所以我无法验证。
*   **新 RA3 实例类型** —此实例类型系列中的计算节点与红移托管存储协同工作。

## AWS 雅典娜

亚马逊还有另一个可以用于数据仓库和数据湖的服务:Athena。与 Redshift 相反，Athena 是一个无服务器选项，它将 Presto 引擎(*计算*)与 S3 ( *存储*)结合在一起，以按需从位于 S3 的数据湖中查询数据。您需要为每个查询支付+的 S3 存储费用。

## 国际商用机器公司

*IBM Db2 Warehouse on Cloud* 是一个完全托管的服务，采用 SD-MPP 架构，但有一些额外功能，如基于人工智能的查询优化器:

> 正常的查询优化器可能会继续建议相同的查询路径，即使在它被证明不如希望的有效之后，机器学习查询优化器可以模仿神经网络模式，从经验中学习。这有助于它不断改进，而不是不时地优化”。[6]

**补充说明:**在撰写本文时，IBM 声称提供 1000 美元的 IBM 云信贷，以便您可以试用他们的云数据仓库。你可以在这里找到更多关于[的信息。](https://www.ibm.com/cloud/blog/announcements/free-1000-usd-credit-toward-db2-warehouse-on-ibm-cloud)

## SAP 数据仓库云

在某些方面，SAP 采取了与雪花相似的方法，他们也提供虚拟仓库*，他们称之为“空间”:*

> *空间[…]是独立的，可以为可用磁盘空间、CPU 使用率、运行时间和内存使用率分配配额。[7]*

*他们承诺，在这些空间内，您可以彼此独立地扩展存储和计算。然而，存储似乎没有弹性增长，因为您被要求专门分配每个空间的磁盘空间配额。*

## *谷歌大查询*

*BigQuery 是完全无服务器的，因此它从用户那里抽象出存储和计算是如何工作的。BigQuery 自动扩展存储和计算，无需我们做任何事情。在引擎盖下，它使用了一个名为 Colossus 的**独立分布式存储层和一个名为 Dremel** 的**计算引擎。与 Amazon Athena 类似，Big Query 使用按查询定价的模型。***

# *现代数据仓库解决方案中存储和计算的分离模糊了数据湖和数据仓库之间的界限*

*公司倾向于构建数据湖**以节省成本** —数据湖提供无限存储，许多数据湖云服务提供**附加服务**以快速高效地从数据湖中检索数据，通常使用构建在数据湖之上的 **SQL 接口**。这样，我们可以获得一个存储层(*你的数据湖 ex。通过利用 AWS S3* 和一些 SQL 查询引擎作为(*无服务器*计算层来查询这些数据(*例如。亚马逊雅典娜*)。从架构的角度来看，这是一个类似于数据仓库中共享数据层的概念。另外，使用那些为数据湖构建的 SQL 接口通常类似于使用数据仓库。在某种程度上，这模糊了数据湖和数据仓库之间的界限。*

***证实这一假设的常见例子:***

*   *开源的 Presto+亚马逊雅典娜的 AWS 实现*
*   ***Upsolver** 为摄取和转换存储在数据湖中的数据提供 SQL 接口[8]*
*   *“老好人” **Apache Hive** 自 2010 年以来就为存储在 Hadoop 上的数据湖提供了一个 SQL 接口*
*   ***雪花**已经称自己为*云数据平台*，因为它在一个产品中结合了数据仓库和数据湖功能*
*   *Amazon Redshift 创建了 **Redshift Spectrum** 来提供在单个服务中一起查询数据仓库和数据湖的能力。*

# *结论*

*在本文中，我们了解了为什么计算与存储的分离对于**以经济高效的方式让您的云数据仓库**和数据湖架构**面向未来至关重要**。*

*我们回顾了我们如何实现**共享磁盘大规模并行处理架构**的历史，以及它是如何被*雪花、亚马逊、谷歌、SAP 和 IBM* 实现的。*

*最后，我们列出了这种方法的**优势，并得出结论，在现代云数据仓库解决方案中，计算与存储的分离模糊了数据湖和数据仓库之间的界限。***

*感谢您的阅读，并随时关注我的下一篇文章。*

***资源:***

*[1][https://en.wikipedia.org/wiki/Shared-nothing_architecture](https://en.wikipedia.org/wiki/Shared-nothing_architecture)*

*[2] Preetam Kumar: *切断绳索:使用对象存储将您的数据湖中的数据与计算分离*[https://www . IBM . com/cloud/blog/Cutting-cord-separating-data-compute-data-lake-object-storage](https://www.ibm.com/cloud/blog/cutting-cord-separating-data-compute-data-lake-object-storage)*

*[3]雪花文档:[https://Docs . snow flake . com/en/user-guide/intro-key-concepts . html #:~:text = installation % 20 和%20updates。-，雪花% 20 体系结构，节点% 20 在% 20 数据% 20 仓库中。](https://docs.snowflake.com/en/user-guide/intro-key-concepts.html#:~:text=installation%20and%20updates.-,Snowflake%20Architecture,nodes%20in%20the%20data%20warehouse.)*

*[4]AWS Pages:[https://Pages . AWS cloud . com/AQUA _ preview . html #:~:text = AQUA % 20 is % 20a new % 20 distributed，to % 20 compute % 20 clusters % 20 for % 20 processing。](https://pages.awscloud.com/AQUA_Preview.html#:~:text=AQUA%20is%20a%20new%20distributed,to%20compute%20clusters%20for%20processing.)*

*[5] AWS 幻灯片来自 re:Invent 2019 年 12 月[https://D1 . AWS static . com/events/reinvent/2019/NEW _ LAUNCH _ Amazon _ Redshift _ re imagined _ RA3 _ and _ AQUA _ ant 230 . pdf](https://d1.awsstatic.com/events/reinvent/2019/NEW_LAUNCH_Amazon_Redshift_reimagined_RA3_and_AQUA_ANT230.pdf)*

*[6] IBM 博客:[https://www . IBM . com/blogs/journey-to-ai/2020/03/the-technical-advances-behind-DB2/](https://www.ibm.com/blogs/journey-to-ai/2020/03/the-technical-advancements-behind-db2/)*

*[7] SAP 博客:[https://saphanajourney . com/data-warehouse-cloud/resources/what-are-spaces/](https://saphanajourney.com/data-warehouse-cloud/resources/what-are-spaces/)*

*[8]上解器:[https://www.upsolver.com/data-lake-platform](https://www.upsolver.com/data-lake-platform)*

*[9]雪花—支持的供应商:[https://docs . snow flake . com/en/user-guide/intro-cloud-platforms . html](https://docs.snowflake.com/en/user-guide/intro-cloud-platforms.html)*

*[10]雪花虚拟仓库:[https://www . analytics . today/blog/snow flake-Virtual-warehouse](https://www.analytics.today/blog/snowflake-virtual-warehouse)*