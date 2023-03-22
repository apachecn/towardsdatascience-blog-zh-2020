# 3 开源安全风险以及如何解决它们

> 原文：<https://towardsdatascience.com/3-open-source-security-risks-and-how-to-address-them-82f5cc776bd1?source=collection_archive---------36----------------------->

## 你需要知道的是

![](img/30042a3c97427c234400b8df281f4772.png)

迈克尔·盖格在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

开源软件非常受欢迎，并构成了商业应用程序的重要组成部分。据 [Synopsys](https://www.synopsys.com/content/dam/synopsys/sig-assets/reports/2020-ossra-report.pdf) 报道，99%的商业数据库至少包含一个开源组件，这些代码库中有近 75%包含开源安全漏洞。

公司和开发人员选择使用开源软件的一个主要原因是，它使他们不必自己开发这些基本功能。

哦，开源软件是免费的！

尽管有其优势，开源软件往往有可能影响您的数据和组织的漏洞。为了让您大致了解开源安全风险如何影响您的业务，我们列出了三大开源安全风险以及解决它们的方法。

在深入本文之前，我们先来看看开源漏洞到底是什么。

# 什么是开源漏洞？

开源漏洞基本上是开源软件中的安全隐患。这些是脆弱或易受攻击的代码，使得攻击者能够进行恶意攻击或执行未经授权的意外操作。

在某些情况下，开源漏洞会导致拒绝服务(DoS)等网络攻击。它还可能导致重大违规，在此期间，攻击者可能会未经授权访问组织的敏感信息。

当谈到开源软件时，有很多安全问题。例如，OpenSSL 是一个加密库，负责管理各种互联网连接软件的高度敏感的数据传输功能，包括运行一些最流行的电子邮件、消息和 web 服务的软件。

你还记得《心脏出血》吗？是的，那引起了不小的轰动！是的，那是 SSH 库中一个严重的开源漏洞。

同样，2014 年在 Bash shell 中发现了另一个流行的开源漏洞，Bash shell 是许多 Linux 发行版上的默认命令处理器。它有一个任意命令执行漏洞，可以通过 web 服务器上的服务器端 CGI 脚本和其他机制进行远程攻击。这种开源漏洞通常被称为“Shellshock”。

# 3 大开源安全风险是什么？

既然您已经对什么是开源安全风险有了一个合理的想法，那么让我们来探讨一下目前存在的三大开源安全风险，以及如何减轻这些风险。

# 软件安全风险

开源漏洞一旦被发现，就可能成为攻击者利用它们的诱人目标。

通常情况下，这些开源漏洞以及关于如何利用漏洞的细节都是公开的。这使得黑客能够获得实施攻击所需的所有必要信息。结合开源软件的广泛使用，你可以想象当一个开源漏洞被发现时，它会造成多大的破坏。

组织在解决开源漏洞时面临的主要挑战之一是跟踪漏洞及其修复并不像人们想象的那么容易。

由于这些开源漏洞发布在各种平台上，因此很难跟踪它们。此外，查找更新版本、补丁或修复程序来解决安全风险是一个耗时且昂贵的过程。

一旦开源漏洞及其利用途径被公布，攻击者利用它们并侵入您的组织只是时间问题。企业必须集成必要的工具和流程来快速解决开源漏洞。

# 功勋的宣传

开源漏洞在[国家漏洞数据库(NVD)](https://nvd.nist.gov/) 等平台上公开，任何人都可以访问。

公开可用的开源漏洞导致的攻击的一个著名例子是 2017 年的重大 [Equifax 违规](https://www.wired.com/story/equifax-breach-no-excuse/)，该信用报告公司泄露了 1.43 亿人的个人信息。这次攻击的发生是因为 Equifax 使用了一个具有高风险漏洞的开源 Apache Struts 框架版本，攻击者利用了这个漏洞。

这种对开源软件的攻击不仅会导致数据泄露或丢失，还会影响公司的市场声誉、估值和客户关系。这反过来会影响您的客户流失率、保留率、销售额和收入。处理由开源漏洞造成的违规影响可能是一个漫长而痛苦的过程。

# 许可合规风险

开源软件附带一个许可证，允许在定义的准则下使用、修改或共享源代码。然而，这些许可证的问题是，它们中的大多数不符合开源的严格的 OSI 和 SPDX 定义。

除此之外，单个专有应用程序通常包括几个开源组件，这些项目以各种许可类型发布，如 GPL、Apache 许可或 MIT 许可。

组织被要求遵守每一个单独的开源许可，这可能是相当压倒性的。尤其是随着快速开发和发布周期的到来，商业随之而来的事实是，现在存在将近 200 多种开源许可类型。

一项对 1253 个应用程序的研究发现，大约 67%的代码库有许可冲突，33%的代码库有未经许可的软件。不遵守许可证规定会使企业面临法律诉讼的风险，影响您的运营和财务安全。

# 您如何战胜这些开源安全风险？

接下来，让我们仔细看看这些开源安全风险的解决方案。

# 建立安全第一的文化

开发人员常常根据他们需要的功能和编程语言选择使用开源组件。虽然功能很重要，但也应该包括其他标准。

例如，项目的每个单独的组件都可以提供功能，而不需要集成整个项目代码库。这有助于限制开源软件的数量，并有助于简化集成，消除安全风险，以及降低非必需组件中的源代码复杂性。

开源软件和其他软件一样可能存在安全风险，所以你选择使用的每个组件都必须提供功能并且安全。

除此之外，开源项目通常专注于为最终用户提供具有新特性的新更新。由于时间和预算的限制，企业不太重视安全性，更倾向于尽快发布更新。

然而，公司应该在新版本之间保持平衡，同时确保设计、实现和代码是安全的。

你可以做的最重要的事情之一是清点你使用的开源软件，并跟踪与这些库相关的漏洞。

# 拥抱自动化和扫描开源软件中的漏洞

发现并修复开源软件中的漏洞本身就是一个巨大的挑战。公司需要找到一种方法来检测其环境中开放源代码中的所有安全漏洞，定期更新列表，促使开发人员远离旧的、不安全的软件组件，并最终在发现安全漏洞时部署补丁。

解决这个问题的一个方法是引入自动化工具，帮助您持续跟踪您的开源使用情况，并识别安全弱点、漏洞、修复和更新。

开源软件的自动化工具有助于识别哪些项目中使用了哪些包，它们包含哪些安全漏洞，以及如何修复它们。这些工具通常还带有警报功能。如果发现了漏洞，就会向相关的开发和安全团队发送通知，提醒他们新发现的安全风险。

集成自动化来扫描开源软件中的安全漏洞对于大型组织来说尤其重要，因为很难跟踪和识别所有正在使用的源代码中的漏洞。

大多数企业甚至不知道他们拥有的应用程序的完整清单，这使得他们更容易受到网络攻击，因为源代码中存在未知的漏洞。一份报告称，近 88%的代码库在过去两年中没有任何开发活动。

# 交叉培训你的员工

雇佣既精通开发又精通安全的专业人士并不总是容易，甚至是不可能的。然而，培训你的团队是可能的，这样他们可以从两端着手解决问题。虽然为不同的团队定期举行网络安全意识培训并不容易，但这对项目的整体安全性至关重要。

企业应确保其开发人员对网络安全有一个大致的了解，以及最新的趋势和更新。您的开发人员应该能够识别开源代码中出现的常见安全问题，如果没有修复它们的话。

同样，安全团队应该从早期阶段就参与开发过程。与其让安全性成为事后的想法，不如从项目一开始就把它放在优先位置。

正如您分析和跟踪您的开发过程一样，您也应该主动监控您的安全工作。采取积极主动的方法对准备处理开源安全风险大有帮助。

# 最后的想法

开源是一个优秀的模型，在当今的许多项目中都可以找到。然而，为了确保安全的开源代码，您需要认识到开源软件带来的安全风险。您必须确保您的每个开源组件都为项目提供了价值，并且是安全的。

Cypress Data Defense 通过推荐最佳安全实践，帮助公司进行安全审计并加强其项目的整体安全性。

*我们帮助企业创建发布安全更新的路线图，提供开源支持、扫描、监控，并提供安全有效利用开源软件的解决方案。借助 Cypress Data Defense，组织可以获得对其开源组件的必要控制，以降低开源安全风险，同时增加成本节约。*

# 关于作者:

Steve Kosten 是 [Cypress Data Defense](https://www.cypressdatadefense.com/) 的首席安全顾问，也是“Java/JEE 中的 SANS DEV541 安全编码:开发可防御应用程序”课程的讲师。

***来自《走向数据科学》编辑的提示:*** *虽然我们允许独立作者根据我们的* [*规则和指导方针*](/questions-96667b06af5) *发表文章，但我们并不认可每个作者的贡献。你不应该在没有寻求专业建议的情况下依赖一个作者的作品。详见我们的* [*读者术语*](/readers-terms-b5d780a700a4) *。*