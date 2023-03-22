# 优化企业级数据消费的策略

> 原文：<https://towardsdatascience.com/strategies-for-optimising-enterprise-level-data-consumption-7e2c95b6ba96?source=collection_archive---------54----------------------->

![](img/aa4833bc22e28996268ef03d85c79695.png)

由 [geralt](https://pixabay.com/users/geralt-9301/) 在 [Pixabay](https://pixabay.com/photos/integration-migration-refugee-2489613/) 上拍摄的照片

中间件服务，使用 ETL/ELT 和 MASA(网格应用和服务架构)的数据仓库

作为一名顾问，经常会遇到这样的客户需求:

*   我们需要消费多个信息系统的数据，所以要从它们调用多个 API 来获取所有的数据，这是一个很大的痛苦。
*   我们确实在一个数据库中有所有的数据，但是我们需要查询几十个表来将它们连接在一起以获得预期的结果。
*   我们相信我们有一个非常好的数据架构。DB 实例包含用于不同目的的多个数据库，我们以 3-norm 设计一切。然而，当我们想要跨多个数据库对整个系统进行一些统计时，这仍然是令人痛苦的。

# 用例

![](img/d080c687da569d2555f6117a7921fdff.png)

由 [KOBU 机构](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

通常，三种类型的需求会导致上述问题。

## BI(商业智能)仪表板

这可能是最常见的达到限制的用例。

虽然该公司仍处于初创阶段，但很快获得任何类型的数据可能都相对容易。在这个阶段，即使是 Microsoft Excel 也足以满足大多数需求。此外，不建议采用复杂的数据架构，因为这对初创企业来说成本太高。

然而，假设公司发展良好，可能会建立越来越多的部门，以及扩展更多的业务领域，数据持久层将会更加复杂。例如，财务、运输、IT 部门有多个独立的数据库。如果业务是 B2b，也可能有不同客户的多个数据库。当然，每个数据库中的表数量也可能很大。

现在，该高管希望拥有 BI 仪表板来支持决策制定。可以看出，一些高级报告可能需要涉及几个数据库中的大量表格。

## 业务流程中需要

同样常见的是，一些业务场景需要复杂的 SQL 查询作为流程的一部分，比如验证。

例如，公司依赖多个信息系统。在一些特定的业务场景中，我们需要根据几个信息系统来验证客户的请求。

在这种情况下，优化公司范围的数据架构会更有帮助，因为性能会影响正常的业务流程。

## 高级分析

如果公司是“数据驱动”的，或者其业务交易产生大量高速数据，则通常会涉及高级分析，如机器学习技术，以提高业务效率，识别潜力等。

在这种情况下，从多个系统中提取数据来训练机器学习模型或向部署的模型输入正确的数据可能是一场噩梦。

# 原因和可能的解决方案

![](img/4015603320d7943d138a5caa781f5ad3.png)

塞萨尔·卡利瓦里诺·阿拉贡在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

主要困难/原因是:

*   查询本身可能非常复杂，包括各种技术，如连接和连接表、IF-ELSE 判断和大量条件过滤。
*   由于涉及的表太多，性能根本无法保证。
*   对于某些 DBMS，跨多个数据库运行查询可能并不容易。

根据我的经验，对于这种企业数据架构问题，有 3 种典型的解决方案。

## 中间件服务

经济性:★★★☆
维修性:★☆☆☆
灵活性:★☆☆☆

![](img/18d08173a368e52dd66614ac5bcd2fdc.png)

照片由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 [zibik](https://unsplash.com/@zibik?utm_source=medium&utm_medium=referral) 拍摄

这个解决方案指的是构建一个中间件服务来与多个系统通信，并在返回到数据消费实体之前连接/聚合结果。

实现这一点的技术可以是多种多样的，可以是 Python、Java、Node。JS，C#，PHP 等。基于不同的前端数据消费实体，这些技术各有利弊。

这个解决方案可能是花费最少资源的一个，因为它是强烈的需求驱动的。也就是说，每当您需要另一个复杂的查询时，您要么需要向现有的中间件服务添加更多的组件，要么甚至从头开始开发一个新的组件(这可能是因为 DBMS 使用了完全不同的接口)。

因此，这种解决方案的可维护性和灵活性是最差的，尽管有时如果可以预见需求在短期内不会扩展，它仍然是最好的解决方案。

**优点**:

*   需求导向，只为你需要的东西开发
*   成本相对较低

**缺点**:

*   没有建立“平台”，因此未来新的类似需求将需要几乎相同的努力。
*   这个解决方案没有标准。如何实现完全取决于开发者。
*   对数据的每个请求都会触发对所有系统的查询，因此增加了所有现有系统/数据库的负担。
*   难以维持。

## 企业数据仓库

经济性:★★★☆
维修性:★★★☆
灵活性:★★★☆☆

![](img/52cb9a124e8dceb1cc3123e2a3c8b4f3.png)

[emy](https://unsplash.com/@grimnoire?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

数据仓库可能是目前业界最流行的解决方案。基本思想是建立一个系统，可以从多个信息系统中提取数据，然后将所有符合数据仓库标准(星型或雪花型模式)的数据存储在一个数据仓库中。

企业数据仓库通常包括以下组件:

*   **ETL/ELT 数据管道**，其**从各种数据源提取**数据，然后**转换**数据到**加载**到数据仓库。随着大数据概念的发展，ELT 在业界越来越受欢迎，比 ETL 更受欢迎的还有 Azure 等一系列云提供商和 Apache Spark 等一堆分布式/并行计算引擎。
*   **数据仓库**是关于数据如何存储在 DBMS 中的另一个标准。与关注于提高插入/更新/删除性能的常规事务数据库不同，数据仓库是面向报告的，为阅读而优化。因此，从多个数据源提取数据并在存储到数据仓库之前对其进行预聚合是非常常见的，因此可以通过简单地查询几个表而不是几十个表来消耗数据。

**优点**:

*   这是一种“非侵入性”的解决方案。也就是说，消费请求由数据仓库来满足，因此事务系统没有额外的负担。
*   无论数据源的类型如何，在 ETL/ELT 过程中，都必须有相应的技术来从中提取数据。
*   数据可以预先转换。例如，不同的系统可能使用不同的用户性别指标(男/女、男/女、0/1 等。)，但我们可以在转换中统一它们。
*   数据可以预先汇总。例如，可以在 ETL/ELT 过程中生成每日/每周/每月报告，因此消费者可以非常高效地读取可操作的数据。
*   使用 SCD(渐变维度)设计，数据仓库可以捕获数据源评估的历史。例如，如果有一个产品被移动到一个新的类别，它在数据仓库中是完全可追踪的，但是您可能会在事务数据库中丢失这个更改。

**缺点**:

*   数据仓库中的数据会延迟一段时间才可用。例如，如果 ETL/ELT 过程每天都在运行，那么数据每天都是最新的，直到“昨天”。
*   如果一个数据源改变了它的数据结构，ETL/ELT 需要相应地改变，这可能会导致大量的工作，以及在应用改变期间潜在的数据差异。
*   依赖于数据源特性。例如，如果原始数据源没有可靠的时间戳，ETL/ELT 过程就不能以优雅的方式实现增量加载(只加载自上次加载以来新的/更改的记录)。

## MASA(网状应用和服务架构)

经济性:★☆☆☆
维护性:★★★★
灵活性:★★★★

![](img/9d50808bb8f03bab5f0f6c29af7d3ed3.png)

由[阿德里安·施瓦茨](https://unsplash.com/@aeschwarz?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

MASA 是 Gartner 提出的一个相对较新的概念。它是从大量数据密集型企业(如优步[1])的经验中总结出来的。

令人惊讶的是，MASA 的想法更接近于第一种解决方案——中间件服务。然而，MASA 架构的重点是在企业后端系统(不面向客户)和前端系统(面向内部/外部客户)之间建立一个完整的综合 API 中介层。因此，MASA 和中间件服务之间的主要区别在于，前者旨在为不同粒度的后端系统构建统一的、系统的和可管理的服务。

MASA 架构由 3 个主要层组成[2]:

*   **多粒度服务**，包括所有的企业后端服务。“多粒度”意味着后端服务具有不同的规模，因此它们支持外部数据消费的能力也不同。例如，ERP/CRM 系统通常包含许多子组件，这些子组件被设计为在内部彼此紧密合作，而不是向外部提供数据。因此，确定后端服务的粒度以应用不同的策略非常重要。
*   **API 中介**，负责将请求从外部 API(数据消费者的接口)映射到内部 API(后端服务的接口)。在两个 API 层之间的委托过程中，it 部门还需要实时转换数据，确保安全性，并监控使用情况和性能。
*   **多体验应用**，也称为“适合用途”应用。无论数据的最终用户是谁，目的是什么，前端的设计都应该满足他们的需求，并以期望的表示形式提供数据。

**优点**:

*   MASA 是真正的“真实的单一来源”,因为它不像数据仓库那样以另一种形式复制数据。
*   最大限度地提高企业级所有数据消费的灵活性和敏捷性。比如可以在全公司范围内实现“自助式”数据消费。
*   理论上，数据可用性没有延迟。

**缺点:**

*   昂贵的
*   昂贵的
*   昂贵的

# 摘要

![](img/8976f875f61551a8fd81ed9f42763388.png)

由[在](https://unsplash.com/@helloquence?utm_source=medium&utm_medium=referral) [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的

在这篇文章中，我解释了我对企业数据平台优化的看法。事实上，在一家数据驱动型公司的发展过程中，这三种解决方案都有可能被利用。也就是说，当一家公司仍处于初创阶段时，可能根本没有任何“优化”的解决方案。随着一些需求的提出，由于资源有限，公司可能会开始使用更简单的解决方案来解决这些问题。然后，随着公司越来越成熟，可能会引入数据仓库。我相信大多数公司可能只需要这种解决方案，并在很长一段时间内使用数据仓库。最后，如果该公司成为其行业的巨头，MASA 将成为最终的解决方案。

[](https://medium.com/@qiuyujx/membership) [## 通过我的推荐链接加入 Medium 克里斯托弗·陶

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@qiuyujx/membership) 

如果你觉得我的文章有帮助，请考虑加入 Medium 会员来支持我和成千上万的其他作者！(点击上面的链接)

# 参考:

[1] Searle 等人【2017 年十大战略技术趋势:Mesh App 和服务架构。高德纳研究公司。[https://www . Gartner . com/en/documents/3645328/top-10-strategic-technology-trends-for-2017-mesh-app-和](https://www.gartner.com/en/documents/3645328/top-10-strategic-technology-trends-for-2017-mesh-app-and)

[2] B .戴利。MASA: *如何用应用、API 和服务创建一个敏捷的应用架构*。高德纳研究公司。[https://www . Gartner . com/en/documents/3980382/masa-how-to-create-a-agile-application-architecture-wit](https://www.gartner.com/en/documents/3980382/masa-how-to-create-an-agile-application-architecture-wit)