# 建立一个基于预算新闻的算法交易者？那么你需要难以找到的数据——第 2 部分

> 原文：<https://towardsdatascience.com/building-a-budget-news-based-algorithmic-trader-well-then-you-need-hard-to-find-data-part-2-2ddc4a9be1d8?source=collection_archive---------38----------------------->

## 我的故事——零美元建立一个算法交易者，分析免费的 API、数据集和网页抓取器。第 2 部分:数据集和 Web 抓取器

![](img/0a2b3aa0ec7f0bd78dc91511cc590794.png)

斯蒂芬·道森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

为基于新闻的交易者寻找数据是一项非常具有挑战性的任务。获取一年多以前的历史数据要么是一项艰巨的挑战，要么将花费数百到数千美元购买。在第 1 部分中，我分析了访问数据的最佳新闻 API。如果你还没有读过那篇文章，我推荐你先读读[这里](/building-a-budget-news-based-algorithmic-trader-well-then-you-need-hard-to-find-data-f7b4d6f3bb2)。总结一下我发现的免费 API 的结果，它们在为交易者提供实时新闻方面非常出色，但在为用户提供积压的数据方面却非常欠缺。事实上，我找不到一年前的数据。它们还限制了用户在任何一个月中可以发出的请求数量。幸运的是，我们可以采取措施减轻 API 的缺点。在这篇文章中，我将分析免费的数据集和网页抓取工具，看看它们如何为创建算法交易者提供必要的数据。

# 数据集

