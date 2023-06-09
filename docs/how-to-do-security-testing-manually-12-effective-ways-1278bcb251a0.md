# 如何手动进行安全测试:12 种有效方法

> 原文：<https://towardsdatascience.com/how-to-do-security-testing-manually-12-effective-ways-1278bcb251a0?source=collection_archive---------18----------------------->

![](img/35d2d04c6da8f17fdbfad5467509529d.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的 [ThisisEngineering RAEng](https://unsplash.com/@thisisengineering?utm_source=medium&utm_medium=referral)

对于世界各地的企业来说，网络安全攻击正变得越来越突出。随着攻击的不断发展，大约 [68%的商业领袖](https://www.accenture.com/_acnmedia/PDF-96/Accenture-2019-Cost-of-Cybercrime-Study-Final.pdf#zoom=50)感到他们的网络安全风险在增加。

不能再忽视安全测试的需要。

虽然一些公司依靠少量的自动化安全测试工具和流程来维护安全合规性，但其他公司利用自动化测试和手动安全测试来确保他们的软件经过全面测试并且安全。

有许多方法可以手动进行安全测试，以测试应用程序的安全状态。在我们深入研究它们之前，让我们仔细看看为什么您应该手动进行安全性测试。

# 为什么您应该手动进行安全测试？

即使自动化技术发展迅速，仍然有许多因素需要人工注意来验证或准确确定应用程序中潜在的 web 安全漏洞。

一些潜在的漏洞，如业务逻辑问题或加密问题，需要人工来验证漏洞。

这就是为什么您需要手动进行安全性测试。

手动安全测试人员通常使用精选的安全测试软件和工具的组合，这些软件和工具最适合评估他们的应用程序。这些可能包括定制脚本和自动扫描工具。

手动进行安全测试的高级技术包括精确的测试用例，如检查用户控制、评估加密功能，以及彻底分析以发现应用程序中的嵌套漏洞。

手动进行安全测试并不意味着您不能使用自动化。相反，安全专家可以利用自动化技术来寻找模式或其他线索，这些模式或线索可能揭示关于应用程序漏洞的重要信息。

手动安全测试的主要目标是发现应用程序中的弱点和[潜在漏洞，这些弱点和漏洞可能无法被自动化安全测试完全理解或发现。](https://cypressdatadefense.com/blog/web-application-vulnerabilities/)

不管使用多少自动化测试软件和工具，手动分析软件行为以确保其完整性、机密性和可用性原则不被违反是至关重要的。

# 帮助您手动进行安全测试的技术

当应用程序安全性中的任何弱点需要真正的人类判断时，您可以手动进行安全性测试。有一系列手动安全测试技术可以帮助您评估您的应用程序和系统，以确保它们是安全的。

以下是一些关于如何手动进行安全性测试的最有效的方法:

# 1.监控访问控制管理

无论是 web 应用程序还是计算机，访问控制都是帮助保护您的应用程序安全或系统不被攻击者或内部威胁利用的一个重要方面。

访问控制管理可以分为两个部分:

*   认证—你是谁？
*   授权—您能做什么？您能访问哪些信息？

例如，员工应该只能访问完成其工作所需的信息。

通过实施访问控制，您可以确保只有经过授权的用户才能访问数据或系统。

为了手动测试，测试人员应该创建几个具有不同角色的用户帐户。

然后，测试人员应该尝试使用这些帐户访问应用程序或系统，并验证每个用户帐户只能访问自己的表单、屏幕、帐户、菜单和模块。然后，测试人员可以在不同用户/角色的会话中测试一个用户/角色发出的请求。

如果测试人员能够使用禁用的帐户登录应用程序，他/她就可以记录应用程序的安全性问题。

还有呢？

具有受限或较低访问权限的用户不应该能够访问敏感信息或高权限数据。

您还应该手动测试密码质量规则、默认登录、密码恢复、密码更改、web 安全问题/答案、注销功能等。

类似地，授权测试还应该包括对水平访问控制问题、授权缺失、路径逆转等的测试。

# 2.动态分析(渗透测试)

[渗透测试](https://www.cypressdatadefense.com/security-assessments/application-security-testing/web-application/dynamic-penetration-testing-reporting/)或 pen 测试，是一种软件测试技术，它使用受控的网络攻击来瞄准正在运行的系统，以确定可能被攻击者利用的漏洞。

运行系统的手动渗透测试包括以下步骤:

*   **数据收集** —手动渗透测试的第一步是收集数据，如表名、数据库、第三方插件信息、软件配置等。可以手动完成，也可以使用在线免费提供的测试工具(如网页源代码分析)来完成。
*   **漏洞评估** —一旦收集到数据，软件渗透测试团队将对其进行评估，以确定可能使系统面临安全攻击风险的安全风险或漏洞。
*   **发起模拟攻击** —渗透测试团队对目标系统发起受控攻击，以探索更多漏洞，并了解他们如何阻止攻击。
*   **报告准备** —在针对潜在的漏洞对系统进行了全面的定位和评估之后，[软件测试团队](https://www.nexsoftsys.com/articles/cognitive-test-automation-challenges-benefits-methodologies.html)创建一份报告，概述测试的发现，以及保护系统所需的措施。

当您想要手动进行渗透测试以增强系统的安全性时，这是您需要遵循的过程。

# 3.静态分析(静态代码分析)

另一种流行的手工安全测试方法是静态代码分析。它通常作为白盒测试的一部分来执行，也称为代码审查，执行它是为了突出“静态”(非运行)源代码中的潜在漏洞。

[静态代码分析使用](https://www.cypressdatadefense.com/security-assessments/application-security-testing/web-application/static-analysis/)技术，如数据流分析和污点分析，来确定与系统相关的漏洞。

它是由了解应用程序运行的操作环境和使用应用程序的用户的手动测试人员进行的。这些测试人员知道应用程序的总体目的以及单个功能的目的。

他们将这些知识应用到静态分析工具中，这些工具检查源代码、文档甚至是可执行文件，从而在不实际运行代码的情况下找到漏洞。

静态分析工具在目的和范围上有很大的不同，从代码样式强制到编译器级别的逻辑错误检查等等。

简单地说，静态代码分析帮助您维护安全的代码，而不必实际运行代码。

# 4.检查服务器访问控制

Web 应用程序有多个用户访问点，它们提供足够的访问来满足用户的请求，但是它们必须维护安全性以避免数据泄露或攻击。

测试人员如何检查服务器访问控制？

测试人员应确保应用程序的所有网络内和网络间接入点都是由预期的机器(IP)、应用程序和用户提供的，并且所有访问都受到严格控制。

为了验证开放的访问点是否受到足够的限制，测试人员应该尝试从具有不可信和可信 IP 地址的各种机器上访问这些点。

此外，应该批量执行各种实时事务，以检查应用程序在负载条件下的性能。

在手动进行安全测试时，测试人员还应该检查应用程序中开放的访问点是否允许用户以安全的方式进行特定的操作。

例如，测试人员可能会上传超过最大允许文件大小的文件，尝试上传受限文件类型，或者从受限站点下载数据，以检查应用程序是否允许此类操作。

检查服务器访问控制的目的是确保当用户能够使用应用程序时，应用程序不会受到潜在的攻击。

# 5.入口/出口/入口点

测试人员经常检查入口和出口网络点，以确保没有未经授权的网络可以向主机网络发送流量或信息，反之亦然。

什么是入口点和出口点？

入口流量由源自外部网络的所有网络流量和数据通信组成，这些流量和数据通信指向主机网络中的一个节点。另一方面，出口流量由源自网络内部并以外部网络为目标的所有流量组成。

可以通过手动安全测试方法轻松检查网络中的这些入口点，例如尝试将数据从受限网络发送到主机网络，并检查它是否允许流量和接受数据。

测试人员甚至可以将敏感数据或机密信息从主机网络发送到授权的外部网络，以检查出口点是否安全。

入口和出口过滤允许网络彼此交互，同时保持安全标准，并限制未经授权的网络共享敏感数据。

# 6.会话管理

当您手动进行安全测试时，您应该执行会话管理测试，以检查应用程序是否正确处理会话。

为了确保您的应用程序具有正确的会话管理，请检查特定空闲时间后的会话过期时间、登录和注销后的会话终止时间、最大生存期后的会话终止时间、检查会话持续时间和会话 cookie 范围等。

# 7.密码管理

在手动测试时，您可以使用的最有效的安全测试技术之一是密码管理。这是指用于发现密码和访问用户帐户或系统的各种方法。

如何测试密码管理？

如果 web 应用程序或系统没有实施严格的密码策略(例如，使用数字、特殊字符或密码短语)，就很容易暴力破解密码并访问帐户。

此外，不是以加密格式存储的密码更容易被窃取和直接使用。攻击者可以使用不同的方法来窃取存储在数据库中的信息，例如 SQL 注入。

即使密码以哈希格式存储，一旦被检索，也可以使用 Brutus、RainbowCrack 等密码破解工具或通过手动猜测用户名/密码组合来破解。

# 8.暴力攻击

另一种手动进行安全测试的方法是使用暴力攻击。

暴力攻击依靠猜测目标密码的不同组合，直到发现正确的密码。

攻击者使用暴力攻击来获取个人识别号、密码、口令或用户名等敏感信息，从而实施身份盗窃、将域重定向到包含恶意内容的站点或其他恶意活动。

应用程序安全测试人员也广泛使用这种方法来测试应用程序的安全性，更具体地说，就是评估应用程序的加密强度。

例如，测试人员应该尝试使用无效密码登录帐户，理想情况下，系统应该在有限次数的多次登录尝试失败后阻止用户。

此外，如果登录尝试是从未知设备或可疑网络进行的，应用程序应该要求进行多因素身份验证，这可能包括发送到用户已验证的电子邮件地址或联系号码的一次性密码，或者用户设置的安全问题。

# 9.SQL 注入(SQLi)

SQL 注入是一种代码注入技术，用于将恶意 SQL 语句注入到应用程序中，以修改或提取存储在数据库中的数据。

这是最危险、最频繁、最古老的 web 应用程序漏洞之一。它会影响任何使用 SQL 数据库的 web 应用程序，如 Oracle、SQL Server、MySQL 或其他。

如何防止 SQL 注入攻击？

手动测试人员检查 SQL 注入入口点，以确定它是否会被 SQL 注入攻击利用。他们通过接受某些用户输入来识别和测试在数据库上执行直接 MySQL 查询的数据库代码。

例如，应用程序应该能够在输入字段中接受单引号(')。但是如果应用程序向测试人员抛出一个数据库错误，这意味着用户输入已经被插入到数据库的某个查询中，并且已经被执行。

浏览器上显示的 SQL 查询错误消息可能会导致攻击者使整个应用程序崩溃，或者帮助他们提取用户名、密码、信用卡号等数据。

# 10.跨站点脚本(XSS)

除了 SQL 注入攻击，测试人员还在手动安全测试中检查 web 应用程序的跨站点脚本(即 XSS)。这是一种客户端注入攻击，攻击者的目标是在受害者的浏览器中执行恶意脚本。

这些恶意脚本可以执行各种功能，例如向攻击者发送受害者的登录凭据或会话令牌、记录他们的击键或代表受害者执行任意操作。

在手动测试期间，测试人员必须确保输入字段不信任未经验证的用户输入，并且如果这些字段的输出包含在服务器响应中，则必须对它们进行正确的编码。

此外，保护应用程序免受 XSS 注入攻击的主要方法是应用适当的输入和输出编码。

# 11.URL 操作

URL 操作是攻击者利用应用程序的另一种技术。它是攻击者出于恶意目的修改统一资源定位器(URL)参数的过程。

如何保护您的应用程序免受 URL 操纵？

手动测试人员应该验证应用程序是否允许在查询字符串中包含敏感信息。当应用程序使用 HTTP GET 方法在服务器和客户端之间传输信息时，就会发生这些类型的攻击。

当向应用程序提供基于 URL 的输入时，它通过查询字符串中的参数传递该信息。测试人员可以改变查询字符串中的参数值，以验证服务器是否接受该值。

用户信息通过 HTTP GET 请求传递给服务器，以获取数据或发出请求。如果测试人员能够操纵通过 GET 请求传递给服务器的输入变量，他们就可以访问未经授权的信息。

# 12.指定高风险功能

企业每天都要处理大量数据。有数以千计的业务功能需要文件上传/下载、向员工授予用户访问权限、与第三方承包商共享数据以及许多其他可能存在潜在漏洞的活动。

您需要识别高风险功能，以确保为特定活动实施更好的安全措施，例如限制不需要的或恶意的文件上传/下载。

如果您的应用程序处理任何敏感数据，您应该手动检查应用程序的注入漏洞、密码猜测、缓冲区溢出、不安全的加密存储等。

# 使用这些方法手动进行安全性测试

虽然自动化安全测试有很多好处，但它不足以确保应用程序完全安全。

企业必须进行手动安全测试，以确保应用程序中没有可能被攻击者利用的潜在弱点或漏洞。

通过手动进行适当的安全测试，公司可以检测到业务缺陷和注入漏洞，这些缺陷和漏洞在自动安全测试中可能不明显。

准备好开始了吗？在手动进行安全测试时，您可以使用上面有效的手动安全测试技术。

**关于作者:**

Steve Kosten 是 Cypress Data Defense 的首席安全顾问，也是 Java/JEE 的 SANS DEV541 安全编码:开发可防御应用程序课程的讲师。