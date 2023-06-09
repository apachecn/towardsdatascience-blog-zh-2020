# AI 是医学的机会吗？

> 原文：<https://towardsdatascience.com/is-ai-a-chance-for-medicine-e07be6aa53ff?source=collection_archive---------43----------------------->

# 还是噩梦？这取决于医生。

# TLDR

自 1958 年著名的达特茅斯会议以来，人工智能(AI)一词导致了感兴趣和不感兴趣的周期性周期，直到 20 世纪 80 年代。然后，数学进步、有效的摩尔定律以及不断增长的数字数据生成和使用，使得非常精确的人工智能模型得以出现，这些模型很有可能对医学和医疗保健产生指数级影响。

然而，似乎没有人在真实的临床世界中真正实现这些模型，以至于像医生一样使用人工智能是很常见的。事实上，成功的实施首先要通过对医生进行文化适应和去神秘化的教学程序。没有人-如果不是媒体-告诉他们人工智能的机会。他们觉得没有必要实施，而应该实施。但是盲目的信任也是不可取的:算法有弱点，在开明的使用中必须知道并牢记在心。

人工智能是一个真正的机会，可以腾出医疗时间，以重建与患者的关系。但这不会发生，除非我们解决医生适应机器学习的挑战。

![](img/3dce341c3f9b6f808f8292ebdedea382.png)

