# 科莫说，21%的纽约居民患有新冠肺炎。这是正确的吗？

> 原文：<https://towardsdatascience.com/cuomo-says-21-of-new-york-residents-have-had-covid-19-is-this-correct-23e8a63d2045?source=collection_archive---------60----------------------->

## 处理统计数据时因果推理的案例研究

*撰稿*[](http://wenhaoz.io)**，编辑* [*拉明·拉梅扎尼*](http://web.cs.ucla.edu/~ramin/) *。—2020 年 5 月 4 日**

*![](img/262e7091d54e2f929a42b87ed8140dd3.png)*

*如果被选择偏差污染，数据可能会欺骗你。我们的分析需要超越数据本身，调查数据生成/收集过程。图片:[来源](https://www.furman.edu/covid-19/wp-content/uploads/sites/177/2020/03/CoronaVirusHeader-Final-3-1536x647.jpg)*

*“选择偏差”是由优先排除数据中的样本引起的[1]。它是验证统计结果的一个主要障碍，在实验或观察研究中几乎检测不到。这一切都始于我们通常在科学研究中使用样本群体，并假设样本代表总体(统计学方法)。让我们从一个真实的例子开始。*

*在新冠肺炎疫情危机期间，一项全州范围的研究报告称，21.2%的纽约市居民已经感染了新冠肺炎病毒。该研究对全州 3000 名纽约居民在杂货店和大卖场进行了抗体测试，以表明某人是否感染了该病毒。Cassie Kozyrkov【3】认为这项研究可能受到选择偏差的污染。假设是，研究中的队列主要偏向于高风险人群和已经感染病毒的人群。总人口的大部分可能包括规避风险和谨慎呆在家里的人；这些人被排除在研究样本之外。因此，报告的死亡人数(即 21.2%)很可能是夸大的。Cassie Kozyrkov 在解释这项研究中选择偏差的原因方面做了惊人的工作[3]。但在这里，我们试图调查一个更通用的方法来当场选择偏差问题。*

*幸运的是，我们有因果推理的工具。因果推断要求我们在分析数据时做出某些似是而非的假设。数据并不总是完整的，也就是说，它并不总是能说明全部情况，仅从数据得出的分析结果(例如，虚假关联)往往会产生误导。例如，人们可能会发现吸烟的人可能会患肺癌，同时有黄色的指甲。如果我们发现这种联系(肺癌和黄指甲)很强，我们可能会得出一些错误的结论，即一个导致另一个。*

*![](img/dcb337c678c28eefd74a5be34f4d814b.png)*

*图片:[来源](https://miro.medium.com/max/1000/1*ZhYNqU2y96_f3QkWq9oiWQ.jpeg)*

*回到我们的新冠肺炎故事，在抗体测试研究中我们可以做出什么因果假设？让我们考虑图 1，其中以下每个假设代表一个优势。*

*I)我们知道，如果我们做相关的测试，将会发现抗体。*

*ii)感染过新冠肺炎病毒并存活下来的人会产生该病毒的抗体。*

*iii)敢于冒险的人更有可能去户外并参与测试研究。*

*iv)为了在图表中突出样本群组和总体人口之间的差异， [Elias Bareinboim](http://elias bareinboim columbia) 提出了一个假设变量 S(代表“选择”)。图 1 中方框内的变量代表两个群体不同的特征。您也可以将 S 视为包含/排除标准。变量 S 具有来自变量“冒险”和“携带病毒”的输入边。这意味着样本队列和总体人群在这两个方面有所不同。*

*![](img/3d8824a0161b0a4c4e274184b2ee4dbb.png)*

*图 1:说明选择偏差场景的图形模型。变量 S(方形)是一个产生差异的变量，它是一个假设变量，指出两个群体的不同特征。*

*现在，我们已经将我们的假设编码成一个透明而简单的图表。你可能想知道为什么我们要费尽周折制作这个图表？这对我们识别选择偏差甚至去偏差过程有什么价值？*

*好问题。让我们从这样一个问题开始:它如何帮助我们找到识别选择偏差的共同模式/原则？*

# *用因果图识别选择偏差*

*识别选择偏差的几个快速提示:1)在原因变量和结果变量之间的后门路径上找到任何碰撞器变量，2)当你的数据收集过程以这些碰撞器变量为条件时，选择偏差发生[1]。注意，这些提示是发现选择偏差的充分条件，但不是必要条件。我们所说的条件作用是指只考虑一个变量的一些可能性，而不是全部。*

*技巧 1 中的后门路径是指原因变量(COVID 测试)和效果变量(抗体%)之间的任何路径，带有指向原因变量的箭头([4]，第 158 页)。在我们的例子中，唯一的后门路径是“新冠肺炎测试←冒险→ S ←携带病毒→抗体%”。如果我们封锁每一条后门路径，就会消除虚假关联。我们如何知道后门路径是否被阻止？*

