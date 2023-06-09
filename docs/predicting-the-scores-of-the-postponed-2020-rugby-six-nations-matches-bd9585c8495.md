# 预测推迟的 2020 年橄榄球六国赛的比分

> 原文：<https://towardsdatascience.com/predicting-the-scores-of-the-postponed-2020-rugby-six-nations-matches-bd9585c8495?source=collection_archive---------49----------------------->

## 访问和分析六国橄榄球数据，以及预测剩余延期比赛的分数

# 介绍

六国橄榄球锦标赛是一年一度的橄榄球联盟比赛，由英格兰、法国、爱尔兰、意大利、苏格兰和威尔士的国家队参加。锦标赛定于 2020 年 3 月 14 日结束；然而，由于新冠肺炎疫情，意大利对爱尔兰的倒数第二场比赛和所有的决赛都被推迟，意在改期。这是自 2001 年爆发口蹄疫以来，首次有超过一场比赛被推迟。鉴于此，威尔士橄榄球球迷󠁷󠁬󠁳and 的数据科学家对冠军赛的相关数据以及利用这些数据可能实现的目标感到好奇。这是我写的一篇关于我对六国橄榄球数据的分析，以及预测 2020 年推迟比赛的分数的文章。

# 六国橄榄球数据

首先要克服的问题是获得一些我可以用来模拟橄榄球比赛的数据。鉴于锦标赛始于 1882 年，我很早就决定要调查每一场可能的比赛，这需要花费相当多的时间和精力。随着锦标赛在 2000 年正式成为六国赛，我转向谷歌，开始寻找 10 年的橄榄球数据。

在网上查看后，我偶然发现了 ESPN Scrum 网站，它包含了从 1882 年以来所有六个国家比赛的基本数据。

![](img/d8a3d4edfb9196216631a2bd4380bbd4.png)

ESPN Scrum 网站

最突出的一点是数据是表格形式的。当我看到这张写着“*的桌子*”时，我不禁暗自高兴。表格是我们的朋友，它让处理数据变得更干净，更轻松。也就是说，只有当数据源结构良好时，这才是正确的。

让我们看看这个网站还能提供什么。当你点击冠军年，在这种情况下，2020 年，你会被重定向到另一个页面，其中包含了迄今为止的结果表。我们可以看到，爱尔兰和意大利、威尔士和苏格兰、意大利和英格兰、法国和爱尔兰之间的最后四场比赛由于延期，因此没有与之相关联的比分。这些是我们想要预测的。

![](img/5aadc612908a78a14910f35215261781.png)

2020 年橄榄球六国记分牌至今

这个阶段需要考虑的重要的是可用的数据；也就是说，这些变量是否对匹配建模有用。我们目前知道的是，对于每支球队来说，比赛是在主场还是客场进行的，比分，以及球队是赢了还是输了比赛。在这个阶段，这些属性可能足以做出合理的预测。然而，关注球队层面的变量，比如每支球队的出场总数，以及球员层面的变量，比如他们的身高、体重、最近的表现等等，会很有趣。如果我们可以找到一个可靠的数据资源，并且数据容易访问，我们可能会在以后添加这些。但是首先，让我们从 ESPN 网站上摘录这些信息。

# 网页抓取

ESPN 网站不提供任何类型的可下载数据，所以是时候深入网页的来源，提高我的网络抓取技能了！

这个网站的好处在于，2000 年至 2020 年之间的每个记分牌的 HTML 表格都使用相同的 ID。这意味着，给定所有 20 个页面，我可以遍历 URL 并应用相同的预处理步骤来访问每个表。

首先，我复制了 2000 年到 2020 年之间的所有记分牌 URL，并将它们存储在一个数组中。然后，我遍历数组，发出 GET 请求从每个页面获取原始 HTML 内容。使用 BeautifulSoup，HTML 内容被解析为 Python，这样我就可以使用 ID `scrumArticleBoxContent`找到特定的记分板表。

现在我有了所有字符串形式的 HTML 表，我可以使用`read_html`函数将其解析为 Pandas。因为这个函数输出一系列数据帧，所以我可以使用`concat`函数将它们连接成一个主数据帧。然后，我删除了通过 HTML 潜入的不相关的列。

一些行的日期为空，这也反映在 ESPN 网站上显示的表格中。通过使用`ffill`函数，我可以用该列中最后一个已知的日期来填充那些缺失的日期。

为了预测每个国家在推迟的比赛中取得的分数，我们将不得不分开每个比赛记录，以便每个队在单独的一行中得到代表。在此之前，我们还必须考虑到国名的顺序代表了哪个国家是主场还是客场比赛。由于球队的名字有一个破折号作为固定的分隔符，我们可以根据破折号分割字符串，将左边的名字解析到`home_team`列，将右边的名字解析到`away_team`列。

