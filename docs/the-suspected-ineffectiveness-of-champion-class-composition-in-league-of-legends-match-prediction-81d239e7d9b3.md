# 《英雄联盟》比赛预测中冠军职业构成的疑似无效性

> 原文：<https://towardsdatascience.com/the-suspected-ineffectiveness-of-champion-class-composition-in-league-of-legends-match-prediction-81d239e7d9b3?source=collection_archive---------41----------------------->

## 讨论使用 k-均值聚类对冠军进行分类及其对预测比赛结果的有限影响

![](img/d56481e6d56c3a6fb7d68df1474c118f.png)

在一场联赛的选秀阶段，普遍的观念是至少要有一辆坦克，平衡的 AD 和 AP 冠军比例等等，以形成一个强大的冠军组合。如果这是真的，有没有一种方法可以结合冠军类的构成数据来预测比赛结果？当然，有许多其他因素会影响比赛的结果，但很多时候，当一场比赛赢了或输了，人们会将结果归咎于选秀阶段(冠军选拔阶段)。也许对此的一项研究可以告诉我们，我们可以在多大程度上指责教练的正确/错误选择和禁令。

在这个研究中，我使用 k-means 聚类将冠军分成各种簇，我有时会从现在开始将这些簇称为“类”。一些衍生的集群与我们对冠军职业的常规概念相吻合:例如，一个集群充满了远程的，基于 AD 的冠军，一个我们可以称之为射手职业的集群。其他的就不那么直观了。然而，使用这种分类并没有对各种神经网络模型的预测精度产生任何积极的提高。这似乎表明，尽管不是决定性的，冠军阶层的构成本身没有预测能力。

# 背景和期望

## 以前的文献

以前没有文献研究冠军的分类。然而，为了预测这项研究的结果，有几项研究值得注意。Hall (2017)表明，完全忽略冠军选择，仅从过去 20 场比赛中获取球员统计数据，足以在 LoL 比赛预测中产生 84.4%的准确性。考虑到 LoL 的复杂性，很难假设像冠军职业组合这样的额外功能可以添加到这种已经令人窒息的高准确性上。

此外，黄等人(2015)使用特定冠军的个人胜率来预测比赛结果，达到了惊人的 91%的准确率，这比他们仅使用冠军选秀权作为输入特征所达到的 64%要好得多。考虑到他们在冠军精选特征上的朴素贝叶斯分类器可能包含了比冠军合成更多的知识，我们可以得出结论，无论这项研究中选择的特征多么有效，最终的准确度都将低于 64%。

这两项过去的研究表明，球员技能的重要性压倒了冠军选秀权的重要性；因此，冠军级作文的重要性要低得多。

## 那么这一切有什么意义呢？

如果课堂作文被认为是如此的不重要，为什么还要测试它呢？

没有办法表达出来，让它看起来更有意义；这项研究的唯一原因是实际证明冠军类构成不重要的直觉。或者，奇迹般地，发现它在某种程度上确实意义重大。

## 基线精度

如果我们使用一个浅前馈神经网络，将冠军类标签作为输入特征，结果的精度在 50%左右，正负 1%。改变训练集和测试集、调整超参数和在各次运行中求平均值无助于提高预测精度。

我说的冠军职业标签是指 Riot 在发布时给每个冠军的职业标签。例如，凯特琳被赋予神枪手标签，戴安娜被赋予战士标签和法师标签。总共有六个职业:战士，法师，射手，刺客，坦克，支援。

为了获得上面的基线预测准确性，我尝试的第一种方法是检索游戏中每个团队的每个冠军的标签，将它们转换为一个热门向量，然后将它们相加，从而为每个团队获得一个 6 大小的向量。然后，我将它们连接成一个 12 大小的向量，并在输入神经网络之前进行相应的标准化。

由于这没有任何意义，我过滤了数据集，提取了正确标记了冠军通道和角色的游戏文件(RiotApi 因搞砸了这一点而臭名昭著……smh ),然后只使用这些过滤的游戏文件作为训练/测试集，只是这次我根据通道(按顺序分别为顶部、丛林、中部、底部、支持)连接了所有的一个热点向量，并跳过了求和部分。这让我得到了一个 60 大小的输入特性，尽管进行了所有的超参数调整，它仍然显示出令人沮丧的预测准确性。

然而，将结果建立在 Riot 的冠军类标签上是不公平的，因为 Riot 经常弄错(就像他们的 RiotApi 一样)。因此，为了更好地对冠军进行分类，我决定使用 k-means 聚类，这是一种无监督聚类算法。

# 数据预处理

## 使用的数据集

我在 Kaggle 上使用了 *michel 的 fanboi* 数据集来检索白金级 9800 款游戏的 gameId，并在运行 ec2 实例的 2~3 天内获取这些，使用 RiotWatcher 进行限速指导。从累积的匹配数据中，9000 个用作训练集，其余 800 个用作测试集。

我还应用了与计算基线精度时相同的过滤函数。编号为 3695 的过滤训练集和编号为 343 的过滤测试集。

## 应用 K-均值聚类

为了应用 k-means 聚类，我必须指定 LoL 冠军将在哪些维度上分类。选定的尺寸如下:

> towerKills '，' inhibitorKills '，' baronKills '，' dragonKills '，' riftHeraldKills '，' stats.kills '，' stats . stats . magicdamagedealt '，' stats.physicalDamageDealt '，' stats.trueDamageDealt '，' stats.largestCriticalStrike '，' stats . totaldamagedealttochampions '，' stats . magicdamagedealttochampions '，' stats . physicaldamagedealttochampions '，' stats '，' totalHeal '，'等

