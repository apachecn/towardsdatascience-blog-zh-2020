# 如何提高预测模型的可解释性

> 原文：<https://towardsdatascience.com/how-to-increase-the-interpretability-of-your-predictive-model-b786d72365f1?source=collection_archive---------41----------------------->

## SHAP 价值观

## 从商业角度的实用见解。

![](img/86bcf6254735736918fabb3984d31c66.png)

作者创作的照片

准确性和可解释性据说是截然不同的。复杂的模型往往能达到最高的精度，而简单的模型往往更容易解释。

但是如果我们想两全其美呢？获得高精度是很酷，但是如果我们能理解模型不是很好吗？尤其是，如果预测对企业的成功至关重要？正如里贝罗等人所说:

> “[……]如果用户不信任某个模型或预测，他们就不会使用它。”(里贝罗等人 2016 年，第 1 页)

# 假设的情况

让我们想象一下:我们在一家大型储蓄银行担任数据科学家。我们的工作是确保我们知道哪些客户很有可能流失。

我们的模型会发生什么？我们将使用我们的结果来创建具有不同流失率的客户群。

然后，具有最高流失率的客户群会接受有针对性的营销，这样他们就不会离开银行。

与获得新客户相比，留住客户的成本要低得多(Keaveney 1995)。因此，我们的工作对银行的成功至关重要！

我们必须实现两个目标:

*   营销团队必须获得尽可能准确的结果。为什么？因为银行是花钱留住这些客户的。如果客户无论如何都会留下来，银行就是在把钱扔出窗外。
*   我们必须让利益相关者相信他们可以信任我们的结果。祝你好运，向营销经理解释我们是如何创建我们的模型的…

所以我们假设营销老板不理解我们的模式，但是信任我们(不管什么原因)。*因此，他们实现了我们的复杂模型。*

*   该模型具有很高的预测能力。营销团队很高兴，因为他们看到所采取的措施有助于留住客户。我们很高兴，因为我们得到了该模型的积极反馈。

不错！我们可以就此收工，把精力集中在下一个任务上，为我们所做的伟大工作获得更多的荣誉。

![](img/691c38e1a05886c2f8b90bb8a568735e.png)