现在队伍被分开了，我们也必须从队伍名称中删除分数。我们可以使用 Regex 从团队名称中提取数字，并将它们解析到`home_team_score`和`away_team_score`列中。

我们还想知道比赛场地的名称。鉴于这些数据在另一页的另一个表格中，我将打一张懒牌，假设在过去 10 年里，这些比赛在每个国家的同一个体育场进行。我可以通过迭代球场名称并从我的球场字典中分配相应的值，将球场名称与主队联系起来。

基于这最后一个数据帧，我们知道如果`home_team_score`不为空，游戏就开始了，如果为空，那么这些就是被推迟的。我们可以根据这个规则将数据分为训练和测试。

让我们先关注一下训练数据。在这个博客的下一部分，我需要知道哪个国家赢了这场比赛。这不会作为一个变量包含在游戏比分预测中。为此，我遍历训练数据帧，并将获胜的团队关联到一个`winner`列。

最后，为了分割数据，使每个国家都是数据框中的一行，我可以根据国家是主场还是客场来选择这些国家，然后将它们附加到另一个国家的顶部。

# 快速分析

这篇博客的主要焦点是看我们是否能做出合理的比赛分数预测。然而，我认为快速查看数据中是否存在任何潜在模式也很有趣。我感兴趣的一件事是，与客场比赛相比，一个球队在主场比赛时是否会赢得更多比赛，这两者之间是否存在某种关联。

围绕主场优势有很多卓有成效的研究。也就是说，有没有据说主队比客场队获得的好处？这些好处可以归因于支持球迷对竞争对手或裁判的心理影响、时区或气候的差异、旅行后的疲劳以及许多其他因素。所以，我想知道 10 年来 6 个国家的数据是否反映了这一点。

熊猫的`correlation`函数用于查找数据帧中各列之间的成对相关性。因为这个函数忽略任何非数字数据，所以必须首先将它们映射到某种数字表示。熊猫有另一个内置功能可以为你处理这些。当您将列的数据类型转换为`category`时，该列会将非数字数据转换为分类表示。因此，在这种情况下，如果我们要查看一支球队在主场或客场比赛时与他们输赢之间是否存在相关性，例如，这些列将把`win`转换为 1，把`lose`转换为 0。

如果我们对整个数据集应用`correlation`函数，我们会得到 12%的相关分数。相关性旨在最大化其价值；也就是说，较高的分数意味着属性之间有很强的关系。所以在这种情况下，12%的低得分表明没有太大的主场优势。

现在，我不是 100%确信这是真的。当我的祖国威尔士在卡迪夫千年体育场主场比赛时，我确信当威尔士观众放声高唱[卡隆·兰](https://www.youtube.com/watch?v=yYOxBncgmLQ)时，这点燃了威尔士橄榄球队的某种激情。我自己想想都起鸡皮疙瘩！所以，我们来看看这个。

如果我们关注威尔士在 10 年六国赛中的表现，我们可以绘制出一些结果。首先，我们来看看他们的总体表现。10 年来，威尔士队参加了 100 场锦标赛。在这 100 场比赛中，威尔士赢了 52 场，输了 45 场，平了 3 场。

如果我们看看威尔士主场 49 场比赛的结果，他们赢了 28 场，输了 20 场，平了 1 场。

最后，如果我们看看威尔士 51 场客场比赛的结果，他们赢了 24 场，输了 25 场，平了 2 场。

鉴于这些结果，可以有把握地说`correlation`指标反映了相同的输出。与客场作战相比，威尔士主场作战时只多赢了 4 场比赛。但这并没有抵消我们的主场优势。这只告诉我们这个数据集内的相关性。我们可以将其他几场橄榄球比赛纳入分析，这些比赛可能会改变这一结果。

# 进行分数预测

将主场优势放在一边，我想看的下一件事是预测剩下的延期比赛的比分。有两种监督学习方法。**回归**用于预测连续值，而分类预测离散输出。例如，预测房子的英镑价格是一个回归问题，而预测肿瘤是恶性还是良性是一个分类问题。由于橄榄球比赛的最终得分在技术上可以是任何正数(甚至是零)，我们将研究回归方法。

首先，让我们为训练和测试添加一个标签，这样我们就可以知道哪个数据集是哪个数据集。然后我们将它们组合起来，并对`team, stadium`和`home_or_away`列进行编码。这是为了确保在我们再次分割它们之后，我们在每个集合中有相同的列和编码。这里需要注意的是，我没有将`date`作为建模中的一个变量。现阶段我只是希望能够根据前面几场的比分来预测剩下几场的比分。此外，由于锦标赛通常在每年的同一时间举行，我不认为这对造型有多大影响。如果是季节性的，这可能是一件有趣的事情。

一旦我们对数据进行了编码并再次将其拆分，这样我们就有了训练集和测试集，我们将需要再次拆分我们的训练数据，这样我们就有了验证集。也就是说，我们将从训练集中抽取一个数据样本，这样我们就可以评估我们的模型在预测这些样本的分数方面的性能，因为我们已经知道答案。为此，我们将抽取 30%的训练集样本。所以在 610 个记录中，有 183 个样本。我们还将确定哪些列是属性，哪些是标签。属性是自变量，而标签是我们想要预测其值的因变量。现在我们已经对数据进行了编码，我们有 14 个属性，我们希望根据这些属性来预测分数。因此，我们的属性被设置为 *X* 变量，而`score`列被设置为 *y* 变量。

现在来训练一个模型。这个问题虽然是回归问题，但不是线性问题。并不指望每支球队在每场比赛后得分都会增加。这就抵消了那些方法。在这种情况下，我决定使用一个 **RandomForestRegressor** ，因为该算法易于使用，相对准确，而且与标准决策树相比，它可以减少过拟合。随机森林算法创建了几个决策树，在特征权重中注入了一些随机性。这些决策树然后被组合以创建一个用于最终分析的森林(因此是决策*树* ) 的*随机森林*)。该算法既支持分类，也支持回归，使其非常灵活地用于各种应用。

