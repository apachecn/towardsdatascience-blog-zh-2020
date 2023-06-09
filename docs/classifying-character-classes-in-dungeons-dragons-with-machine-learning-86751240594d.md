# 用机器学习对《龙与地下城》中的角色分类

> 原文：<https://towardsdatascience.com/classifying-character-classes-in-dungeons-dragons-with-machine-learning-86751240594d?source=collection_archive---------17----------------------->

![](img/4ed1e2b7b7c502d83e4e8093469236ab.png)

Clint Bustrillos 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

几个月前，一个朋友邀请我加入他的在线龙与地下城活动。尽管我有着令人尊敬的书呆子名声，但我从未真正玩过 DnD。我并不是反对它，事实上，它听起来很有趣，我喜欢它鼓励合作和机智的创造力。也许这可以避免我在新冠肺炎的单独禁闭中写论文所带来的单调生活。

我胡乱拼凑了一个我认为会很有趣的角色——*，一个变异的阿西玛六刃术士*。我并不热衷于阅读大量记录游戏元素的神圣书籍来优化我的术士，但我的新 DnD 同胞轻轻地把我推向了正确的方向，给魅力分配了最大的属性(唉，我有一只出汗的袜子的实际魅力来公正地进行角色扮演。)

在这样做的过程中，我开始思考:实际游戏的平衡性如何？是不是所有的优化都会导致相同的基本角色构建？或者我可以根据一个有限的角色信息子集推断出一个角色的类别吗？

# **每个分类器都需要数据**

为了建立一个分类器并回答这个问题，我需要一个 DnD 字符的数据集。我在他的 Github[上找到了一个由 B. Ogan Mancarci 编译的。它包含了超过 7900 个由用户通过他创建的网络应用表格提交的字符条目。他列出了一些关于数据集的潜在警告，这些警告似乎都不会妨碍我正在尝试做的简单研究。我将使用 python 和 pandas 和 sklearn 库作为标准工具集。如果您有兴趣跟随，可以在这个](https://github.com/oganm/dnddata) [git 资源库](https://github.com/nadduck/dnd-ml)中找到包含该分析的(凌乱的)Jupyter 笔记本。

数据包含许多不同的特征，包括提交条目的用户元数据，以及感兴趣的实际字符数据。这些信息中的大部分是不必要的，因为我们主要感兴趣的是角色的统计数据和生命体征，即:

1.  能力分数或属性，即 Cha(risma)、Con(constitution)、Dex(terity)、Int(elligence)、Str(ength)和 Wis(dom)
2.  生命值(HP)
3.  装甲等级(AC)
4.  铸造状态(分类特征，{Cha，Con，Dex，Int，Str，Wis}之一)

提供了关于角色可用的法术和技能的附加信息，但由于以下几个原因，这些信息大多会被忽略:a)许多可能是特定职业所独有的，因此使分类变得琐碎，b)在完全扩展的数据中有数百个法术和技能，这显著增加了适度规模的数据集的维度。这很容易导致后期的过度拟合问题，除非它们能够以不同的方式进行提炼或浓缩。现在，我们也将忽略这些功能和设备。

# **数据探索**

首先，我们将探索数据的一些主要特征，看看是否有任何需要解决的意外情况，或者是否有任何可识别的数据模式可以利用。从一个简单的问题开始:每个类中有多少在完整的数据集中被表示？检查不同类别是否平衡很重要。

![](img/2383fb26ab118b03659de0a09a51c28d.png)

与其他十几个类相比，数据集中 Artificer 样本的稀缺性是显而易见的，也是令人担忧的潜在原因。事实证明，工匠职业是 DnD 5e 佳能最近增加的，因此，还没有足够长的时间供玩家大量选择。这种不到整个数据集百分之一的不平衡可能会在以后产生问题。为了简单起见，我们将在本研究的其余部分忽略这个设计者——至少在有更多的设计者数据可用之前。其余的，虽然没有完全平衡，但仍在合理范围内，无需进一步调整。

