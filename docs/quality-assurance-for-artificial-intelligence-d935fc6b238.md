# 人工智能的质量保证

> 原文：<https://towardsdatascience.com/quality-assurance-for-artificial-intelligence-d935fc6b238?source=collection_archive---------23----------------------->

## 数据的一般思想和质量保证

这是我关于如何测试利用机器学习的系统系列的第一篇文章。

# **关于人工智能如何工作你需要知道的事情**

下面介绍一个例子 AI 项目来解释相关术语(数据科学的人可以跳过)。想象你经营一家面包店。所以你想知道每天早上要烤多少面包。为此，您可以使用以前收集的历史数据，例如:

![](img/88b75e6ae67ec24735de58f203d8c68c.png)

仅通过日期进行预测几乎是不可行的，但是您注意到您的需求取决于:

*   天气条件(在寒冷或下雨的天气，很少有人出去购物)
*   月(在夏天，您的客户去度假)
*   一周中的某一天(因为周日不营业，所以人们会在前后购买更多商品)
*   附近的一些事件(想象你的面包店靠近一个足球场)

因此，您添加了包含每天值的列。您将预测的列称为“**目标**，将用于预测的列称为“**特征**”。

![](img/e33c782a7d7a7eba92d08218513adfbd.png)

# **问题**

所以你把你的数据交给一个自称为数据科学家的人，让他们创造一些预测需求的东西——数据科学家称之为“**模型**”。你可以把一个模型想象成一棵决策树，它将由一个算法使用你的数据来创建。在模型交付后，你需要知道你是否可以信任它(盲目地)并在日常工作中使用预测。

为了回答这个问题，我们将重点放在方法部分，并将模型本身视为一个黑盒。这应该给 QA、经理、开发者和基础设施人员提供指导，他们需要确保使用人工智能的软件的质量。我确信，如果你学习了人工智能模型是如何开发的剧本，那么对质量保证和常识的理解是足够的先决条件。你不需要额外上数学、统计或深度学习的课。

我还想为数据科学家提供想法和最佳实践，因为他们通常必须自己确保数据和模型的质量。特别是如果你的经验主要来自于 ML 课程、研究或 Kaggle 挑战，它们只涵盖了模型生命周期的一部分，你可能会对在这个行业工作时需要的其他 QA 技术感兴趣。

# **AI 模型生命周期**

从生命周期的角度来看，人工智能项目通常包括 3 个阶段:

*   收集和准备数据
*   训练模型
*   在生产中部署模型以进行预测、监控模型

因此，QA 根据阶段执行不同的检查或审查:

*   将用于模型训练的数据质量是否足够好？这就是这篇博文的主题。
*   投入使用的构建模型是否具有足够的质量？这将是下一篇文章的主题。
*   在生产中运行时，模型是否能保持足够的质量？我会在这个系列的[最后一篇](https://medium.com/@perlinmi/quality-assurance-for-artificial-intelligence-part-3-b90392789058)中处理这个问题。

一些 QA 步骤归结为将数据或模型的指标与预定义的值或阈值进行比较的检查。其他的则是分析或评论，需要时间、体力、领域知识和常识。

# **关于自动化**

一旦您的模型上线，即使方法和工具保持不变，您也不需要重新培训它的可能性接近于零。除了技术变化和新的需求，还有一些人工智能特有的原因:

*   以后你很可能会获得更多或者更高质量的数据。由于数据量和质量是你在人工智能中的主要优势，你不会错过这个机会。
*   如果你的挑战是关于预测，你需要今天/本周/本月的数据来预测明天/下周/下个月的事情。所以你需要用最近的数据重新训练模型。
*   随着时间的推移，世界在变化，随着时间的推移，你的模型曾经很好地反映了现实。想想估计房价和不断变化的房地产市场。
*   您的系统的用户很可能会发现您的模型做出错误决策的条件。尤其是如果你的系统值得欺骗(比如保险索赔的自动处理)，期待坏人会尝试它。所以你需要调整你的模型来消除或者至少减少这种影响。

模型更新的频率取决于用例，可能从几小时到几年不等。这个频率对从原始数据到新的生产阶段模型的流程的自动化水平有很大的影响。您可以用不同的方式实现这种自动化，这是一个单独的主题，不在这里考虑。但是，在任何情况下，你必须为 QA 检查提供**相同级别的自动化**。这样，您就使 QA 成为模型开发过程中不可避免的一步。

假设您有一个每夜运行的脚本流，它从不同来源收集数据，开始模型训练，用新模型构建服务，并替换旧版本的服务。在这种情况下，对数据和模型质量的检查必须是作为您的流程的一部分运行的脚本，如果没有满足定义的条件，就会发出红色标记。

# **检测数据收集错误**

在极少数情况下，如我们的小面包店，模型中使用的所有数据可能来自同一个来源。对于至少是中等规模的公司来说，用于预测的数据可能分布在多个系统中。在一个普通的电子商务公司中，CRM 知道客户的人口统计数据，支付系统知道他们的购买行为，web 跟踪系统知道他们搜索什么，库存系统知道你提供的产品，此外，你想使用外部服务的天气数据。因此，在数据科学触及数据之前，大部分数据都经历了一个非同寻常的多步过程。无论这条路径涉及手动操作还是使用 ETL 工具完全自动化，都可能出错。并且源系统也可能包含错误。所以在训练模型之前，我们需要一套“入口检查”。

让我们假设数据收集运行已经完成(我们认为它是一个黑盒，将细节留给数据工程师)，并且您有一个新更新的客户表或一个包含图像的文件夹。

最简单的检查类型是基于统计的。一旦实施了数据收集过程，手动验证最终结果的正确性，即通过跟踪源和目标系统中选定的条目(如果您的数据工程同事已经这样做了，那么您很幸运)。一旦验证了这一点，就要计算对模型训练很重要的实体(帐户、图像、客户评论、音频文件)。引入阈值，确定必须有多少个阈值可用，以假设数据收集工作正常，没有重大错误。

考虑计算进一步的统计数据，从长远来看，这些数据应该不会发生重大变化:您的帐户如何按性别分布，平均审查长度是多少，最常见的图像类型是什么，等等。对于每个统计数据，定义一个阈值或范围，该阈值或范围将在模型训练之前进行验证。

您可能想知道有多少记录(至少是一个数量级)足以训练一个足够好的模型。仅仅从问题描述和数据中很难得到这个数字。先来判断训练后模型的准确性；我们将在下一篇博文中解决这个问题。

# **检测数据质量问题**

下一步，想想你是否真的想在你的模型中使用所有可用的记录。在训练模型之前，您最有可能修复或删除的条目有:

*   复制
*   为测试创建的条目
*   无意中输入了错误日期的条目(如出生年份 1897，而不是 1987)
*   覆盖您的模型不应该服务的用例的条目(比如公司帐户，如果您想要一个仅用于个人帐户的模型)

进行一些探索性的数据分析。对于模型中使用的每个列/特征，您应该知道它的确切含义以及它可以取什么值。也许会有一份文档，也许是最新的。但是不要假设一切都是正确的，并且与文档保持一致。

对于像“年龄”这样的数字列，构建一个直方图。对于像“教育”这样的分类列，列出所有可能的值。要发现重复项，请检查技术键的唯一性，也可以检查一些功能集的唯一性(如客户的姓名和地址)。

另一种更高级的发现奇怪记录的方法是“异常检测”想象一个 21 岁的客户，拥有博士学位和 10 年的工作经验。这 3 个数据点本身都很好，但它们的组合是不太可能的；我们可以假设有人进入了错误的年龄。像这样发现异常是一个纯粹的机器学习主题，有很多关于它的伟大论文。

# **寻找解释**

如果您的数据环境足够陈旧，您可能会发现许多问题。对他们中的一些人来说，解释会很容易找到或者显而易见——但很可能不是对所有的问题。很多类似“带有这个日期的记录看起来很奇怪，我应该修复它还是过滤掉它还是保持原样？”我知道的唯一方法就是从你的椅子上站起来，去问一些问题。好的候选人是:

*   处理边缘案例的同事:客户支持、运营
*   非常了解系统使用方法的同事:客户支持(再次)，QA
*   刚进公司不久的同事

# **修复数据质量问题**

我们只是简单地触及这个主题，因为它主要是关于数据科学，而不是关于 QA。一旦发现问题，考虑从源头上解决它——重复的用户记录应该直接在 CRM 中修复，错误的支付汇总必须在 ETL 部分修复。但是您仍然应该假设上游系统有数据问题(一个将被修复，但另一个将通过实现一个新特性而出现)，并对它们进行检查和/或修复。

如果问题有一个解释，但不可修复(在短期内)，这是常见的情况，您应该修复它，以防止错误数据对模型的影响。修复通常是关于

*   过滤记录:例如，您可以通过 ID 删除重复的记录
*   从另一个来源丰富缺失的数据点:例如，缺失的性别可以通过在字典中查找名字来猜测
*   输入缺失数据点:即，如果年龄缺失，则使用数据集的中值年龄

在任何情况下，清理每个数据问题并不是继续进行的强制要求；您的数据子集也可以用于训练。因此，首先解决以下问题:( 1)关于重要特性;( 2)经常出现;( 3)容易解决——然后训练你的候选模型。如果它不能表现出足够的质量，你可以追求更难的问题。

# **接下来是什么**

现在，我们已经完成了数据集的 QA，可以继续构建模型了。模型的 QA 将是我们下一篇文章[的主题。](https://medium.com/@perlinmi/quality-assurance-for-artificial-intelligence-part-2-d20e0ef9791e)

![](img/f253f3717da1c354f53afda0dc882c81.png)

图片来自[生物多样性遗产图书馆](https://www.flickr.com/photos/biodivlibrary/albums/page1)