在构建和训练我们的模型之前，我们首先需要设置一些超参数。这些参数通常是最难设置的，因为这些设置通常没有完美的值。一般的经验法则是最初坚持使用默认值，然后一旦模型被训练和测试，就开始使用试错法来调整这些值，直到获得最佳结果。对于这个模型，我发现 50 个 *n 估计值*和 4 个 *max_depth* 是提供最佳结果的一组很好的值。有关这些特定设置的更多详细信息，可在[官方 scikit-learn 文档](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html)中找到。

我将在`X_train`(属性)和`y_train`(标签)上拟合模型，然后预测我们从训练中移除的验证样本`X_val` 的得分`y_pred`。然后，我会通过测量均方根误差(RMSE)来比较预测值和实际得分(T4)。

RMSE 是残差方差的平方根。它表示模型与数据的绝对拟合。也就是说，观察到的数据点与模型的预测值有多接近。它还有一个有用的特性，就是和你要预测的变量在同一个单位里；所以在这种情况下。

模型的 RSME 结果是 10.1 (10)分…好吗？不好？绝对不完美。由于大多数球队每场比赛得分不到 40 分，10 分的误差并不是特别准确。正如这里所展示的，该模型在预测所有结果的分数方面做了相当多的工作。在预测得分较低的游戏时，该模型似乎表现得更好，但不是明显更好。也许如果我们把那些高分匹配从图片中去掉，我们可能会看到模型中的错误减少。但我们希望捕捉这些可能性，不会把它们视为离群值。这是需要进一步调查的事情。

让我们看看这个模型对延期比赛的预测得分。我们可以在`X_test`上应用模型，并将预测作为一列附加到测试数据帧上，这样更容易阅读。

好的。模型还没有给出不切实际的预测！预计英格兰会以 36 比 13 战胜意大利。虽然这么说让我很痛苦，但考虑到英格兰目前领先赢得整场比赛，这似乎是一个令人尊敬的预测。爱尔兰看起来像预测他们会输给法国 19 比 25。同样，这似乎不是一个不切实际的预测。在每场比赛以大约 10 分的优势击败英格兰和意大利之后，法国和英格兰并列榜首。预测威尔士 25 比 16 赢苏格兰(耶！🏴󠁧󠁢󠁷󠁬󠁳󠁿).在只赢了意大利之后，这意味着我们将会避免那个木勺！最后，预计爱尔兰将以 25 比 11 战胜意大利。

# 结论

那么，我从这个分析中学到了什么？

非线性回归问题并不总是容易的。虽然模型的 RSME 没有我希望的那么低，但我怀疑这是因为数据的可变性。有时威尔士在球场上全力以赴，以超过 40 分的比分获胜，但其他时候，他们真的没有！这是我想进一步调查的事情。我还想在预测中加入其他变量，比如天气状况，裁判是谁，因为他们总是为威尔士的失利负责..还有更多！

![](img/21e0137ddce7511900d640fa74321414.png)

当前橄榄球六国 2020 领先委员会

然而，该模型预测的分数并没有那么不切实际。根据 2020 年锦标赛的分数，预测的产出遵循类似的趋势。总体而言，如果没有奖励积分，法国和英格兰可能会成为 2020 年橄榄球六国赛的共同赢家。

完整的笔记本，请查看下面我的 GitHub 回购:[https://github.com/LowriWilliams/Rugby_Six_Nations_2020](https://github.com/LowriWilliams/Rugby_Six_Nations_2020)

如果你喜欢这篇文章，别忘了点赞和分享。