DnD 为角色提供了追求多个职业的能力，只要满足特定的条件。对于这个练习来说，这增加了一层额外的复杂性，角色的职业没有很好的定义，玩家在潜在的多个不同方向发展他们的角色时会引入模糊性。为了提高我们的敏感度，我们将只考虑只有一个职业的角色构建，剩下的不到 7，000 个角色。现在让我们探索一下前面提到的不同角色属性的分布，看看是否存在可以区分职业的相关性。

![](img/d21f4f95f7bbeaea1fb75de827edbef8.png)

能力分数、生命值和护甲等级的分布

![](img/5f9aaae4ebf1ed414b17da334bc6276e.png)

不同属性和类别之间的关联热图

从热图中可以看出，某些属性与某些类别的关联可能比其他类别更大。另一方面，一些属性，比如说，战斗/战斗/敏捷施法属性，看起来在所有职业中几乎是一致的，这一点值得注意。

需要警惕的一点是，游戏中的角色进展允许玩家随着游戏的推进增加这些不同的属性。这可能是潜在的混淆，因为一个角色被扮演的时间长度在样本中不是恒定的。下面显示了不同属性与角色等级的关系。

![](img/5e9d811396e4b408d49004b746e2bf89.png)

我们看到角色的 HP 与角色的等级相关，Pearson 分数为 0.93，其他属性的趋势要小得多。为了说明这一点，我们将使用角色的 HP 除以角色的等级，而不仅仅是 HP。

在对这些分布的研究中，有一些异常值，与大部分人口相比，这些异常值似乎具有不自然的大值。尽管有许多处理异常值的选项，我们将对 HP/level 特性应用熟悉的 1.5*IQR 规则，删除 79 个观察值。

到目前为止，在这个初步的探索性分析之后，我们已经以增强我们的建模的统计能力的方式清理和准备了数据集，并且我们还基于类和属性之间存在的不同相关性确定了字符属性似乎是类之间可行的鉴别器。我们现在可以动手做一些初步的建模了！

# 二元建模

虽然最终目标是预测 12 个类别中的一个，但我们可以从一个较低复杂度的分类模型开始，以了解我们可以从数据中预期的性能。为此，我们将手动识别每个类是否是一个*施法*类，并构建一些基本的二元分类器。

我们应该如何决定我们是否成功开发了一个预测模型？我们需要一个[成功指标](/the-5-classification-evaluation-metrics-you-must-know-aa97784ff226)来评估我们的结果。总的来说，这使我们能够比较一个模型与另一个模型的性能，并表明对模型的改进是否使预测朝着正确的方向发展。一种方法可以是准确性度量。我们的数据并没有严重失衡，所以这可能就足够了，但我们还可以做得更好，通过优化 F1 的分数，努力在精确度和召回率方面做得更好。这通常是特定于问题的，您应该决定哪个更重要，是最小化预测负面错误识别还是正面错误识别案例的频率。在我们的情况下，无论我们以何种方式识别错误，都不一定是危险的，但我们可以尝试惩罚假阳性，并尝试实现至少 80%的真阳性率(TPR)，同时只允许 5%的假阳性率(FPR)。

