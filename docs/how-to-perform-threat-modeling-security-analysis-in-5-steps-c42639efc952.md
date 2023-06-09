# 如何通过 5 个步骤执行威胁建模和安全分析

> 原文：<https://towardsdatascience.com/how-to-perform-threat-modeling-security-analysis-in-5-steps-c42639efc952?source=collection_archive---------22----------------------->

![](img/ccced3c64aed9bfb9d7641731fc634dd.png)

彼得·拉格森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

想学习如何执行威胁建模吗？

那么，你来对地方了。

但在此之前，让我们快速讨论一下执行威胁建模和安全分析的重要性。

如今，几乎所有的软件系统都面临着各种各样的威胁，随着技术的成熟，网络攻击的数量也在不断上升。根据[的一份报告](https://www.mcafee.com/enterprise/en-us/assets/reports/rp-quarterly-threats-sep-2018.pdf)，2018 年第二季度，利用软件漏洞的恶意软件增长了 151%。

[安全漏洞](https://www.cypressdatadefense.com/blog/business-data-breach/)可能是由内部或外部实体造成的，它们可能会带来灾难性的后果。这些攻击可能会泄漏您组织的敏感数据或完全禁用您的系统，甚至可能导致数据完全丢失。

您如何保护您的数据不被窃取或防止恶意攻击您的设备？

一种开始的方法是执行威胁建模，这是一个帮助您分析您的环境、识别潜在的漏洞和威胁，并创建适当的安全需求来[应对这些威胁](https://www.cypressdatadefense.com/security-assessments/why-security-testing-is-important/)的过程。

# 对于您的设备，什么是合适的安全级别？威胁建模如何帮助您实现这一级别？

为了设计安全性，建议开发人员和制造商分析操作环境，以确定每台设备可能受到的攻击，然后记录下来。

理解和记录安全需求的过程被称为威胁建模和安全分析(TMSA)。

但是，执行威胁建模和安全分析如何帮助您保护您的设备免受网络安全攻击呢？

它可以帮助您分析您的设备并了解:

*   您的安全性需要有多强？
*   您应该采取哪些预防措施来避免安全问题？
*   哪些潜在威胁会影响您的设备？

威胁建模和安全分析(TMSA)强调了在实施安全措施来保护您的产品或设备时应该考虑的关键问题和挑战。

它会提示您考虑一些关键问题，例如:

*   您的设备面临哪些潜在威胁？
*   这些威胁有多严重？
*   您的设备符合安全标准吗？
*   有哪些潜在的漏洞会使您的设备面临安全漏洞的风险？
*   您可以实施什么对策来保护您的设备？

# 执行威胁建模的步骤

下面是一个分步过程，它将帮助您了解如何执行威胁建模和安全分析来确定您的安全需求。

# 步骤 1:确定用例、要保护的资产和外部实体

执行威胁建模的第一步是确定一个用例，即作为您的[安全评估](https://www.cypressdatadefense.com/security-assessments/)主题的系统或设备。通过这样做，你将会知道什么设备或系统需要进一步分析。

由于攻击者可能会以您的设备为目标来窃取重要数据或恶意操作，因此您需要识别包含敏感信息或最有可能受到攻击的资产。

例如，如果您有一个智能扬声器，那么您可能希望保护以下资产:

*   登录凭证
*   网络通信
*   固件
*   事件日志
*   证书和唯一密钥
*   系统配置(保护您的 IP 地址)
*   设备资源(如扬声器、麦克风阵列、电池、存储、调试接口、网络带宽和计算能力)

您的设备中可能有许多不同的资产，但重要的是，您要专注于保护保存有价值数据且对您的组织和客户至关重要的资产。

此外，为了识别和[了解可能影响您设备的潜在威胁](https://www.cypressdatadefense.com/blog/business-data-breach/)，您需要确定与设备交互的外部实体和用户。

这可能包括合法用户，如虚拟系统管理员或设备所有者。但是它还应该扩展到识别试图访问设备的潜在对手或攻击者。

一旦确定了这些，就该进入执行威胁建模的下一步了。

# 步骤 2:确定信任区域、潜在对手和威胁

在执行威胁建模的这一步中，您必须确定信任区域和相应的入口-出口点。通过使用这些信息，您可以开发带有权限边界的数据流图，这将帮助您定义输入数据验证、用户身份验证和错误处理的方法。

此外，您需要创建一个基于对手的威胁模型，以帮助您识别可能试图利用或攻击您设备的潜在对手和攻击者。

通常，基于对手的威胁模型有四类攻击者:

*   **网络攻击者:**这种类型的攻击者可能会进行中间人攻击等网络攻击，攻击者拦截双方的通信。
*   **恶意内部攻击者:**这些攻击者可能是您的员工、第三方供应商或任何能够访问您的设备或网络的个人。
*   **远程软件攻击者:**大多数攻击者都属于这一类，他们试图通过引入恶意脚本/代码或病毒来破坏安全软件，从而窃取数据或控制设备/网络。
*   **高级硬件攻击者:**这些攻击者通常拥有高级资源，需要物理接触设备。他们经常在专业设备的帮助下部署复杂的攻击，如显微镜探测或离子束光刻。

至此，您应该已经确定了需要保护的内容，以及哪些潜在的对手可能会导致安全漏洞。

接下来，您应该识别潜在的漏洞，包括软件、物理设备、开发生命周期和通信，它们可能作为进入您设备的入口点，并允许攻击者进入您的系统。

这些漏洞包括哪些？

这些漏洞可能包括过多的用户访问权限、薄弱的密码策略、缺乏 Web 应用程序防火墙(WAF)、不可靠的身份验证、不安全的加密存储、缺乏安全指南或安全错误配置。

一旦确定了潜在的漏洞，就可以针对每个入口点实现一个威胁模型来确定安全威胁。

但是，如何设计合适的安全级别来保护您的设备免受这些威胁呢？

在识别潜在的安全威胁后，您需要考虑评估每个威胁或攻击的严重性，并适当地分配您的资源。

您可以使用通用漏洞评分系统(CVSS)来评估威胁的影响。它使用 0 到 10 之间的分数来帮助您了解攻击会如何影响您的设备。

例如，如果威胁的 CVSS 分数是 9，那么您应该将您的资源和注意力集中在它上面，因为它的影响将是严重的。

通过这样做，您将能够在您的设备中建立适当的安全级别。

# 步骤 3:确定应对潜在威胁的高级安全目标

在如何执行威胁建模的这一步中，您必须建立安全目标，重点维护以下安全元素:

*   机密
*   有效性
*   完整
*   安全开发生命周期
*   真实性
*   不可否认性

攻击的类型决定了这些安全元素的风险。

例如，您可以确定篡改攻击可能会影响设备的完整性，而欺骗攻击可能会影响设备的真实性。

一旦您评估了潜在威胁及其严重性，您将能够确定需要采用什么对策来应对这些威胁，以及如何适当地应对它们。

# 步骤 4:明确定义每个安全目标的安全需求

由于每个威胁对高级安全目标构成不同的风险，您需要分析并创建具体的、可操作的安全需求，以直接应对这些威胁。

例如，为了保护身份，您应该:

*   维护角色、可信的通信渠道和授权
*   实现最低特权用户访问
*   设置故障阈值限制
*   安全远程管理

# 步骤 5:创建一个文档来存储所有相关信息

一旦收集了为系统设置安全要求所需的所有必要信息，就可以创建一个威胁建模文档来准确存储这些信息。

你应该在这份文件中包括什么？

该文档应包括单独的表格，列出您需要保护的资产、潜在的对手和威胁、您需要采取的对策以及安全要求。

它应该是结构良好的，并且具有清晰简明的信息，以帮助您了解攻击的潜在严重性以及如何应对每种威胁。

维护良好的文档可以帮助您高效地执行威胁建模和安全分析(TMSA)。

# 本指南中关于如何执行威胁建模的关键要点

既然您对威胁建模以及如何执行威胁建模有了更多的了解，那么就从 TMSA 文档开始吧。请记住，您需要[根据安全需求](https://www.cypressdatadefense.com/blog/application-security-best-practices/)识别潜在的漏洞，这将有助于保护您的系统免受攻击者和威胁。

关于如何执行威胁建模，您还有其他问题吗？请联系我们的安全专家。

**关于作者:**

Steve Kosten 是 [Cypress Data Defense](https://www.cypressdatadefense.com/) 的首席安全顾问，也是“Java/JEE 中的 SANS DEV541 安全编码:开发可防御应用程序”课程的讲师。