*Judea Pearl 在他的书[4]中谈到了 3 条规则，告诉我们如何阻止后门路径和虚假的关联流。如果你对这 3 个规则的完整数学证明感兴趣，请参考[5]*

*A)在链式连接中，A→B→C，以 B 为条件阻止关于 A 的信息到达 C，反之亦然。*

*B)在一个分叉或混杂连接中，A←B→C，以 B 为条件阻止关于 A 的信息到达 C，反之亦然。*

*C)在对撞机中，A→B←C，正好相反的规则成立。当没有以 B 为条件时，A 和 C 之间的路径被阻塞。如果我们以 B 为条件，则该路径是畅通的。请记住，如果这条路径被阻塞，A 和 C 将被视为相互独立。*

*有了这样的背景知识，我们知道再看我们的图解。我们现在看到，后门路径上有 3 个基本组件:1)一个分叉“新冠肺炎测试←高风险→S”；2)一个对撞机“高风险→ S ←携带”；3)另一个叉“S ←携带病毒→抗体%”。现在我们看到，如果我们不在碰撞器中对变量 S 进行条件运算(规则 c)，这个后门路径就被阻塞了。如果我们以变量 S 为条件(例如，set S={high risk，had virus })，后门路径将被打开，并在您的抗体检测结果中引入虚假关联。*

*现在我们认识到，如果我们在原因→结果之间的后门路径上以碰撞子为条件并打开后门路径，我们将遇到选择偏差问题。有了这个结论，我们可以很快确定我们的研究是否有选择偏差的问题。当图形复杂时，这种识别过程也可以自动化。所以，我们把这种判断交给算法和计算机。希望您在这一点上确信，使用图形模型是识别选择偏差的更通用和自动化的方法。*

# *do-calculus 无偏估计*

*为了测量两个变量 X 和 Y 之间的因果关系，Judea Pearl 引入了 do-calculus 符号[4]。例如，P(Y|do(X=x))表示当每个 X 固定为值 X 时，从 X 到 Y 的因果效应.注 P(Y| X=x)反映了 Y 在 X 值为 X 的个体中的总体分布.后者只能表示 Y 与 X 之间的关联.如果你对更多细节感兴趣，请参考([6]，53 页).*

*现在我们感兴趣的是“新冠肺炎试验→抗体%”之间的因果估计，P(抗体|do(试验))。换句话说，如果我们测试群体中的每个人，因果效应代表抗体发现的可能性。我们的读者可能想知道 do-calculus 在这一点上是否有意义，但是我们如何计算和删除 do-operator 呢？*

*do-calculus 只有 3 个规则来减少我们熟悉的计算。下面三个规律的完整证明可以参考[7]。*

*a)当我们观察到一个与 Y 无关的变量 W 时，那么 Y 的概率分布不会改变，*

*P(Y|do(X)，Z，W) = P(Y|do(X)，Z)。*

*b)如果一组 Z 个变量阻塞了从 X 到 Y 的所有后门路径，那么以 Z 为条件，do(X)等价于 see(X)，*

*P(Y|do(X)，Z) = P(Y|X，Z)。*

*c)如果从 X 到 Y 没有因果路径，那么*

*P(Y|do(X)) = P(Y)。*

*在我们的例子中，*

*![](img/c61d31dd07d0ba562411a7860f4d7224.png)*

*我们可以看到，在方程的最后一步，我们需要在研究中测量四个概率项，以获得无偏估计。如果我们假设封闭世界(风险= {高，低}，病毒= {真，假})，这意味着我们需要测量每一个分层的群体。在报告[1]中，他们报告的数值是 P(抗体|测试，风险=高，病毒={。})这与真正的因果效应相比是有偏差的。*

*现在我们已经看到，do-calculus 可以帮助我们确定我们需要哪些部分来恢复无偏估计。希望您在进行因果推理时，对图形模型结合 do-calculus 的强大功能印象深刻。*

# ***参考文献***

*[1]埃利亚斯·巴伦博姆和朱迪亚·珀尔。控制因果推理中的选择偏差。《人工智能和统计》，第 100-108 页，2012 年。*

*[2]杰里米·伯克。cuomo 说，一项全州范围的抗体研究估计，2020 年，21%的纽约市居民患有冠状病毒。*

*[3]卡西·科济尔科夫。21%的纽约市居民真的感染了新型冠状病毒吗？, 2020.*

*[4]珀尔、朱迪亚和达纳·麦肯齐。*原因之书:因果的新科学*。基础书，2018。*

*[5]盖革、丹、托马斯·维尔马和朱迪亚·珀尔。"识别贝叶斯网络中的独立性."网络 20.5(1990):507–534。*

*[6]珀尔、朱迪亚、玛德琳·格雷穆尔和尼古拉斯·朱厄尔。统计学中的因果推断:初级读本。约翰·威利父子公司，2016 年。*

*[7]黄、李一民和马可·瓦尔托塔。"珀尔的干涉计算完成了."arXiv 预印本 arXiv:1206.6831 (2012)。*