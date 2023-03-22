# 针对您的应用的 5 种开发运维监控策略

> 原文：<https://towardsdatascience.com/5-devops-monitoring-strategies-for-your-application-6fb01363a928?source=collection_archive---------32----------------------->

![](img/4035afeb5f8a97d80fc1818ab27bf401.png)

妮可·沃尔夫在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

如今，越来越多的公司采用 DevOps 进行持续集成和持续交付。在 DevOps 领域，自动化经常成为焦点。

这并不奇怪。为什么？

根据 Puppet 的 [2019 年开发运维状况报告](https://puppet.com/resources/report/state-of-devops-report/)，开发运维自动化对组织的整体效率具有积极影响

然而，也许比自动化更重要的是，DevOps 监控是另一个关键元素，有助于在交付管道的每个阶段提高意识。

您可能需要考虑监控的许多方面。比如什么？

您应该监控什么，使用哪些工具，或者如何开始您的 DevOps 监控策略。

虽然监控先于 DevOps，但 DevOps 进一步改变了软件开发过程，以至于监控也必须发展。软件开发的整体步伐随着开发运维而加快，团队现在正在自动化集成和测试，并在云中部署软件，以快速的时间表和连续的交付。

有了 DevOps，现在需要监控的东西更多了，从集成、供应到部署，团队需要使用 DevOps 监控策略来有效地监控项目的不同方面。

# 对于您的应用，最好的 5 种 DevOps 监控策略是什么？

为了帮助您在快速变化的环境中使用 DevOps 监控策略，我们创建了一个通用框架来帮助您了解如何开始、监控哪些内容、使用哪些工具来满足监控需求，以及您可以在何处进行整合。

# 确定您应该监控的内容

有效开发运维监控策略的第一步？

确定应用程序中应该监控的内容。监控目标可以分为几个主要类别，您可能希望至少涵盖每个类别的一个方面。

这些类别包括:

*   服务器运行状况
*   应用程序日志输出
*   脆弱点
*   发展里程碑
*   用户活动

## 发展里程碑

监控开发里程碑是您的 DevOps 策略运行情况的指示器。这是深入了解您的工作流程并确定您的团队运作效率的有效方式。跟踪每次冲刺的持续时间；缺陷被识别、记录和修复的速度；和预期交付特性的比率。

询问以下问题:

*   我们能赶上最后期限吗？如果没有，是什么阻碍了这一进程？
*   团队是否有效地遵循 DevOps 方法？

尽可能整合监控工具，以简化和加快故障排除。使用开源和开放许可代理来扩展技术并保持独立于供应商。

还有什么？

您可以使用机器学习技术来自动化配置任务并节省时间。

## 脆弱点

漏洞可以大致分为两类:通过国家漏洞数据库(NVD)维护的列表广为人知或可识别的应用程序中的已知弱点或漏洞，以及由于应用程序中不安全的编码实践、不安全的设计或不安全的架构而出现的漏洞。

企业必须监控这些漏洞并及时缓解它们。这些漏洞可以通过多种方式解决，例如修改第三方依赖关系、定期进行安全代码审查、培训您的软件开发团队以及雇佣有经验的专业人员。

## 用户活动监控

用户活动监控可能是 DevOps 最明显的监控策略之一。应持续监控异常请求或意外输入，例如多次失败的登录尝试、异常登录次数和未知登录设备，以确保只有授权用户才能访问系统。

还有呢？

监控用户行为还有助于检测异常活动，如访问权限提升。例如，开发人员试图访问管理员帐户。

这种不寻常的行为和请求可能会引发怀疑，并使您更加意识到由于用户活动监控不力而可能发生的潜在内部威胁或其他网络攻击。

## 应用程序日志输出

监控应用程序日志输出经常被低估，但是如果您的服务是分布式的，并且您没有集中的日志记录，那么这个任务就困难得多。

此外，如果错误和漏洞没有被实时检测到，它们就没有多大价值。确保错误代码或易错代码实时生成通知，并且这些通知易于搜索，这一点很重要。在生产环境中跟踪 bug 或错误的能力是一个巨大的优势。

## 服务器运行状况

通过分析可用资源的性能和正常运行时间来监控服务器的健康状况。确保配置正确，扫描功能正常工作，例如识别应用程序中的[漏洞。](https://cypressdatadefense.com/blog/web-application-vulnerabilities/)此外，确保服务器强化到批准的配置。

# 确定监控功能

DevOps 的监控工具应该能够从开源代理收集性能时间序列数据，跟踪机器学习在警报和报告方面的应用，并在可扩展的时间序列数据库中收集数据。

以下是一个或多个监控工具可能提供的一组功能:

*   **仪表盘**:预置易于定制的仪表盘，与同行分享。
*   **诊断**:对您的整个应用程序堆栈进行故障排除，以识别潜在的漏洞，并确保所有功能都按预期运行。
*   **数据收集器**:每种编程语言和中间件的开源和开放许可代理。
*   **数据保留**:时序性能数据和日志数据。
*   **通知**:可与升级服务和即时消息集成的实时警报。
*   **报告**:深入的见解和报告，有助于确定绩效热点和规划。
*   **REST API** :包含自定义数据，通过文档化 API 更新配置，访问任何数据。
*   **机器学习**:非实时的容量损失分析和实时的异常检测。

# 监控您的整个应用体系

您选择的 DevOps 监控工具应该能够端到端地监控您的整个堆栈，并提供更快的故障排除和快速补救。此列表本质上并不全面，而是旨在涵盖应用中最大的功能集:

## 基础设施监控

基础设施监控是全栈应用监控策略的关键组成部分。

工具应该测量什么？

*   有效性
*   CPU 使用率
*   磁盘使用
*   正常运行时间
*   响应时间
*   数据库
*   储存；储备
*   成分
*   虚拟系统
*   表演
*   用户权限
*   安全性
*   网络交换机
*   流程级使用
*   应用程序的吞吐量
*   服务器的负载

此外，它们还应该能够提供趋势的历史、测量的时间序列数据，以及具有过程级向下钻取的数据的集合。

## 网络监视

网络监控工具应该能够测量性能指标，如延迟、不同端口级别的指标、带宽、主机的 CPU 使用率、网络数据包流量，并提供自定义指标。一般来说，网络监控工具需要一个跨各种网络拓扑(如基于云的网络和异构网络)工作的平台。

## 应用程序性能监控

应用程序性能监控是通过应用程序上可用的跟踪和分析来搜索、收集和集中日志的地方。

它还有助于提供对性能的测量，如可用性、错误率、吞吐量、用户响应时间、慢速页面、页面加载、第三方 JavaScript 慢速、track[SLA](https://freshservice.com/sla)、浏览器速度，以及对最终用户事务的检查。

尽管这个列表并不详尽，但它应该让您了解现有的监控工具提供了什么，以及 DevOps 监控策略中有哪些漏洞。

# 评估开发运维工作流的监控工具

创建一个大纲框架，开发运维团队可以将其作为评估流程的起点。

通过概述适用于您的整体 DevOps 监控策略的目标，您可以将评估期间的关注点缩小到特定问题，例如:

“这个监控工具符合我的目标和需求吗？”

了解 DevOps 监控工具及其提供的功能将有助于您在评估过程中深入了解特性功能。

还有呢？

了解与每个监控方面(如应用程序监控或基础架构)相关的监控功能，将有助于为更具体、更全面的 DevOps 监控策略提供最佳选择。

# 利用工具进行有效的开发运维监控

以下是当今市场上最好的 DevOps 监控工具:

*   **Collectl** — Collectl 将各种性能监控工具整合到一个平台中。它可以监视各种子系统，如节点、存储、处理器、TCP 和文件系统。Collectl 运行在所有的 LInux 发行版上，可以在 Debian 和 Red Hat 仓库中获得。
*   **Consul** — Consul 在众多数据中心环境中提供键值存储、发现、故障检测和其他功能。它与用于查询服务的内置 DNS 服务器集成在一起，并且支持现有的基础设施，而无需修改代码。
*   **上帝** —上帝使用 Ruby 框架来提供一种简化的监控方法。它可以在 BSD、Darwin 系统和 Linux 上获得。上帝提供了一种编写事件条件和轮询事件的简化方法。它还提供了一个集成的自定义通知系统。
*   **Ganglia** — Ganglia 利用了针对集群联合优化的分层设计。它使用 XDR 和 XML 等常见技术进行数据表示和传输，并使用独特的数据结构和算法方法来实现高级别的并发性并减少节点上的开销。
*   **Nagios** — Nagios 结合使用无代理和基于代理的软件工具，为 Unix、Linux、Windows 和 web 环境提供应用程序、网络和服务器监控。该系统使用各种报告格式和可视化来提供正常运行时间、响应和可用性。

# 外卖食品

企业创建和实施有效的 DevOps 监控策略至关重要。DevOps 中更快的开发过程带来了几个挑战，特别是由于快速过程或缺乏测试而可能留下的系统中的漏洞。

拥有高效且可扩展的 DevOps 监控策略将有助于您深入了解您的应用，在流程的早期发现漏洞，并减少漏洞。请记住，虽然监控的一个方面可能比另一个方面对您的业务更重要，但评估您的应用程序或项目的各个方面是至关重要的。

如果您对 DevOps 监控策略有任何疑问或需要任何帮助，请联系我们。

**关于作者:**

Steve Kosten 是 [Cypress Data Defense](https://www.cypressdatadefense.com/) 的首席安全顾问，也是“Java/JEE 中的 SANS DEV541 安全编码:开发可防御应用程序”课程的讲师。