我使用 Pandas framework 加载所有的训练集 csv 文件，然后取上面列出的所有列的平均值。下一步是标准化数据，然后使用 sklearn 的聚类库来应用 k-means 聚类算法。对于 k-means，有必要指定聚类的数量，这使得它成为该项目的超参数之一。峰值提前，15~20 个集群显示为最佳。

为了形成输入特征，我使用了与计算基线精度相同的两种方法，只是这次使用了 champion 分类的聚类算法的结果。

由 k-means 算法产生的 20 个聚类如下:

1.  ' Sion '，' Warwick '，' DrMundo '，' Trundle '，' JarvanIV '，' Skarner '，' Poppy '，' Shen '，' Ornn '
2.  凯乐，伊莉斯，希瓦娜，齐格，戴安娜，埃克科
3.  '勒布朗'，'提莫'，'科尔基'，'维伽'，'奥丽安娜'，'朗布尔'，'仙后座'，'黑默丁格'，'肯南'，'马尔扎哈尔'，'艾克瑟瑞斯'，'阿里'，'维克多'，'辛德拉'，'奥雷连索'，'佐伊'，'维尔科兹'，'塔利耶'，'阿济尔'
4.  '莫甘娜'，'闪电侠'，'利昂娜'，'鹦鹉螺'，'布劳姆'，'拉什'，'巴德'，'拉坎'，'皮克'
5.  约里克，俄洛伊
6.  '战争女神'，'特莉丝塔那'，'财富小姐'，'阿什'，'凯特林'，'瓦鲁斯'，'凯撒'，'金克斯'，'卢西恩'，'卡莉斯塔'，'赛亚'
7.  '奥拉夫'，'赵信'，'沙科'，'夜曲'，'莱辛'，'乌迪尔'，'格雷夫斯'，'伦加'，'赫卡里姆'，'卡济克斯'，'卡因'，'亲族'，'六'，'雷科赛'
8.  阿木木'，'披甲龙龟'，'毛凯'，'塞胡阿尼'，'扎克'
9.  马斯特伊'，'薇恩'，'盖伦'，'柯格玛'，'大流士'，'卡米尔'，'塞特'
10.  弗拉迪米尔、莱泽、伊芙琳、卡瑟斯、卡萨丁、莫迪凯塞、菲兹、西拉
11.  特伦达米尔'，'菲奥拉'，'德莱文'，'奎因'，'亚修'，'阿弗利奥斯'
12.  “安妮”，“扭曲的日期”，“阿尼维亚”，“卡塔琳娜”，“暗影之拳”，“西萩五十铃”
13.  艾翁的
14.  “加利奥”，“小提琴”，“烧毛”，“乔加特”，“斯温”，“马尔菲特”，“古拉加斯”，“丽桑卓”
15.  索拉卡'，'基兰'，'索纳'，'迦娜'，'卡玛'，'力士'，'露露'，'塞纳'，'娜美'，'大村裕美'
16.  努努，奈达利
17.  品牌'，' Zyra '
18.  ' Urgot '，' Jax '，' Irelia '，' Renekton '，'悟空'，' Nasus '，' Riven '，' Gnar '，' Kled '，' Aatrox '
19.  阿里斯塔'，'宝石骑士'，'塔姆肯奇'
20.  '抽动'，'跳板'，'万神殿'，' Ezreal '，'塔龙'，'杰斯'，'泽德'，'奇亚纳'

# 培训和结果

## 网络体系结构

通常我会写下超参数、神经网络的层数等，但我没有这样做，因为最终的预测精度不令人满意，其中一个可疑的原因是我在超参数调整方面的无能。

也就是说，曾多次尝试对网络进行微调。值得注意的是，增加层数&网络层数的大小似乎只会鼓励过度拟合。逻辑回归实际上产生了最好的结果。

## 结果/讨论

由于最终的预测精度因运行而略有不同，所以我取了 50 次运行的平均值，结果为 54.17%。虽然它击败了基线准确性，但最终的准确性仅比蒙住眼睛猜测获胜团队略好。这可能有几个原因。

首先，k-means 聚类算法选择的维度可能不合适。以第 9 组为例。这里的冠军因为他们高百分比的真实伤害而明显被分组在一起，但是在这个过程中，远程射手冠军*薇恩*和近战坦克冠军*盖伦*被分组在一起。应该做进一步的工作来为各个维度分配权重，以更准确地对冠军进行分类，尽管其对整体预测准确性的影响是可疑的。

第二，我可能在任务中使用了错误的聚类算法。K-means 聚类算法将冠军分为离散的组，但更好的选择可能是，例如，用于期望最大化聚类的高斯混合模型，它允许将某些数据点包含在多个聚类中。这对于联盟中的许多冠军来说是有意义的，他们可以被归类为法师、射手、发起者等等。

第三，所选数据集仅来自白金级。如果这个技能水平存在一定的偏差，以至于对冠军构成的强调已经过时，那么这里的结果不能推广到整个 LoL 游戏。

然而，我确实相信，基于上述因素改进模型可能不会大大提高预测准确性。事实上，正如我在前面提到的，这里的结果与以前文献的结论一致。

因此，似乎有理由得出这样的结论:冠军职业的构成很可能在决定比赛结果方面并不重要。

1.  霍尔，肯尼斯·t，2017，*深度学习进行英雄联盟比赛预测*
2.  黄，托马斯和金，大卫和梁，格雷戈里，2015，*英雄联盟胜利预测师*
3.  米歇尔的 fanboi，2020，*英雄联盟钻石排名赛(10 分钟)，*[https://www . ka ggle . com/bobby science/League-of-Legends-Diamond-Ranked-Games-10 分钟](https://www.kaggle.com/bobbyscience/league-of-legends-diamond-ranked-games-10-min)
4.  https://riot-watcher.readthedocs.io/en/latest/暴乱观察者