AI 会取代医生吗？我不太确定。[国立癌症研究所](https://unsplash.com/@nci?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/medicine?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片。

# 一切都是从他开始的。

艾伦·图灵，50 英镑面值的英国钞票的象征，于 1912 年 6 月 23 日出生于伦敦。经过多年对数学和密码学的研究，他在第二次世界大战期间以一种特殊的方式做出了贡献:由于他出色的算法技能，他在解密 Enigma(德国军队用来加密通信的机器)中发挥了重要作用。战后，他致力于一个非常特别的想法:建造一个人造大脑。那是计算机的开端。

因此，他参与了对人类智能进行数学建模以创造人工智能的可能性的新辩论。为了测试模型，他提出了著名的图灵测试。出版于 1950 年(2)，它包括让一个人与计算机或另一个人进行盲目的讨论。如果它不能区分计算机和人类，计算机就通过了测试。在这篇文章发表近 70 年后的今天，计算机在这项测试中表现非常好，这项测试现在被认为是相对基础的。事实上，他们能够在大多数棋盘游戏中击败人类(3)，以无与伦比的准确性描述图像(4)，创作令人钦佩的艺术作品([见此处](/gangogh–creating–art–with–gans–8d087d8f74a1, 2017.))，等等。虽然和 AI 本来的意思差了很多，但这是他们的叫法。

但是这个术语是什么意思呢？很少有人能准确说出。定义不明确，最重要的是，远远没有达成共识。[维基百科](https://en.wikipedia.org/wiki/Artificial_intelligence)将人工智能定义为“机器展示的智能，与人类和动物展示的自然智能形成对比”。这也许是最接近一般观点的定义。这一定义的原因是非常历史性的。事实上，在图灵和达特茅斯会议的时代，目标是模拟和复制人类智能。然而，今天以 AI 的名义开发的工具却大不相同。他们几乎完全依赖机器学习技术。

机器学习是统计学的一个特殊分支。以一种(非常)简化的方式，ML 集合了允许创建一个数学函数来模拟某个行为的方法。回归、随机森林、提升梯度、神经网络等等，都是机器学习的一部分。

深度学习(DL)也是机器学习的组成部分之一——尽管它是一个多次辩论的主题。需要注意的是，深度学习是基于更复杂的神经网络，离基本的统计学习还很远。这伴随着对数据的更大需求和对计算能力的增加的需求(7)。

因此，我们听到/看到/读到的“人工智能”主要(但不完全)仍然是机器学习，这是一种产生具有多种用途的算法的数学方法:预测模型(如何完成时间序列)和识别工具(如何分割图像)是两个很好的例子。该算法从输入和输出数据中找到相关性。这些相关性允许算法找到与新输入相关的输出。直到今天，所提出的算法在给定的任务中是相对专门的。一般来说，算法越是特定于任务，它们的性能就越好(3)。因此，在这个模糊和不具体的术语背后，只隐藏着计算机工具，这些工具对一个给定的问题提供一个有误差区间的答案。在医学中，最终与成像工具或听诊器相关的技术工具。

然而，人工智能引起的反应比现代听诊器大得多。书籍、推文、纪录片、文章等。，从极端的铺张浪费到对大众不太有用的技术理性。不信任，恐惧，有时拒绝，或者，在另一个极端，坦率的乐观或不合理的信任。近年来，夸张的反应层出不穷。流行文化，往往非常误导，在这里扮演着不可低估的角色。无论是通过电影(终结者，黑客帝国等。)或者书籍(生活 3.0，龟壳里的幽灵等。)，人工智能要么不是真的吸引人，要么就是太过了。描绘了一台希望终结(或者，充其量，奴役)人类的机器，他们强调了对人工智能资产的非常不讨好的观点。媒体，往往有偏见和/或消息不灵通，也不会更好。这已经成为人类生存的问题。如果不是，这就是一个普遍失业的问题，因为这些机器人会取代我们的工作。

![](img/9a6c710ce2804ca49c29456c547a557a.png)

这些陈述真的没有帮助。图片来自 Pixabay 的 024–657–834。

在某种程度上与工业化的连续阶段相分离的医学领域，将被这些技术彻底改变。这场革命，如果没有正确的解释和伴随，就有被误解甚至拒绝的危险。因此，有必要对这个问题感兴趣:医疗保健界如何积极地利用机器学习工具？这是这次反思的目标。

# 但是到底什么是机器学习呢？

谈论一项技术而不解释它是很有可能的。然而，在机器学习的情况下，最好用几行文字来解释它的基本原理。

ML 是统计、优化和算法工具的集合。为了深入理解它们，有必要深入研究作为整体基础的数学理论:从矩阵计算到局部梯度和最小值的概念，包括主要的统计原理和不同的定律。但这不是重点，除非你想成为数据工程师或者数据科学家。

作为(未来的)健康专业人士，对这个术语是什么有个直觉就够了。直觉很简单:我们正处于一个因有果的境地。在每个 *x* (原因)，我们观察到一个 *y* (结果)。从一个极其简化的角度来看，机器学习的整个艺术就是找到一个将这种联系建模的函数，如此精确，以至于如果用一个新的 *x* 来呈现它，这个模型可以提供一个连贯的 *y* 。就是这样！

我们注意到模型的构建至少包括两个阶段:一个训练阶段(我们在数据上训练一个算法，我们先前收集的 *x* 和 *y* )和一个测试阶段(我们为算法提供一个 *x* ，我们期望一个正确的 *y* )。数据量的重要性很容易理解:向算法提供的训练数据越多，它将找到越多的链接，因此它将被更好地构建(8)。

因此，AI 或 ML 的含义是将一个 *x* 连接到一个 *y* 的函数。这个函数可能或多或少地复杂，或多或少地忠实反映现实。它可以对应于线性或逻辑回归——一个不太复杂的模型，几个世纪以来一直是手工操作的。它也可以基于更复杂的模型，如[支持向量机](/support-vector-machine-introduction-to-machine-learning-algorithms-934a444fca47)(支持向量机)或[随机森林](/understanding-random-forest-58381e0602d2)。

最复杂的模型，有时复杂到我们不知道如何确切地解释结果(因此有了“黑盒”这个不好听的术语)，是神经网络，例如 [CNN](https://medium.com/@RaghavPrabhu/understanding-of-convolutional-neural-network-cnn-deep-learning-99760835f148) (卷积神经网络)(递归神经网络)或[甘](/what-is-a-gan-d201752ec615)(生成对抗网络)。

但即使在计算能力或使用的模型之前，最具决定性的成功因素是数据。基本元素，为推理服务的基本砖块。一个恰当地收集和公正的数据，良好的结构和大量，是一个巨大的资产。问题是，很难有干净和公正的数据。此外，这是很难得到足够的。

事实上，一个从零开始在图像上训练的经典深度学习模型需要超过一百万个例子(一个例子是输入和输出， *x* 和 *y* 在一起)。这是数百千兆字节的数据，很难在本地计算机上运行。

这就是为什么我们看到了云服务的出现。这些可在互联网上获得的平台，使得以可承受的价格使用大的计算能力成为可能。这些平台主要由网络巨头托管:谷歌([谷歌云](https://cloud.google.com/))、亚马逊([亚马逊网络服务](https://aws.amazon.com/))、IBM ( [IBM 云](https://www.ibm.com/cloud))、微软([Azure](https://azure.microsoft.com/))……但这种使用也伴随着伦理问题(谁拥有数据？)，信任(怎么用？)和主权(这些公司都是美国的)。

今天，所有这些创新都是由一个非常活跃的生态系统驱动的(9)。从未有过如此多的领域投资、发表论文或成立公司。然而，值得强调的是，这种生态系统可能会误导人，或者适得其反。事实上，许多论文被拒绝，因为缺乏统计和方法的严谨性。并非所有创立的企业都是相关的；他们中的大多数很快就用完了现金。所有这些公司都是投资的温床。它们是如此之大，以至于人们担心会发生金融危机。

# AI 如何帮助医生？

在医学院，符号学很快就被纳入课程。临床检查是其中很大的一部分，还有听诊，今天依靠听诊器。这个强大的工具，大约在 1816 年由拉埃奈克博士创造，是临床实践的必备工具(10)。它使用了人类的一种能力——听觉——并为医生提供了一个了解心肺世界的机会。

在许多方面，人工智能并不比听诊器复杂。它的主要影响是促进任务，当然是智力，但重复，低附加值的病人护理。这些斑点可以分为三大类。

![](img/be6c2f689fd8ffe0de42c7b636c7c0fd.png)

人工智能只是一个现代的、适应性强的、自主的、数字化的听诊器。Marcelo Leal 在 [Unsplash](https://unsplash.com/s/photos/medicine?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片。

第一，分析功能。这是一个关于记忆的数据，这是一个非常标准化的任务。生物学、影像学、病理学是产生报告的医学行为，完整阅读这些报告需要一段时间，但这并不十分必要。

然后，进行诊断、远程监控和对处于危险中的患者的监控。大多数历史诊断方法都是基于统计的。比回归更先进的新模型可以提高灵敏度和特异性。如今，对患者的随访是有限的:电话、预约、电子邮件，都需要医生或管理人员的帮助——他们的帮助越来越少。算法不知疲倦。他们可以跟踪，交换，跟踪病人，编程后自动跟踪。与连接的对象集成，他们可以跟踪身体活动和睡眠周期，并实时控制心率、血压和氧饱和度等生命体征。所有这些数据都可以汇总并呈现给医生。实际上，这种装置已经被食品药品监督管理局(FDA)批准(11)。

最后，在成像和信号处理中的病理检测。深度学习包括各种类型的神经网络(CNN ),专门用于表征体积数据，如图像。这些神经网络，在 CT 扫描或 MRI 上训练和评估，有相当可敬的结果，有时甚至与放射科医生竞争(这是一个非常错误的评估方法)。在其他类型的成像中也是如此。此外，我们强调，这绝不是小事，他们接受的识别具体和精确案例的训练越多，他们就越好。信号处理也是如此。

无论是为了分析脑电图，检测睡眠呼吸暂停还是识别心律失常，算法都是非常有效和有趣的帮助。为什么？克服缺乏时间和专业知识的问题，或者仅仅是为一个复杂的案例带来新的观点。算法可以为需要它们的临床实践提供支持。

所有提到的任务都是医学上的。但我们不要忘记，行政时间也与医疗专业有关。这些任务会激发人们对自动化的强烈渴望。所有这些释放出来的时间都不会是自由时间。医患关系是医疗成功的一大挑战。长时间呆在病床边对修复这种对医疗实践至关重要的联系是一笔财富。因此，有必要仔细关注被释放时间的用途:所有这些都不是为了治疗更多的病人，而是一个更好地治疗他们的机会。

# AI 将是医学的机会，只有医生和算法合作。

不可能有完美的算法，因为不可能在所有可以想象的环境中测试一个算法。根据这一观察，让算法和医生相互竞争似乎不合适，在科学上也不可接受。这不应该是这样的。

虽然算法在一般情况下的执行速度和精度方面非常有效，但医生在特殊情况下是无与伦比的，这些情况下，在高斯曲线的极端情况下，离开了规范。许多研究表明，在算法和医生的合作中，诊断的准确性是最好的。ML 仍然是一个工具。增强型听诊器。

然而，如果一个维护良好的听诊器总体上是可靠的，那么算法就不一定了。

# 一些弱点。

一个算法是它被训练的数据的反映。

当这些数据有偏差时，可能会给现实世界的实施带来问题。有着良好批判意识的人通常会认为训练数据不能完全反映真实生活。事实上，这种情况几乎从未出现过。根据定义，除非上下文状态不变，否则历史数据不能等于未来数据。除了时间偏见之外，地理和种族偏见也经常成为问题。选择偏见和社会经济偏见也可能存在。另一个问题是数据的方差。方差太大的算法将无法正常执行:结果将无法重现。

数据的质量和数量是两个基本要素。但是你还是要知道如何正确使用。构造算法的一个主要挑战是避免过拟合和欠拟合的问题。如果算法与数据匹配太多，这就是过拟合:算法用心学习数据。在训练期间，该算法将具有非常好的性能。然而，在现实生活中，它会产生非常糟糕的结果，因为它仍然过于忠实于训练数据。装配不足是相反的问题，并且在实践中导致相同的问题。这给我们带来了评估算法的挑战，这是一件非常复杂的事情(13)。为此，有许多方法，每种方法都有优点和缺点，但重要的是要记住，没有完美和整体的方法:算法永远不会完美。

# 那现在怎么办？

对人工智能的排斥会对医学产生短期、中期和长期的负面影响。

人工智能将在未来的病人护理中发挥重要作用，无论是在诊断阶段，治疗阶段，甚至是在管理过程中。对于医生来说，这是一个学习如何使用这种新工具为病人腾出更多时间的真正机会。但是适应这种新工具是一种强烈的无与伦比的需要。高中对算法的介绍还不够。在医学领域，揭开这些工具的神秘面纱是一个远未实现的目标。没有人告诉我们这是什么。没有人告诉我们如何使用它。

从我的角度来看，作为一名接受过数据科学培训的医学住院医师，文化适应的挑战至关重要:它的成功将取决于算法在真实临床世界中的实施。

此外，GAFA(美国数字巨头:谷歌、亚马逊、脸书和苹果)或 BATX(中国数字巨头:百度、阿里巴巴、腾讯和小米)的数据中心不应该是托管健康数据的唯一可能性。今天情况不再如此，我们必须鼓励这种情况。

医院、诊所和图书馆中的数据极其稀少，管理不善，缺乏维护，而且很大程度上没有得到充分利用。它的研究用途是无限的。不同参与者之间的互操作性是乐观者的梦想，悲观者的乌托邦。

我们不能隐瞒，每次技术革命的目标都是一样的:通过技术提高人的能力。在医学上，越早越好。

# 感谢

我们要感谢跨学科研究中心对我们的欢迎，以及它推动创新和批判性思考的生态系统。也要感谢组织会议带来了对这一问题的不同看法，包括与 Marie-Pauline Talabard、Simon Jégou、Cédric Villani、Henri Bourdeau、Bertrand Nordlinger 博士、Clément Goerhs 博士、Luc Julia、Romain Pommier、Stéphanie Allassonnière 和 Laurent Alexandre 博士的会议。

非常感谢 Cloé Brami 博士和 Olivier Bory 所做的一切。

当然，我没有任何利益冲突。

# 参考

1.  A.霍奇斯。艾伦图灵:谜。2012.
2.  艾伦·m·图灵。计算机器和智能。头脑，49:433–460，1950 年。
3.  托马斯·休伯特等人。一种通用的强化学习算法，可以掌握国际象棋、日本象棋和自我游戏。《科学》,第 1140-1144 页，2018。
4.  穆罕默德·马吉德等人。使用卷积神经网络的医学图像分析:综述。医疗系统杂志，2018。
5.  肯尼·琼斯。Gangogh:与 gans 一起创造艺术。走向数据科学
6.  维基百科关于人工智能的页面
7.  林永硕律师事务所。医学生应该对医学中的人工智能有哪些了解？J Educ 评估健康教授，2019 年 16:16–18。
8.  Ajibuwae & Al。垃圾邮件过滤的机器学习:综述、方法和开放研究问题。赫利永，2019 年 5 月。
9.  霍尔登·佩奇。人工智能市场正在增长，但很难确定增长速度有多快。https://news . crunchbase . com/news/the-ai-market-is-growing-but-how-fast-is-tough-to-pin-down/，2019。
10.  心脏听诊的前 200 年和未来展望。j 多碟健康 c，12:183–189，2019。
11.  莱斯菲尔德马等人。使用 apple watch 监测心率的临床价值。Cardiol Rev .第 60–62 页，2019。
12.  奎师那 KR & Al。医患关系之谜。印度精神病学杂志，(增刊 4):S776–S781，2019。
13.  尼泊尔陆地卫星 8 号场景地表水提取的机器学习算法评估。传感器(巴塞尔)，2019。