数据集是快速访问海量数据的首选。如果有正确的数据可用，由于能够快速下载和使用大量数据，数据集在算法开发时间上提供了无价的加速。我从[谷歌的数据集服务](https://datasetsearch.research.google.com/)到 [Kaggle](https://www.kaggle.com/datasets?utm_medium=paid&utm_source=google.com+search&utm_campaign=datasets&gclid=Cj0KCQjwhtT1BRCiARIsAGlY51L-jUWyCaU_xslZe9JAunbe0JApcmzjoQvcI_BRRQb2Bniu52mss2gaApItEALw_wcB) 搜索了几十个数据库档案。令人惊讶的是，能够提供真正有用的数据集的唯一来源是 Kaggle，他们实际上有多个！

## 优点:

大量信息-可用的信息越多，学习和发现趋势就越容易，这就是经典数据集从未过时的原因！

快速编译—当数据集被下载时，访问、训练和使用数据集的速度非常快，从而缩短了开发时间。

## 缺点:

难以更新-更新不是由您创建的数据集是一项具有挑战性的任务，即使如此，您也可能会遇到拼接不完全匹配的源的问题。您可能会受数据集创建者的支配，发布新版本，或者可能只能永久访问旧数据，这都是经典数据集的显著缺点。

很难找到-找到新闻 API 比找到新闻数据集容易得多。即使您找到了数据集，也不太可能找到与您试图解决的问题完全匹配的数据集。这可能使使用数据集成为不可能的选择。

## [Kaggle 美国财经新闻文章](https://www.kaggle.com/jeet2016/us-financial-news-articles#blogs_0000002.json)

该数据集包含 2018 年 1 月至 5 月彭博、美国消费者新闻与商业频道、路透社、华尔街日报和财富杂志的文章。数据集的总大小超过 1 千兆字节，包含成千上万的文章和元数据。

## 优点:

充足的数据——1gb 是迄今为止我发现的最大的数据集。这意味着，无论你只想要特定的股票还是一般的新闻，任何用户都可以从这个数据集中提取他们需要的信息。它还有大量的元数据，包括文章是关于什么实体的，以及对该实体的看法。

可靠数据-数据集仅包含可靠的来源，提供可靠的新闻报道作为算法的基础。

## 缺点:

时间跨度短— 5 个月的数据是一个小样本。这段时间市场稳定，表现良好，这可能会导致不可靠的学习。

杂乱的数据——数据按文章排序，而日期和相关的实体存放在元数据中。这意味着在该数据集可用之前，可能需要大量的数据争论。

## 总体而言:

这个数据集是数据收集的一个很好的起点。它有一个明显的缺点，即缺乏一个大的时间跨度，但如果你以此为起点，并填写 2018 年 5 月以来的补充数据，这个数据集可能会被证明是有价值的！

## [消息对股票收盘价的影响](https://www.kaggle.com/BidecInnovations/stock-price-and-news-realted-to-it#MicrosoftNewsStock.csv)

这个数据集非常轻量级，但却是这个列表中最有趣的数据集。它只包括微软和苹果公司从 2006 年到 2016 年的文章。每个日期包含开盘价和收盘价，以及《纽约时报》与该公司相关的所有标题。数据集包含对组合标题串的情感分析，指示是否检测到正面或负面情感。

## 优点:

长时间跨度——10 年的标题数据足以用来训练、测试和验证算法，并且可以通过在类似的方法中添加额外的数据来进一步改进。

补充信息-内置的股票价格和情绪分析列使这成为一个数据集训练准备！像自然语言处理这样的附加步骤已经为您完成了！

可靠的数据——数据直接来自《纽约时报》,虽然这不是一个多样化的数据来源，但它是一个可靠和一致的来源。

## 缺点:

只有 2 个报价器——从 2 个报价器中学习并推断出其他股票是危险的。这是一个耻辱，这个数据集不包含来自不同部门的 20+ticker！苹果和微软也是成功的公司，这可能会引入不必要的幸存者偏见。

数据越来越旧——只有 2016 年的数据可能会伤害到现在想要创建一个交易算法的人。这可能需要对丢失的信息进行大量的填充才能使用。

缺少元数据—提供的信息只是标题字符串。这缺乏可以证明有用的深度元数据和文章内容。

## 总体而言:

这个数据集对于学习如何建立一个算法交易者非常有用。它提供了大量的数据，并提供额外的分析。如果您想获取数据集并开始训练，没有比这更好的选择了！然而，我会谨慎地把它作为你唯一的数据源。尤其是如果你想建立一个全面的算法。旧数据的缺点和没有太多的信息阻碍了原本是一个伟大的数据集。

## [Kaggle 每日新闻进行股市预测](https://www.kaggle.com/aaron7sun/stocknews#Combined_News_DJIA.csv)

该数据集包含从 2008 年到 2016 年每天从 Reddit 的世界新闻论坛检索到的前 25 条世界新闻。它还包含道琼斯工业平均指数数据和一个布尔值，如果当天道琼斯指数收盘时较低，则为 0，如果收盘时较高，则为 1。

## 优点:

时间跨度长— 8 年以上，每天有 25 个标题，这足以用来训练、测试和验证算法，并且可以通过在类似的方法中添加额外的数据来进一步改进。

制作良好-数据集组织良好，可用于算法开发。数据集是由一位教授制作的，用于深度学习课程，因此它自然易于使用。

## 缺点:

数据有效性——根据用户投票赞成和投票反对的内容提取标题可能会给算法带来偏差。Reddit 也没有审查被投票支持的新闻来源的有效性。

数据越来越旧——只有 2016 年的数据可能会伤害到现在想要创建一个交易算法的人。这可能需要大量的回填信息才可用。

不具体—数据仅来自世界新闻，而非金融新闻或个别符号，因此无法提取具体的金融文章。

## 总体而言:

这是三个数据集中最全面的。它提供了充足的数据、很大的时间跨度，并为用户提供了轻松添加数据、使用 NLP 等技术扩充数据或使用数据快速开发算法的机会。然而，这种便利和大量免费数据带来了数据可靠性的缺点。

# 数据集的总体印象

所有这些数据集以令人难以置信的速度提供了大量的免费数据。然而，这些数据集没有一个是完美的。它们都有各自的缺点，可能会限制它们的实用性，并且都是 2018 年或更早的产品。然而，数据集的好处是，它们为向免费 API 或 web scraper 添加一些历史背景提供了一个很好的起点！

# Web 刮刀

Web scrapers 涉及创建一个程序，该程序将从源站点系统地提取数据，并保存这些数据以备后用。它们是许多人的最爱，因为它们可以自由创建，并且完全可定制。在这篇文章中，我将介绍 web 抓取工具的两种方法！

## 优点:

完全可定制—您正在编写提取数据的代码，因此您正在完全按照您想要的方式存储您想要的数据。

无限制的免费访问——只要你允许，你的机器人就会运行，没有付费墙，或者对你接收的数据没有限制。

## 缺点:

可能会很慢—因为您是以编程方式访问网站，所以收集大量数据比使用 API 慢得多。

受限于网站——你也受限于在你抓取的网站上物理可见和可访问的内容，这可能意味着回到很久以前(比如获取几年前的推文)可能在编程上具有挑战性。

高开发成本——创建 web scraper 比使用 API 或下载数据集更具挑战性，耗时也更长。

## [硒](https://www.selenium.dev/)

Selenium 是一个大多数编程语言都支持的工具包，用于使用脚本编程控制 web 浏览器。它广受欢迎，受到广泛支持，易于使用，目前被数百家公司用于 web 抓取、自动化和系统测试。

## 优点:

广泛的支持——借助对 Python、Java、Ruby、Javascript 和 C#的开发支持，使用您最喜欢的语言并开始自动化 web 浏览器变得非常容易！

完全可定制—您可以完全控制 web 浏览器。您可以在浏览器中做的任何事情都可以自动化，保存，并用于以编程方式存储数据！

## 缺点:

高开发成本——创建您的完美刮刀需要时间，此外，网站始终有可能发生变化，需要维护。

耗时——与利用 API 等其他来源相比，等待 scraper 收集足够的数据来创建任何有用的算法可能会令人望而却步。

## 总体而言:

硒真正是“你想要吗？建吧！”网页抓取选项。这是一个非常扩展和有用的工具，唯一的缺点是你只能通过浏览器来完成。如果您需要特定的数据，并且具有创建自己的解决方案的编程能力，没有比 selenium 更好的平台了。

## [Getdata.io](https://getdata.io/docs/semantic-query-language/quick-start)

getdata.io 提供了一个有趣且可能更快的网络抓取解决方案。该平台允许使用其查询语言创建“食谱”，该语言将在网页变化时系统地从网页中抓取数据。然而，最重要的是，你不需要精通他们的查询语言，因为他们有一个 chrome 扩展，可以作为一个点击式的解决方案来生成食谱！与为执行任何基于 web 的任务而构建的 selenium 不同，它是为收集数据而定制和构建的！

## 优点:

快速学习-使用 getdata.io 时，开始抓取网页所需的时间不会太长。添加的 chrome 扩展使抓取数据变得简单！

专为提取数据而构建—该平台专为检测数据变化并相应更新而构建。然后，您可以使用 get 请求将任何数据拉入您的算法中！

数据社区——您创建的配方和提取的数据可以公开。这意味着你得到了一个已经在收集数据的巨大的社区！然而，我为金融新闻找到的食谱太弱，不足以报道。

## 缺点:

缺少历史提要——因为 scraper 只寻找变化，它不擅长向后搜索历史数据，这意味着您需要等待足够的数据！

比硒更有限——配方创建系统虽然简化了过程，但也限制了可以提取的内容的能力。复杂的提取可能更困难，从长远来看，这可能会使硒更容易提取。

## 总体而言:

对于那些想要简单了解网络抓取和轻松访问定制数据的人来说，这是一个很有吸引力的选择。它在深度上的不足在数据社区和快速启动时间上得到了充分的弥补！

# 卷筒纸刮刀的总体印象

Web scrapers 为需要创建自己的数据的人提供了最佳选择。虽然他们可能需要更长的时间来收集必要的数据，但可定制性的数量是无与伦比的。Web 抓取可以用来扩充现有的数据集或 API，也可以单独使用来获得巨大的成功。总的来说，你在 web scraper 上投入的工作量将决定它能否成功创建完美的数据集！

你有它！如果你跟着我看了这两部分，我希望我已经提供了一个很好的资源，告诉你从哪里开始寻找算法交易的新闻。我对创建免费数据集的总体建议是

1.  不要害怕混合来源。只要你试图保持一致性，数据集和 APIs 刮刀就能很好地协同工作。
2.  使用适合您的用例的资源。这些资源都不完美，但它们都是有原因的。这 10 个项目中的每一个都提供了至少一个其他 9 个项目没有涵盖的独特方面！
3.  用自己的钱交易要小心！

如果您有我错过的最喜欢的 API、数据集或 web scraper，请告诉我，如果您喜欢这篇文章，请关注我，了解更多数据科学领域的内容！