照片由[延斯·约翰森](https://unsplash.com/@jens_johnsson?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

**但是停！坚持住！**

准确性和可解释性不能用同一个模型来实现，对吗？

因此，我们只关注模型的准确性。但是如果模型有瑕疵呢？

我们可以在我们的模型中加入一个变量，这个变量实际上没有任何意义。不知怎么的，有一段时间是管用的，后来就不行了，也没人认了。

更糟糕的是:我们可能创造了一个性别歧视的算法，在社交媒体上引起轩然大波。你认为我在开玩笑吗？这种情况不知何故发生在苹果和高盛身上。

> 一个经理会为了几个更准确的点而拿他/她的职业生涯冒险吗？

在这里我可以给你一个浅显简单的答案……不会，管理者不会冒这个险。他们花了很多年建立自己的事业，对机器学习一窍不通。

当然，预测客户流失概率可能不是一个会在媒体上引起轩然大波的热门话题。但是，如果我们的模式因为我们未能正确理解而对我们不利，*后果可能是痛苦的。*

# 解决方案

可解释性是必不可少的，因为它促进了对我们模型的信心和信任。用户不会采用不能做到这一点的模型。此外，增强的可解释性有助于提高模型性能，并扩展我们可以从模型中获得的知识(Lundberg & Lee，2017)。

不错！通过增加可解释性，我们不仅能够理解我们的模型，还可以获得有价值的见解。也许营销团队想更多地了解他们的客户？

幸运的是，消除模型准确性和模型可解释性之间的权衡已经引起了研究人员的关注(Ribeiro 等人，2016 年 Lundberg & Lee，2017 年 Chen 等人，2018 年)。

> 他们的一个解决方案获得了很多关注:Lundberg & Lee (2017)引入的 SHapley 加法解释(SHAP)值。

SHAP 价值观源于博弈论。他们衡量一个变量的观察水平对个人最终预测概率的边际影响(Lundberg 等人，2019 年)。

通过这种方法，可以解释为什么客户会收到其流失预测值，以及这些特征如何有助于这种预测。这种局部可解释性增加了透明度。此外，将本地解释结合起来以获得全球可解释性也变得可行。

让我们使用这些神秘的 SHAP 值将一个复杂的模型转换成一个复杂的和可解释的模型。

# 和行动

记住，我们想知道哪些客户会流失。因此，我使用这个 [Kaggle 数据集](https://www.kaggle.com/barelydedicated/bank-customer-churn-modeling)来预测银行客户的流失概率。

用于预测流失概率的前十行数据集。

对于预测，我使用了基本的逻辑回归和默认的 XGBoost 算法。为了让这篇文章可读性更好，我不会展示代码行。如果你有兴趣知道我是如何构建模型的，请看看我的 [GitHub 库](https://github.com/JRatschat/How-to-Increase-the-Interpretability-of-Your-Predictive-Model)。在那里你可以找到你需要的一切。

因此，让我们快速比较 logit 模型和默认 XGBoost 模型的模型统计数据。

logit 模型达到 84.1%的测试准确度，而默认的 XGBoost 模型具有 86.6%的测试准确度。AUC 怎么样？这里，logit 模型的 AUC 为 82.3%，而默认 XGBoost 模型的 AUC 为 85.1%。

事实上，更复杂的模型更能预测谁会流失，谁会留在银行。

因此，我们通常可以使用 XGBoost 的三个不同的重要性度量，通过它们我们可以更详细地了解我们的模型。

![](img/3cd6276d442dad035dc82dc29ba66b69.png)

XGBoost 模型的重要图。作者创造的情节。

我想到了什么？这三种重要性度量为要素分配了不同的重要性级别。

此外，我看不出自变量和客户流失之间的关系。更高的年龄是增加还是减少成为一个搅动者的概率？这些情节无助于回答这个问题。

因此，让我们看看如何使用 SHAP 值来解释我们的模型。

在下图中，特性按照它们对默认 XGBoost 模型的全局影响进行排序。较高的 SHAP 值表示客户退出银行的预测较高。圆点表示训练集的各个预测对模型输出的特征影响。根据特征值的不同，点的颜色从蓝色(低)到红色(高)。因此，我们可以探索特性影响的范围、强度和方向。

![](img/0fa94ae04ca5f8b05a4e525f95fc8cbb.png)

SHAP 概要图。作者用 [SHAPforxgboost](https://github.com/liuyanguu/SHAPforxgboost) 创作的剧情。

年龄、NumOfProducts 和 IsActiveMember 具有最高的全局功能重要性。从这个概要图中，我们可以得出几个有趣的见解:

*   特征对预测的影响范围是广泛分布的。例如，年龄对一些客户的预测有很大的影响，而对另一些客户则只有很小的影响。
*   尽管有些变量的全局重要性较低，但该特征对某些个体的影响可能很大。例如，对于信用评分低的人来说，信用评分与流失有正预测关系。
*   乍一看，一些变量显示出与客户流失的直观关系，而对其他人来说，这是违反直觉的。例如，为什么产品数量越多，客户流失的可能性就越大？这有道理吗？

为了更深入地研究单个变量，我们可以使用依赖图。下图显示了年龄的 SHAP 依赖图。与汇总图一样，每个点都是一个客户。如图所示，年轻客户对流失的预测值较低，而年长客户对流失的预测值较高。但这不是线性关系！当达到 60 岁时，客户流失概率开始下降。

![](img/32c2758a1cacad98aa8a75573b82224c.png)

年龄的 SHAP 依赖图。作者使用 [SHAPforxgboost](https://github.com/liuyanguu/SHAPforxgboost) 创建的情节。

祝你用 logit 模型探索这种关系好运…

![](img/780620bc5da66c8cbd1451d4d0f2ba89.png)

基于与 XGBoost 模型相同的数据的逻辑回归的摘要输出。年龄变量突出显示。

要疯狂，还可以看看变量的交互作用效果。

在下面的左侧面板中，您可以看到年龄变量的相同依赖关系图。但这一次，我加入了性别变量，以观察年龄和性别如何相互作用。

在右边的图中，年龄和性别的交互作用表现得更为明显。不知何故(我缺乏解释这一点的领域知识)，当与年龄配对时，男性和女性有不同的行为。例如，年轻女性的 SHAP 互动值为负值，这意味着年轻女性的 SHAP 值低于年轻男性。

![](img/ee24843e9c5081e666fd0f9c52749730.png)

年龄和性别的 SHAP 依赖性图(左图)和 SHAP 相互作用图(右图)。作者用 [SHAPforxgboost](https://github.com/liuyanguu/SHAPforxgboost) 创作的情节。

到目前为止，一切顺利。但是，客户拥有的产品数量对客户流失预测的影响如何呢？至少对我来说，产品越多的客户越有可能翻盘，这似乎有悖常理。我们都知道终止合同有多难，尤其是银行合同。

当观察逻辑回归的系数值时，我们看到了同样的效果。不知何故，与拥有一个、三个或四个产品的客户相比，拥有两个产品的客户流失的可能性更低。

![](img/bad12919c8a51ff9a635b983f97343c5.png)

logit 模型的摘要输出基于与 XGBoost 模型相同的数据。突出显示 NumOfProducts2 变量。

因此，我假设这种趋势存在于数据中，而不是被我们的 XGBoost 模型随机使用。

我还担心吗？是的。我通常会做什么？

*   **看文献。**这种关系可能有意义，谁知道呢？
*   质疑数据的相关性。当我搜索数据集时，我已经想到了这个主题。我没有太多的选择，而且这个数据集没有版权。算法和数据一样好。
*   **探索数据集。**在建立模型之前进行解释性分析是非常可取的。也许，我可以找到一些模式来解释这个违反直觉的结果。
*   **删除变量。**如果我怀疑该变量不能提供有意义的结果并可能导致缺陷，我会删除它。即使这意味着损失一些准确性或 AUC 百分点。

到目前为止，我所做的分析可以用于每一个变量。我们需要完全理解我们的模型，对吗？但是因为这篇文章太长了(如果你到目前为止还没写完，就猛敲！)，我就不赘述给你进一步分析了。

# 结论

理解我们的预测模型以及该模型捕捉数据的一般潜在趋势是至关重要的。否则，该公司将面临一颗定时炸弹。一切都很顺利，直到它不再顺利。

此外，我们需要能够向相关的利益相关者解释我们的结果。向一个理解基本统计学有困难的人解释预测模型，首先是 SHAP 值是很难的！尽管如此，这些利益相关者通常是决策者，所以我们必须确保我们可以让他们相信我们的模型在实践中确实有效。

除了通过增加对我们模型的信任来减少可能的风险，我们还可以获得更简单的模型所不能获得的额外的洞察力。这可能非常相关。尤其是对于总是有兴趣了解客户的营销部门来说。

*如果您有任何问题或意见，欢迎在下方留下您的反馈。另外，如果你想和我联系，你可以通过*[*LinkedIn*](http://www.linkedin.com/in/jonathan-ratschat)*联系我。*

*敬请期待，下期帖子再见！*

如果你对我和 190 名学生如何学习数据科学感兴趣，请查看以下文章:

[](/how-190-students-and-i-have-learned-data-science-55da9e0e5c6b) [## 我和 190 名学生是如何学习数据科学的

### 如何学习编码的可行策略？

towardsdatascience.com](/how-190-students-and-i-have-learned-data-science-55da9e0e5c6b) 

[1] Ribeiro，M. T .，Singh，s .和 Guestrin，C. (2016)，“我为什么要相信你？”:解释任何分类器的预测，见 B. Krishnapuram & M. Shah 编辑的“KDD 16:第 22 届 ACM SIGKDD 知识发现和数据挖掘国际会议论文集”，第 1135–1144 页。

[2] Keaveney，S. M. (1995)，“服务业中的顾客转换行为:一项探索性研究”，《市场营销杂志》59，71–82。

[3] Lundberg，s .和 Lee，S.-I. (2017)，解释模型预测的统一方法，载于 U. von Luxburg，I. M. Guyon，S. Bengio，H. M. Wallach 和 R. Fergus 编辑的《NIPS'17:第 31 届神经信息处理系统国际会议论文集》，第 4768-4777 页。

[4]陈，j .，，温赖特，M. J. &乔丹，M. I. (2018)，学习解释:模型解释的信息论观点，载于 J. G. Dy & A. Krause 编辑的《第 35 届机器学习国际会议论文集》，第 882-891 页。

[5] Lundberg，S. M .，Erion，G. G. & Lee，S.-I. (2019)，《树集合的一致个性化特征属性》，第 1–9 页。