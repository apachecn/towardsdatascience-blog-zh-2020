# 离线强化学习的力量:第一部分

> 原文：<https://towardsdatascience.com/the-power-of-offline-reinforcement-learning-5e3d3942421c?source=collection_archive---------9----------------------->

## 可能扩展到现实世界问题的 RL 算法

![](img/41158a398e9986078446c4696e55802c.png)

[来源](https://pixabay.com/illustrations/evolution-artificial-intelligence-3885331/)

**线上 RL 的局限性**

强化学习在过去几年中发展迅速，从只能解决简单玩具问题的表格方法到处理难以置信的复杂问题的强大算法，如下围棋、学习机器人操纵技能或控制自动驾驶汽车。不幸的是，RL 在现实世界应用中的采用有些缓慢，虽然当前的 RL 方法已经证明了它们能够找到高性能策略来解决高维原始观察(如图像)的挑战性问题，但实际使用它们通常很困难或不切实际。这与监督学习方法形成了鲜明的对比，监督学习方法在工业和研究的许多领域非常普遍，并获得了巨大的成功。这是为什么呢？

大多数 RL 研究论文和实现都面向**在线学习**设置，其中代理与环境交互并收集数据，使用其当前策略和一些探索方案来探索状态-动作空间并找到更高回报的区域。这通常以下列方式说明:

![](img/c87bbf9ba363e9220d1c425e07339448.png)

原创艺术

这种在线 RL 算法与环境交互，并立即或通过一些重放缓冲器使用收集的经验来更新策略。重要的是，数据是直接在环境中收集的，并且只有这些数据用于学习，学习和收集是交替进行的。

这带来了几个困难:

-代理必须收集足够的数据来学习每项技能/任务，这对机器人或自动驾驶汽车等系统来说可能过于昂贵。

-代理使用部分训练过的策略与环境进行交互，这可能会采取潜在的不安全行为，例如给患者服用错误的药物。

-使用训练环境为每个任务收集专门数据的需求通常会导致非常狭窄的状态分布，这可能会导致策略易受轻微变化的影响，从而使其不值得部署。

当将 RL 应用于现实世界的问题时，这些并不是人们可能面临的唯一困难，但是它们可能是决定不在您的任务中使用 RL 的主要因素。简单地浏览一下当前的 RL 研究论文就足够了，即使是相对简单的模拟任务也经常需要数百万个交互步骤来学习一个好的策略，那么在真实的机器人上尝试这一点并为每个新任务收集如此大量的数据会有多实际呢？

有趣的是，这些问题在监督学习中并不常见。当训练图像分类器或对象检测网络时，从业者通常可以在不同的现实世界设置中访问大量标记数据的数据集。这就是为什么许多这样的监督学习模型有时甚至在与训练期间遇到的图像非常不同的输入图像上也能惊人地推广，并且通常可以针对具有非常少的标记任务数据的新任务进行微调。在 NLP 社区中可以看到类似的事情，在那里，在巨大的数据集上预处理的大型模型对于学习新任务非常有帮助，使得该过程变得可行，并且在标记的任务数据方面只有适度的要求。

![](img/81817a9d39620bfb26fad286759bcc7d.png)

[来源](https://pixabay.com/vectors/robots-silhouette-web-internet-4838671/)

那么，为什么不在学习政策时也这样做呢？假设我们想从图像中学习一些机器人技能，我们不能只使用在 ImageNet 上预先训练的模型吗？事实证明，这与我们在监督学习中习惯的好处不太一样，因为这样的模型没有给我们任何关于我们应该做什么的线索，因为它没有经过任何**任务**的训练。还有什么办法可以缓解这个问题，让 RL 更适用于现实问题？

**非政策 RL 和分配转移**

2018 年发表了一篇令人印象深刻的论文，名为“ [QT-Opt:基于视觉的机器人操纵的可扩展深度强化学习](https://arxiv.org/pdf/1806.10293.pdf)”。在这篇论文中，作者(谷歌…)使用几个机器人同时收集数据，并训练了一个抓取垃圾箱中物体的策略。他们连续进行了几个月的实验，并在此过程中进行了 58 万次抓取尝试，产生了一个最先进的抓取策略。在其核心，他们的方法是基于 Q 学习，这是一种基于动态规划的 RL 方法。我们在 RL 中的目标是找到最大化期望值**的策略**:

![](img/90f5df486cb14d672631b5917a5eaf55.png)

对于给定的状态，策略的价值函数告诉我们，通过遵循来自该状态的策略，我们可以期望得到的折扣奖励的总和是多少，并且 RL 的目标是找到在所有状态上期望值最大的策略。我们还可以描述 **Q 值**，这是我们希望通过采取特定行动，然后从现在开始遵循该政策而获得的值:

![](img/4fc5edbd92feaa0f8c10cb83c05b776c.png)

在 Q 学习中，我们试图通过最小化贝尔曼误差来找到最优 Q 函数(或最优策略的 Q 函数):

![](img/3836a8eea1a24daafb3744f950f97f71.png)

对于所有状态动作，贝尔曼误差为零的 Q 函数保证是最优的，并且我们可以通过在每个状态采取具有最高 Q 值的动作来提取最优策略:

![](img/87e973a4e87b407af34f10fef76f040a.png)

当然，对于实际问题，Q 函数是由一些深度神经网络来近似的，并且需要对基本的 Q 学习方法进行一些修改，以使其以这种方式工作。QT-Opt 论文使用了这种基于 Q-learning 的方法，并获得了非常令人印象深刻的结果(这需要 Google scale 资源)，但他们在论文中进行了另一个有趣的实验；他们收集了训练期间收集的所有数据，并试图仅使用这些数据从头开始训练一个新的 Q 函数，而不与机器人进行任何进一步的交互。

原则上，这应该是可行的。如果我们看上面的数学，我们可以看到 Q-learning 算法实际上不知道数据的来源，这意味着我们可以将其应用于通过任何其他策略或程序收集的数据，特别是我们应该能够在记录的训练数据上使用它。这种特性被称为**非策略学习**，这也是 Q-learning 是一种高效学习方法的主要原因之一，因为它可以重用来自任意来源的数据。然而，令人惊讶的是，作者观察到原始策略(在它收集的相同数据上训练，因为它正在收集它)和使用静态数据训练的策略之间存在显著的性能差距，并且从静态数据中学习产生了更差的性能。这种从静态数据中学习策略或 Q 函数而不与环境进一步交互的过程称为**离线 RL** (有时称为批量 RL)，与我们直接从环境中收集新数据的在线 RL 设置相反。

![](img/8c83c00190a72ca9a0ec9cdf7ec3e199.png)

原创艺术

上图是离线 RL 的样子；数据由某个或某些来源(策略、脚本、人员等)收集。)并保存在某个缓冲区中，策略仅使用该数据进行离线训练，然后在完全训练后部署到现实世界中。

如果收集的数据足够好，可以成功地学习第一个策略，为什么离线训练时效果不好？让我们再次检查 Q 学习算法的贝尔曼误差:

![](img/b497d508cfdcf413e4a3969f3d1454d5.png)

在实践中实施时，我们会这样做:

![](img/c4741cd4326cc19007c90ccfac1e0c82.png)

对于以下形式的转换，我们试图最小化贝尔曼误差:

![](img/25edf225e88d68ac6822ba4b03aad882.png)

其包含状态、从该状态采取的动作、通过采取该动作获得的奖励以及在采取该动作后观察到的状态。计算贝尔曼误差的目标值时:

![](img/db7cfca8bc5b840372f097f15404298f.png)

我们采用我们的 Q 函数**认为**通过采取行动**a’**可以得到的最佳 Q 值，并使用它来校正我们对状态 **s** 的 Q 值的当前估计。这被称为自举，是 Q-learning 的一个重要方面。由于我们的 Q 函数不是最优的(特别是在训练的早期阶段)，这个目标值有时肯定是错误的，并且会导致我们将误差传播到对 **s** 的 Q 值的估计。由于这个原因，在线 RL 来救援，并且由于 Q 函数估计中的错误将导致政策采取错误的行动，它将直接体验采取这些行动的结果，并且最终能够纠正其错误。然而，在离线情况下，这种情况会发生，因为策略不与环境交互，也不收集更多数据，因此无法知道它正在传播错误的值并纠正它们。

更糟糕的是，使用 max 运算符会导致对具有最高数值的 Q 值进行几乎对立的搜索，这通常是非常错误的。在许多情况下，这可能导致预测的 Q 值偏离，训练完全失败。在这种情况下，我们的 Q 函数认为它可以获得极高的回报，而事实上，它不能。从形式上来说，这个问题的出现是因为在收集数据的策略和我们现在学习的策略之间存在分布转移，并且当我们在**s’**上评估我们的 Q 函数并寻找具有最高分数的动作时，我们正在对我们的模型查询它从未见过的状态动作，并且可能是完全错误的。

那么如何才能缓解这个问题，在线下的设定下学好呢？一种方法是通过诸如 KL-divergence 之类的发散度量来约束策略，使得它保持接近数据收集策略。这将阻止 Q 函数传播高度乐观的分布外 Q 值，但可能会阻止它学习比数据收集策略更好的策略。如果数据收集策略不是很好，这可能是一个主要问题，因为离线 RL 的一个主要诉求是改善我们以前拥有的东西，否则我们可以只使用行为克隆并完成它。一个更微妙的约束是强制策略选择与数据集中出现的动作接近的动作，同时允许策略偏离数据收集策略。乍一看，这似乎毫无意义，如果强制使用数据集中相同的操作，策略又怎么会不同呢？下图说明了这一点:

![](img/d0be2cd289e75ca95eea7c53c9687e5b.png)

原创艺术

在上图中，右图描绘了我们的数据中存在的两条轨迹，一条从 A 到达 B，另一条从 B 到达 C。我们希望学习从 A 到达 C，但该轨迹实际上并未出现在数据集中。幸运的是，**轨迹之间有一些重叠，这允许仅使用数据集**中的动作来学习从 A 到 C 的轨迹。这是动态编程 RL 的主要优势之一，它可以将部分轨迹缝合在一起，并学习比数据中呈现的更好的策略。然而，需要注意的是，在大型状态和动作空间中以现实的方式实施这样的约束(仅使用来自数据集的动作)需要我们以某种方式对数据收集策略建模，这通常需要首先用一些神经网络对其进行近似，然后在离线 RL 期间使用它。这种近似的数据收集策略是错误的潜在来源，一些研究论文证明了行为建模的改进提高了这种离线 RL 方法的性能。

这实际上是一个比从文献中乍一看更具挑战性的问题。我们在离线 RL 中的希望是使用从多个来源随时间积累的大量先前经验的数据集，这可能包括像脚本化的政策和人类示威者这样的事情，它们可能以非马尔可夫方式表现，使得对它们的行为建模非常困难。理想情况下，我们希望我们的 RL 算法不需要这样的行为模型，并且简单和可扩展。

**保守的 Q 学习**

最近，Berkeley 的研究人员发表了论文“[保守 Q-Learning for Offline Reinforcement Learning](https://arxiv.org/pdf/2006.04779.pdf)”，其中他们开发了一种新的离线 RL 算法，称为保守 Q learning (CQL)，它看起来表现非常好，同时相对简单，并保持了一些不错的属性。正如我们之前所看到的，当对离线数据执行天真的 Q 学习或 actor critic 算法时，我们在最小化贝尔曼误差时传播高度乐观的 Q 值，并且贝尔曼误差中的 max 算子找出这些误差。CQL 通过对目标函数的简单添加解决了这个问题。

在标准 Q-learning 中，我们的损失是:

![](img/21eec7c0ed5ac5124a85dbb4116c2735.png)

作者建议增加以下内容:

![](img/9e552e33270abd860d98ce1c97e6c983.png)

通过积极地尝试最小化我们的政策认为很高的国家行为的 Q 值，我们逐渐地迫使所有那些乐观的错误，并迫使 Q 值不大于它们实际应该的值。作者证明，通过适当选择α，得到的 Q 函数可以由“真实的”Q 值(未知的)限定，因此是这些值的保守估计。他们从经验上证明确实如此，并且预测的 Q 值低于通过部署学习的策略获得的 Q 值。事实上，得到的 Q 值有点过于保守，作者提出了损失函数的另一个补充:

![](img/3731391481e375c990789b75cc202b8b.png)

这种添加试图最大化数据集中出现的状态动作的 Q 值，鼓励策略坚持更熟悉的动作，并使 Q 值不那么保守。作者证明了期望的结果 Q 值是由“真实的”Q 函数上界的，并证明了这种变体产生更好的结果和更精确的 Q 值。他们在广泛的离线 RL 基准上测试了他们的方法，并表明它优于现有的方法。

这种方法的好处在于它相对简单，解决了核心问题，并且以一种直观的方式运作。它还具有不需要数据收集策略模型的优点，这消除了潜在的错误来源，并从过程中移除了冗余的机器和模型。

**使用先前数据集的归纳技能**

我们已经看到，使用庞大的离线数据集来学习在现实世界中通用的强有力的政策有很大的潜力，离线 RL 算法的改进正在使这一愿景更接近现实，但有一件事一直困扰着我。我看到的大多数研究论文似乎都假设我们想要学习执行某个任务 X，并且我们有一个大型的离线数据集，该数据集标注了针对该任务 X 的适当奖励。这似乎不现实，因为使用离线 RL 的整个前提是能够利用随着时间的推移从不同来源收集的大型数据集，事后来看，假设我们能够用针对我们任务的奖励来标注这样的数据集是可疑的。人们怎么可能用图像来注释机器人开门的数据集，以奖励抓取物体呢？

CQL 论文作者的一篇名为“ [COG:用离线强化学习将新技能与过去的经验联系起来](https://arxiv.org/pdf/2010.14500.pdf)的新论文解决了这个问题，并证明了未标记的离线数据可以用于增强和概括我们任务的较小的注释数据。作者使用了一个机器人的例子，这个机器人被训练来抓取放在一个打开的抽屉里的物体，使用的数据是通过一些脚本化的策略收集的(任务数据)。除此之外，还存在机器人与环境交互的更大数据集，用于其他任务，例如打开和关闭抽屉、拾取和放置物体等(先验数据)。使用一些离线 RL 算法(如 CQL)在任务数据上训练我们的策略将在任务上产生良好的性能，并且机器人将很可能能够以高概率从打开的抽屉中抓取对象。然而，如果我们以某种方式显著地改变初始状态，例如关闭抽屉，那么期望我们的策略现在成功是不现实的，因为任务数据不包含这样的信息。

作者提出了一个简单的解决方案；用稀疏二进制奖励(完成任务+1，否则为 0)注释任务数据，用 0 奖励注释所有先前的数据。然后，将数据集合并，并使用 CQL 对结果大数据集进行训练。正如我们之前看到的，使用动态编程的离线 RL 算法具有看似神奇的能力，可以将部分轨迹缝合在一起，并学习比其部分总和更大的东西。作者证明，CQL 能够将 Q 值从最终目标到达状态一直传播到初始条件(抽屉打开，物体放在里面)，并进一步传播到抽屉关闭的状态，从而学习将任务概括为新的看不见的初始条件，这在为我们的任务收集数据时从未遇到过。

在我看来，这是一个强有力的证明，当提供了先前的未标记数据时，一个简单而优雅的算法可以做什么。我希望在未来，我们将看到更好的方法被开发出来，大量的数据集被收集起来，这将使 RL 在工业和研究中被广泛采用，释放它的全部潜力。

对于感兴趣的读者，我强烈建议阅读谢尔盖·莱文(伯克利研究小组负责人)[关于离线 RL](https://medium.com/@sergey.levine) 的媒体文章。