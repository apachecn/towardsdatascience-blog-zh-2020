# 使用机器学习和 Strava 智能运行

> 原文：<https://towardsdatascience.com/running-smart-with-machine-learning-and-strava-9ba186decde0?source=collection_archive---------19----------------------->

## 基于你和其他运动员的体育观察数据，你的最大潜在训练收获的有序列表。

# 聪明跑步？

作为一名跑步者，我总是希望提高我的个人最好成绩，我经常想，如何优化我跑步的时间，以获得最好的成绩，同时尽可能地懒惰。有时候我一周跑七次，但是几个月都没有提高速度。其他时候，在几周的徒步旅行、饮酒和每周只跑一两次之后，我跑得非常好。这违背了经营论坛和培训计划的智慧。幸运的是，我已经在 Strava 上记录了五年多的训练，许多人也是如此。这些数据中一定有某种模式。

所以我建立了一个服务，在其他运动员允许的情况下，从运动员的社交网络 Strava 获取数据。机器学习算法从所有运动员的数据中确定哪些因素对改善他们的跑步最重要。通过这种算法，有可能给运动员一个有序的训练改进列表，他们可以进行这些改进以获得更快的速度。

# 这篇文章很长。

这个问题不容易解决，解决方案也不容易解释，简而言之，因为跑步教练和机器学习工程师之间的重叠可能相当小。出于这个原因，我在顶部放了一个总结部分，并让每个技术部分对于那些研究细节的人来说都是相当独立的。我解释了整个过程，从开始到结束，包括生产“产品”

# 摘要

从多个跑步者那里获得数据后，我建立了两个模型:

*   一个模型，可以预测，高达 89%的准确性(R)，什么时候运动员将运行在一场比赛(5k 至 42k)完全基于他们的训练计划。换句话说，根本不用他们的步速数据来确定他们的步速。这个模型并不总是对普通跑步者有用，因为在你的速度和你跑的频率或距离之间有很多关联。当与模型比较时，普通运动员可以看到他们相对于顶级运动员是如何训练的，但看不到如何到达那里。
*   一个模型，它可以预测运动员根据他们的训练计划将会提高多少。这个模型对跑步者更有用，因为它可以告诉普通跑步者怎样做才能跑得更好。然而，我觉得我需要更多的训练数据来达到可接受的 70%。

