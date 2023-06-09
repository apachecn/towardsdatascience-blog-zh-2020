# 市场分笔成交点-数据回放

> 原文：<https://towardsdatascience.com/market-tick-data-replay-9719866eb64c?source=collection_archive---------38----------------------->

## 一个只有 100 行代码的市场数据回放工具。

![](img/92b1d5e2ef22e8dce69db15925cbe3be.png)

Wolfpack Flow 是我正在开发的用于操作订单流的最新工具。来源:www.wolfpackflow.com

在过去的几个月里，我一直在研究一个可视化和分析分笔成交点数据的解决方案。虽然该工具的第一个版本开发得非常快，但它被证明存在一些延迟问题，图形部分也很好，但缺乏现代标准，如平滑滚动，这需要适当的硬件加速使用。

带着比自然技能更多的承诺和决心，我一直在开发一个新的改进版本，它被证明比我最初预期的更复杂和更具挑战性，但同时也增加了只有专业工具才有的功能。

在开发过程中，当市场关闭时，我面临着没有市场数据的问题，这在某种程度上限制了开发时间，尤其是在周末或 CME 清算时间工作是一种负担(尽管我不提倡在周末工作)。

为了克服这个问题，我开发了一个小型市场数据回放工具，事实证明这是一个非常简单的工具，可以在不到一个小时的时间内实现。这个简单的工具允许:

1.  用一致的和可复制的数据集测试你的软件，
2.  简化调试，因为您总是处理相同的数据包、时间戳等。这看起来是一个小好处，但在处理低级软件处理字节和时间戳时却不是。
3.  将开发与市场数据馈送 API 分离。
4.  将开发时间与市场时间分离。
5.  出于训练目的复制过去的市场条件——可能需要更复杂的代码，但基础已经在这里了。

要做到这一点，你只需要 3 个步骤和大约 100 行代码。

# 1.获取数据

在我的例子中，我在数据馈送 API 提供者和我正在开发的工具之间开发了一个定制的中间网络接口。这允许将与数据供应商和应用程序相关的逻辑解耦。我这样做是因为:

1.  更改数据馈送提供者更容易，因为您只需要专注于更改与市场数据 API 交互的代码。
2.  该软件可以位于不同的服务器上，因为我们使用 UDP 套接字来与两个软件模块进行通信。
3.  任何与市场数据馈送 API 代码相关联的潜在软件许可问题都通过使用中间的中性网络协议而被绕过(尽管这将产生激烈的争论)。

为了捕获数据，可以使用 *tcpdump* 或 *Wireshark* 等工具*。*尽管作为开源软件出身卑微，但它们是可以可靠使用的专业工具。 *Wireshark* 其实诞生于一个小电信运营商。它们甚至在第一层电信级电信环境中被广泛使用，并且已经成为非常成功的专业网络监控和审计解决方案的核心。对于更严重的应用，可以编写一个定制的数据包分析器，并作为插件集成到 Wireshark*中。*

![](img/72ce9c2a750ef914927fb4a0ab342285.png)

Wireshark 允许捕获任何网络协议。

这使我们能够从数据中生成输出。在我的例子中，为了简单起见，我只使用了 Wireshark 的文本格式，它会生成一个相当长的文件。

![](img/b3b768b71cc93c66d7518c7bb442fc15.png)

从 Wireshark 捕获的文件可以导出为多种格式，包括纯 ASCII 文本。

# 2.解析数据

这样一个冗长的文件(它为每个包创建了 14 行文本)肯定是不需要的，也不适合提供给重放工具。

一点经典的 UNIX 足以将这个文件转换成更合适的文件。假设有两个字段的 CSV。我不太喜欢 CSV，因为使用固定宽度的字段更有效，但这次我在寻找最简单的选项。

![](img/ad9e1c26252985c6fb9c75a30eb1ab9c.png)

“数据工程”是这个行业中最不吸引人的部分，包括许多像这样的步骤。

现在数据是一种易于阅读的格式，可以输入任何软件。请注意，解析是用我正在使用的特定协议完成的，但是它可以用于任何协议，因为该工具是不知道数据包大小的。

# 3.开发你的重放工具

快速开发对我来说意味着 Java，所以我用 Java 编写了这个小工具(对其他人来说意味着其他语言)。它基本上分为两类:

1.  market file reader—读取解析的文件并遍历每一行(数据包)，处理延迟并提交数据包。
2.  PacketSender —打开 UDP 套接字并提供传递 UDP 数据包的方法。

源代码如下:

如您所见，代码非常简单和基本。实现这样一个小工具一点也不困难，甚至比学习一个现有的工具还要快。

# 摘要

市场数据回放不是一个常见的功能，但它在交易中有一些优势，不仅在开发方面，而且在自主交易的培训方面。能够复制市场数据馈送是测试整个数据管道的最佳方式，它使开发能够处理小的市场数据样本，而无需配置实际的实时市场数据馈送。