我们将首先尝试 75%-25%训练/测试数据集分割的逻辑回归分类器，并使用 [10 重交叉验证](https://machinelearningmastery.com/k-fold-cross-validation/)方法。我们可以评估测试集的性能，评估我们的成功指标，并检查[混淆矩阵](/understanding-confusion-matrix-a9ad42dcfd62)。

这挺好的！我们成功实现了 87%的 TPR 和大约 10%的 FPR。我们可以用 ROC 曲线来更深入地研究这个问题，看看如果稍微调整一下决策边界，我们是否能达到 80/5 的比率。

![](img/0e3194f7476d452286df840c262bacb2.png)

逻辑回归 ROC 曲线

事实证明，通过对概率阈值的特殊解释，我们确实可以在 TPR 为 80.4%的情况下实现精确的 5% FPR。我们丢失了一些真实的标识，因为这个阈值在分配肯定的标识符以抑制 FPR 时有点保守。我们可以尝试不同的机器学习模型，决策树(DT)，看看它是否允许我们改进我们的建模，并提供更好的 TPR/FPR 比。使用网格搜索交叉验证方法调整 DT 的超参数以改进建模

马上，我们有 92.6%/6.3%的 TPR/FPR，这已经显示出潜在的改善！通过执行相同的练习和检查 ROC 曲线，我们确实找到了一个阈值，在这个阈值内我们可以获得 5%的 FPR 和高达 90%的 TPR！

![](img/e9a7100c998b7cc2589f3f59e6ffcaf0.png)

决策树 ROC 曲线

**多类建模**

这很好，但是现在我们应该停止训练，解决将 12 个不同的类分类的原始问题。我们可以从同样的逻辑回归和 DT 技术开始。有各种方法来计算一个[多类分类](/multi-class-metrics-made-simple-part-ii-the-f1-score-ebe8b2c2ca1)的总数值分数，但总的来说，DT 似乎比逻辑回归和另一个模型，支持向量机(SVM)更能成功地对大多数单个类进行分类。以下是(有点复杂的)混淆矩阵，以及多类 DT 的几个成功指标。

这显示了希望，然而，每个职业的建模能力有很大的差异，从成功的(牧师)到相当糟糕的(术士)。

# 集成学习

也许我们可以尝试使用集成方法来扩展 DT 建模，例如 XGBoost 和随机森林(RF ),从而增加一点复杂性。就其本身而言，XGBoost 并没有明显优于 DT。另一方面，使用 RF，我们似乎仍然能够挤出多一点的辨别能力来改善分类。

在这一点上，就我们能够从我们选择使用的有限数据中提取多少信息而言，我们可能正在接近极限。对于一些职业，即吟游诗人、巫师和术士，由于相似的优化建造，模型似乎很难区分这三个施法者。我们最初忽略了法术的使用，因为它们有效地识别了各自的职业，但也许我们可以注入间接的法术信息，而不用求助于法术本身。具体来说，我们可以将某个特定角色已经学会的*个法术*作为一个特征。然而，就像 HP 一样，一个角色所知道的法术数量是依赖于等级的，随着等级的提高，新的法术也会被获得。因此，我们将添加一个每级法术的特性到我们的数据集中。

我们可以使用这个新添加的列重新运行我们的 RF 模型。

通过为每个职业注入最少的法术信息，我们确实能够在这些职业之间提供更多一点的分离。它仍然不完美，但我们已经达到了一个可接受的阶段，我们可以回过头来检查使用 RF 模型进行分类的[重要特征](https://machinelearningmastery.com/calculate-feature-importance-with-python/)。

![](img/ca6f4f0cca8b4946f2c50ad43e5c6eda.png)

最终随机森林模型的特征重要性

这似乎是明智的，回想一下来自相关矩阵的 Con/Dex/Str casting stat 显示了跨类的一致性。这反映在这个图中，当涉及到分类时，重要性相应地降低。

从这里开始，我们可以继续改进模型，改进现有的特性，删除不重要的特性，或者在模型中加入额外的特性。也许某些种族有利于某些职业的优势，也许某个职业更有利于具有某种道德一致性的角色扮演，更不用说我们从未接触过的武器或技能信息，但可以以类似于法术的方式进行改编。最终，我们应该根据模型在哪里挣扎来决定，并进入需要更多信息来解决的具有最高相似性级别的类。

然而，这篇文章已经写了足够长的时间了，我相信我们已经设法解决了我们试图回答的原始问题。这些职业以独特的方式发展，鼓励不同的角色，让玩家扮演不同的角色。值得一提的是，我们可以总结测试的每个不同多类分类器的不同成功度量分数:

哦，当我们总结事情的时候，也许是为了记录，即使它看起来仍然和我的角色的职业有最大的冲突，我们可以通过我们的小 RF 模型让他看看会发生什么。🤞🏼

🤗

非常感谢 Lance McDiffett，他在一开始就把我拉到了 DnD，并以他作为数据科学家的经验为我的分析提供了宝贵的帮助。