整个系统现在可以在[的一个简单网站](http://howeffectiveismyrunningplan.appspot.com/)中获得【更新:我已经关闭了该网站，因为该系统很快就用完了我的主办预算】，运动员可以在那里注册并深入了解他们的训练计划。

第一个模型的系统输出的原型可视化如下所示。这里，蓝色标记显示了运动员相对于前 10%和后 10%运动员的训练情况。该列表是按照运动员训练中最重要的因素排序的，是每个因素的重要性和运动员在其中的缺点的产物。

在这里，很明显，运动员需要每周跑更多次，跑更多的距离。在此过程中，他们应该花更多的时间在心率 2 区。然而，有一些事情他们做得很好，甚至相对于最好的运动员。例如，在他们跑步前的三个月，他们减少了花在非跑步活动上的时间，因为他们更专注于跑步，并且他们增加了长跑的比例。

![](img/8db5d2ef6697d23514ea1a1f15a1800d.png)

# 深入！

从现在开始，事情变得更加技术性:

# 为问题设定一些界限

*   Strava API 不会返回他们拥有的所有数据(细粒度的心率数据)或见解。返回的数据是每公里的平均值，这意味着人们无法看到在几分钟内均匀分布的因素。例如，由于非常短的短跑训练计划导致的心率或节奏的峰值不能被考虑。
*   这种分析着眼于“宏观”的训练计划——你在长期训练中的表现。例如，你如何安排你的周数，增加距离，平均跑步的轻松程度。幸运的是，这是跑步者面临的最热门的问题之一。选择一个有效的培训计划很难。
*   有许多方法可以解决这个问题，导致许多模型和特征工程决策更多的是艺术而不是科学。例如，我选择只关注个人最佳成绩(PB)前三个月训练的因素。这个决定背后有一些科学依据，但选择两个月或六个月可能会更有效。其他类似的决定包括为相对于其他跑步的“长”跑或“快”跑设置阈值。
*   很多我想拥有的因素都不见了。这些模型永远不会完美，因为 Garmin 和 Strava 对他们的体重、饮食、压力和睡眠统计数据掌握得非常紧密。
*   类似地，这些模型平均来说表现不错，但是每个运动员的效果可能不同。一些运动员比其他人给模型添加更多的噪音。随着更多的数据，这种噪声将在模型中考虑。但当涉及到个性化的可视化时，建议会有所不同:例如，你可能是一个非常健康的人，训练非常完美，但需要减掉 10 公斤的上身肌肉才能改善。
*   同样，这个模型是为普通跑步者设计的。有了更大的数据集，我相信我可以在相似跑步者的子集上运行该模型，以便为跑步者提供更相关的建议，例如显示排名后 10%的跑步者，喜欢他们的人是如何改进的。

# 掌握技术——首先是一些跑步科学

我在这里解决的问题是长跑:5 公里到 42 公里之间。虽然这些仍然是非常不同的比赛，但动力是相似的，有一个公式和常数变量控制着运动员在这个范围内任何距离的速度之间的映射。假设我经常跑 25 公里到 30 公里的快速(速度或门槛)跑和长距离跑，从我的 5 公里时间推断出我的马拉松时间是相当简单的。这是通过传奇跑步教练杰克·丹尼尔开发的常数和公式[“vdot”来完成的。在我的整个模型中，假设 vdot 是您整体跑步健康状况的准确代表，我们处理的是 5-42 公里距离范围内的健康状况。](https://en.wikipedia.org/wiki/Jack_Daniels_(coach))

然而，vdot 并不是健身的完美同义词，与其说它是速度的度量。对于健康的整体测量，人们必须考虑 OBLA、V02max、肌肉效率和肌肉功率输出与足部划水持续时间的关系。我们无法用腕表数据测量那些。但是我们可以衡量是什么帮助人们提高最终目标——速度。

大多数跑步者使用运动员社交网络 Strava 来上传他们的数据，这也是我获取数据的地方。Strava 确实在他们自己的模型中估计你的适合度(vdot 或他们自己的度量)，但并不通过他们的 API 提供这一点。出于这个原因，我建立的模型只能在你跑个人最好成绩(PB)时推断你的健康状况，Strava 确实将它作为“估计的最佳努力”提供有可用的选项，例如根据心率和速度之间的关系来估计健身，但这将在最小可行产品(MVP)的模型中添加太多噪声。

![](img/f5b53bb21c07befa23a599e2346fb084.png)

我最大的努力

为了达到这些最佳效果，人们普遍认为，你必须在努力训练和恢复之间保持微妙的平衡，并通过大量轻松跑步来保持你的机器运转良好。前者由 trainingpeaks 所谓的[脉冲反应模型](https://www.trainingpeaks.com/blog/the-science-of-the-performance-manager/)定义——你让你的身体处于压力之下，它通过变得更强来回应这种压力。后者只是因为[科学表明，我们的身体在有氧心率区](https://www.frontiersin.org/articles/10.3389/fphys.2015.00295/full)获得最有效的表现，这对应于“区域 2”中相对轻松的跑步速度。

**这将我们带到心率区**:教练和运动员根据每位运动员的最大心率定义了一组区域或范围，为我们提供了基于心率数据进行训练的目标区域，从而简化了我们的工作。这些区域从 Z1 到 Z5，从最小努力到最大努力。许多专业运动员完全按照心率范围进行训练，而不是按照速度，因为我们的心脏是我们身体对训练反应的最佳指标。下图给出了区域的指示。请注意，根据您的年龄来估计您的心率范围是一种相对糟糕的做法，因为这是根据遗传而不是健康状况来变化的。例如，[克里斯·弗鲁姆的最大心率是 161](https://www.theguardian.com/sport/2015/dec/04/team-sky-chris-froome-cycling) ，根据这个模型应该是 186。幸运的是，Strava 不做这种假设，而是随着时间的推移来确定这一点。

![](img/bdea76b750b425b65e002df1f4edda24.png)

心率区(维基共享)

我们可以在心率较高的区域花较少的时间训练，但在较高的区域花一点时间会受益匪浅。不同的教练有不同的看法，[一般的建议](https://www.runnersworld.com/uk/training/motivation/a27718661/what-is-80-20-running/)是花 80%的时间在“轻松”区 Z1-Z3，20%的时间在“困难”区 Z4 和 Z5。然而，这也有所不同，取决于你是在训练季节的早期，准备为一场比赛“达到顶峰”，还是为一场比赛“逐渐减少”你的努力。

为了管理你在这些区域的时间，并进一步简化训练，教练建议几种类型的跑步:

*   轻松跑步
*   长距离跑
*   间歇训练
*   节奏跑步
*   用大步跑或法特莱克跑轻松跑，快速冲刺而没有太多相应的心率增加
*   以上的任何组合。

如果这还不够，还有关于每周增加多少里程的科学，一个宏观类型的脉冲响应模型，在这里你的身体慢慢适应更多的努力，因此变得更健康。过度增加这一点的代价当然是受伤或倦怠。

# 简化的跑步科学

综上所述，对于每一个运动员来说，都存在着一个最佳的但又难以找到的训练平衡

*   每项活动的轻松和努力
*   跑步和休息，取决于你之前的活动
*   轻松跑、长跑、间歇训练、速度跑
*   跑步和交叉训练
*   每周增加你的努力

如果没有对自己或教练的深入了解，即使是经验丰富的跑步者，也很难找到这种平衡。有可用的工具，如 [TrainingPeaks 的性能管理器](https://www.trainingpeaks.com/blog/what-is-the-performance-management-chart/)和 Strava 的高级产品。他们很棒，尤其是他们告诉你，你训练太辛苦了，需要休息。然而，我发现他们都专注于试图估计你当前的训练负荷，因此依赖于大量[不准确的每日心率数据](https://www.google.com/search?q=heart+rate+data+inaccurate+garmin&oq=heart+rate+data+inaccurate+garmin)。我需要一些东西来建议我在几个月的时间里可以做哪些不同的事情，而不是每天都做。

所以，作为一名跑步者，我建立了这个分析作为一个辅助工具:告诉我在更长的几个月里，相对于其他运动员，我可以做些什么不同。

# 系统的高级概述

像这样的系统有几个部分，需要收集数据，训练模型，运行模型，并为前端用户提供见解。由于 API 访问或处理所需的时间，人们可以将它们视为如下交互的系统，绿色线条表示同步流，橙色线条表示异步流:

![](img/4070d3a067bf5797a5a86239dc9fb709.png)

# 获取数据:Strava API

Strava 对他们的 [API](https://developers.strava.com/) 的使用有很大的限制。没有运动员的允许，它不能被查询，然后被限制速度，每天只允许大约 10 个跑步者的数据被提取。这降低了数据采集的速度。

除此之外，Strava API 为每位运动员提供:

*   运动员的心率区——他们体验 Z1-Z5 的心率
*   一个活动列表，根据活动类型进行标记，包括跑步、自行车或运动员选择上传的任何内容
*   每次跑步的距离、心率、配速和“圈数”——通常以公里为单位
*   每圈的平均心率、配速和节奏
*   对于每一次运行，无论它是否是“最大努力”——换句话说，一个 PB

我的 20 个朋友非常友好地通过 Strava 向我提供了他们所有的数据。鉴于他们每个人的数据平均有 10 个 Pb，这为我的模型提供了近 200 个输入，足以建立一个精确的模型来估计 vdot，但不足以建立一个模型来估计 vdot 的改善，这是我稍后将解释的问题。

![](img/23ad9f49b6d29e62847a394984f11e17.png)

1.  遍历所有运动员活动，确定哪些是 PBs。对于每个 PB，如果它在前一个 PB 之后超过一个月，并且超过前一个记录 0.5 vdot，则成为一个数据点。这是为了确保每个数据点都是足够大的独立 PB。
2.  根据运动员的所有活动，构建一个回归变量，将该运动员在一个月的时间间隔内的步速映射到心率。这是因为许多运动员活动是在没有心率监测器的情况下进行的(一般来说，心率监测器只是在过去两三年才被广泛使用)。然而，用这个回归量仍然可以相当准确地估计心率，R 为 0.9。这在训练机器学习模型时非常有用:它将整个模型的 R 提高了 0.1。
3.  对于每个 PB，使用杰克·丹尼尔公式确定该 PB 的 vdot。这是第一个机器学习模型的“y”:模型被训练的特征。对于第二个模型，使用 vdot 的变化或 delta-y。同样对于每个 PB，提取 PB 之前 3 个月的所有活动。根据最终模型的 R 选择 3 个月。
4.  对于每个活动，提取有用的特征，例如活动的类型、长度、总体努力等。虽然我不会对模型特征进行太深入的讨论，但诸如心率的标准差之类的东西可用于确定活动是否是间歇训练，相对努力和活动的长度可用于确定它是一种节奏还是一次长跑。类似的逻辑也适用于加快步伐、爬山重复等。
5.  特别是在几年前的活动的情况下，步速数据用于推断活动的预期心率，以使得能够从心率中提取一些以上和以下特征。
6.  活动按周分组，这种方法我还是有点不舒服，因为有些运动员可能以 10 天或 14 天为周期进行训练。对于每周，提取更多的特征，例如每周里程、跑步和其他活动之间的分割以及跑步类型之间的比率。
7.  将周分组为训练块也是如此。在这里，整个三个月被考虑，并且特征更符合三个月中里程、努力和整体行为变化的相对增加。最后，比赛前的锥度也被分析为一个因素。

所有上述特征都存储在每个运动员的数据库中。都是用来训练最终的机器学习模型。需要注意的是，节奏不是一个特征，因为用它来预测是很愚蠢的..步伐。

# 机器学习模型

对于机器学习专家来说，这一部分将是相当乏味的。根据所选择的特性，性能最好的模型是决策树，紧随其后的是普通的 XGBoost。调整这些模型显示，相对于通过一些特征工程来改善数据，收益甚微，例如在没有心率数据的情况下，从心率外推心率。

直觉上，并且基于模型性能，问题是近似线性的。

正如本文前面提到的，该模型分为两部分:

*   一个模型是在 vdot 上训练的:确定解释运动员 vdot 的特征，本质上是马拉松配速。这在最好的情况下有 0.89 的 R，但是根据运动员的不同可以低至 0.6。
*   另一个模型，真正的金罐，在运动员最后一次 PB 之后，在 vdot 的变化上被训练。这更有价值，因为它不容易受到相关性和混杂因素的影响。然而，在这里，最好的情况 R 只有 0.5。

每个的特征(基于我的 n=200 的小数据集)如下。随着数据库的增长，我将对此进行更新:

# 解释 vdot(健身)的功能

在这里，我们有一个相当健康的 SHAP 情节。在一个简单的系统中，该图的健康状况通常由红点和蓝点之间的清晰分隔来表示。

*   所有功能都是针对 PB 之前的 3 个月培训期。
*   普通特征(常数)以 f_ 为前缀。例如，f_avg_weekly_run_distance 是运动员跑步的平均距离(km)。
*   相对特征(相对于这个运动员的其他数据)以 r_ 为前缀。例如，“r_proportion_yoga”是运动员在这三个月*相对于之前训练的剩余时间*做了多少瑜伽。

![](img/d6d16cefa923cf9039a78773a208b993.png)

请记住，这些特征被认为对非线性模型很重要:随机森林回归算法，所以我们不能把它作为跑步者的重要特征清单。我会对“r_proportion_yoga”这样的功能持保留态度。例如，该模型可能已经确定，如果运动员不做很多简单的跑步，那么他们花在做瑜伽上的时间就格外重要。但是由于这个模型的 R 相当好，并且考虑到我们有一个*几乎*的线性问题，以这种方式看特征是安全的，或者运行一个线性 XGBoost 特征分析。

关于跑步者在 PBs 前的表现，我们可以得出几个相当可靠的结论:

*   他们比跑得慢的人跑得多，总次数也多
*   他们在心率区 1、2、4 和 5 的时间较长，在心率区 3 的时间较短。换句话说，他们要么跑得很轻松，要么跑得很艰难。
*   他们和更多的运动员一起跑步(**r _ mean _ athlete _ count**)——这肯定是相关的，因为他们可能会在社交生活中关注自己的主要爱好
*   他们跑得更高了
*   …等等。

# 解释相对 vdot(适应性改善)的特征

作为一个快速的回顾，我没有看健康的运动员做了什么，而是训练了一个模型，这个模型是关于运动员通常做了什么来最大程度地提高 vdot。这可能是一个拥有足够数据的异常强大的分析，因为它会将相关性从等式中剔除。我们会看到普通人是如何变得更好的。

在这里，我们的 [SHAP 情节](https://github.com/slundberg/shap)并不健康。有许多对模型有很大影响的无关特性。

![](img/3905d00b4dd062362f17a849db09723f.png)

该模型的最佳 R 为 0.5。因此，就目前的数据集规模而言，即使对于最容易解释的运动员表现，它也只能解释 50%的提高速度的因素。

同样重要的是，该模型比预测纯 vdot 的模型更不线性。一些运动员可能因为是这项运动的新手而跑 PBs，因此该模型可能会决定“那些平均每周跑不到 30 公里的人需要比平时跑得更多才能达到他们的 PB，但那些每周跑超过 120 公里的人需要跑得相对更少但跑得更快。”然而，让我们来看一看有意选择的功能是什么:

*   快跑。很多。
*   骑自行车的次数相对比以前少了(我住在荷兰，数据集中的许多运动员也住在荷兰，所以当我们终于在我们热爱的夏天停止骑自行车，专注于跑步时，我们变得更快了)
*   **f _ slope _ time _ before _ taper**:这是在运动员开始减量之前，锻炼时间“增加”的指示。它被认为是重要的，要么增加很多(对一些运动员来说)，要么减少一点负荷(更多运动员)
*   **f _ slope _ distances _ before _ taper**:这里有一个相当明确的迹象表明运动员需要跑更多的距离。所以把这个和前一个变量考虑进去，可能是他们需要跑的更少，但是跑的更远。
*   f _ proportion _ distance _ activities:这支持了前面的两点:在跑 PB 之前跑更大比例的长距离显然是很重要的。请记住这种相关性的潜在危险——运动员经常在有意尝试马拉松 PB 之前进行几次长跑。

# 可视化

那么这对个人有什么用呢？有了上述模型，就有可能将某个运动员的训练与理想情况进行比较。如下所示，在此处有关于阅读图表[的解释。](https://howeffectiveismyrunningplan.appspot.com/about)

这些特性按照**潜在增益**排序:模型中特性的能力，乘以你在这方面的训练有多差。除了明显的“跑得更多”和“跑得更频繁”，该模型清楚地指导运动员“以 Z2 的心率跑得更多”、“跑更多的山”和“少游泳”。

![](img/8db5d2ef6697d23514ea1a1f15a1800d.png)

# 生产

这种小规模的生产相当简单，我使用了完全的谷歌云设置。结果是一切都非常快，除了 Strava API 查询的速度限制在每秒 1 次左右。

*   由于特征工程和机器学习后端是在 Python 上运行的，所以我用了 Flask 前端
*   该解决方案托管在谷歌云应用引擎上
*   该数据库托管在谷歌云 SQL 上
*   一旦新运动员注册，Cron jobs 就会运行特征工程和 ML 训练算法
*   当加载可视化页面时，Flask 查询后端以生成 matplotlib 图像

# 下一步是什么？

有许多改进可以做，**特别是对可视化及其解释**。然而，首先，我想获得更多的数据，以便建立一个更好的模型来解释如何获得更快的速度。这种更具因果关系的模型对运动员个人来说会更加有用。