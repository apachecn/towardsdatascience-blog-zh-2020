# 利用人员流动数据计算集水区

> 原文：<https://towardsdatascience.com/calculating-catchment-with-human-mobility-data-efd08e2d20f6?source=collection_archive---------24----------------------->

## 利用人员流动数据识别潜在客户

集水区(即贸易区)是零售商、批发商和其他商业场所开展大部分业务的地理区域。正确计算它们对于零售和房地产等行业至关重要，因为它们使组织能够更好地了解客户并制定适当的业务战略。

![](img/136136a647b23ae880e932553f25c429.png)

计算集水区的技术有很多，从环形贸易区、等时线、重力模型，到包含特定位置变量的更复杂的技术。所选择的技术通常取决于可用的信息和数据，以及不同技术中可用的专业知识。

![](img/fb92ba15ce8dfbf5bae935da45ff7217.png)

*图 1。不同的集水区取决于技术:左边是环形贸易区(15 公里缓冲区)，中间是 20 分钟车程等时线，右边是基于流动性数据的集水区。*

当一家新店开业时，由于缺乏可用数据，很难知道哪些顾客会来这家店，或者他们来自哪里。在没有这些数据的情况下，最常见的方法是计算目标位置周围的缓冲区或等时线，但这种方法缺乏精度，可能导致不可靠的结果。

例如，对两个位置采用相同的时间等时线，而不考虑它们周围的人口密度，这肯定会导致不可靠的结果。这是因为居住在低密度地区的人们通常比居住在高密度地区的人们走更长的距离去购物。在这里，我们旨在使用人员流动数据作为潜在客户的代理，计算可靠的潜在集水区。

获得的结果表明，传统的方法，如等时线或缓冲区，无法捕捉到访问特定位置的人实际上来自哪里。它们不能像使用人员流动数据那样灵活地建立目标集水区；例如，能够计算工作日和周末游客的不同集水区。

# 人类移动数据

我们方法的基础是使用来自[沃达丰分析](https://carto.com/solutions/vodafone-analytics/)的人员流动数据。该数据提供了对访问覆盖整个研究区域的任何 250m x 250m 网格单元的人数的洞察。沃达丰对网络中测量的数据进行匿名化、聚合和外推，以提供代表整个国家和国际人口的见解。

此外，该数据还提供了根据到目标像元的距离在不同级别聚集的访问者的来源。对于来自同一个城市的游客，也在 250m x 250m 像元级别提供起点；对于来自同一省其他城市的访问者，访问在城市一级进行汇总；对于来自其他省份的访问者，访问是在省一级进行汇总的。虽然它也提供了，鉴于这项研究的特点，我们不打算考虑来自不同国家的游客的来源。

此外，这些数据可以按活动类型(家庭/工作)、星期几和一天中的时间(上午/下午/晚上)进行分类。数据也可以按社会人口变量分类:年龄范围、性别和经济状况。

为了这个用例的目的，我们在西班牙的塞维利亚市选择了一个目标位置来展示这个方法。下面的地图显示了游客的来源地。

图二。这张 choropleth 地图显示了按来源地划分的游客数量，并按该来源地的总人口进行了标准化。

我们还使用 Unica360 的人口统计数据来标准化访客数据。Unica360 的数据是在 100m x 100m 的网格中聚合提供的，除其他变量外，还包括人口、按年龄范围划分的人口以及家庭数量。数据聚合被升级以适应沃达丰的 250m x 250m 单元网格，应用面积插值。

# 定义我们的集水方法

计算集水区的第一个想法是为每个起点-目的地对计算一个指数，该指数衡量目的地相对于起点的游客吸引力潜力。这里，目的地被理解为包含新商店位置的网格单元。

该指数将被定义为:

![](img/0bf3ec39453273a8302080abbbf593d4.png)

基于该指数，我们将通过选择具有最高指数值的源来计算每个目标像元的集水区，该值占该目标像元总访问量的 70%。

然而，由于来自其他城市和省份的游客数量在小区一级无法获得，因此需要采用一种新的方法来调整第一个想法，以便在不同的汇总级别(小区、城市和省份)比较游客数量。

这种新方法有两个主要步骤:

1.  查找覆盖至少 80%目标像元访问者的起点的最小等时线(基于乘车旅行时间)。
2.  通过在先前的源中选择索引值最高的源(占该目标像元总访问者的 70%)来缩小集水区的大小。

# 寻找最小等时线

如前所述，来自同一省其他直辖市和其他省份的访问者分别在直辖市和省一级进行汇总。等时线允许我们只考虑在一个直辖市/省内那些(在时间上)更接近目标像元的区域。所开发的方法计算越来越大的等时线，直到覆盖 80%的目标像元的总访问者。

为了计算来自一个等时线与一个省(或直辖市)的交叉点*nvisitorsection*的游客数量，以下步骤如下:

1.  首先，使用 250x250m 网格单元的人口统计数据计算居住在交叉点的省人口比例，*pctpupulationintersection*
2.  其次，从路口过来的游客数量用下面的公式计算。这个公式是基于[托布勒地理定律](https://en.wikipedia.org/wiki/Tobler%27s_first_law_of_geography)和使用经验数据找到一个粗略的拟合。

![](img/8e4227b8a85661ca5a9addec239befd6.png)![](img/ca773705d6e74c6f98d5f0acb048258c.png)

*图 3。转换功能分配更多的游客到更近的地方。*

函数√将更多的访问者分配为来自该省内距离目标小区较近的区域(因此，较少的访问者分配到较远的区域)。从图 3 中可以看出，该函数如何将来自一个省/市的 70%的访问者分配到一个仅包含 40%人口的区域，但该区域更靠近目的地小区。同样，我们应用这个公式是基于这样一个假设，即住得离目标小区越近的人越有可能访问它。更复杂的模型可以给出更好的预测。

# 游客来源的选择

一旦有了最小等时线，下一步就是计算最小等时线内每个原点的索引值，定义如下:

![](img/8886e0133155560b87a10617bfc99c28.png)

该指数是使用来自每个起点的标准化访客数量*norm _ nvisitorsection*计算的。归一化是通过除以交叉点内人口像元的数量来完成的， *npopcellsIntersection* ，即访问者的数量均匀分布在交叉点多边形内的所有人口像元中。

![](img/6142e09bc150110e8b3d43ff75d67489.png)

这种标准化允许对来自同一城市牢房的来访者与来自其他城市和省份的来访者进行比较。通过选择占目标像元总访问者 70%的具有最高指数值的起点，我们可以获得其估计的集水区。

# 处理和可视化结果

下图显示了计算最小等时线所需的三次迭代，该最小等时线包含塞维利亚市目标像元中至少 80%的总访问者。

![](img/ae609aff0bd501ae1aa6cbf2302ac17d.png)

*图 4。这个可视化展示了达到一个单元的总访问者的 80%所需的三次迭代。颜色显示了作为归一化访问和质心之间距离的函数定义的索引值。*

一旦找到最小等时线，并为每个原点计算指数，我们就可以构建集水区。最后，集水区的凹壳(又名[阿尔法形状](https://en.wikipedia.org/wiki/Alpha_shape))被计算为具有可管理的连接区域。为了计算凸包，我们使用了 Python 库 [alphashape](https://pypi.org/project/alphashape/) 。

下图显示了塞维利亚的目标像元的原始集水区及其凹形船体。

![](img/96fbe797ca98d6f4d9d5145e54c592b3.png)

*图 5。该可视化显示了单元的原始集水区及其凹面外壳。*

如果我们将刚刚获得的集水区与 15 公里缓冲区和 20 分钟车程等时线进行比较，我们可以看到它们看起来非常不同。下图显示了三个集水区以及每个集水区包含的人口像元。

![](img/9e851dfce0e38a23749032a2c6323f07.png)

*图 6。该可视化显示了整个博客帖子中比较的三个集水区及其包含的群体单元。*

从这个比较中，我们可以看到等时线是如何向北和向西扩展的，错过了城市南部的一个非常重要的城区，事实上，该城区是目的地单元的一个非常重要的游客来源，如图 4 所示。在最小等时线过程的每一次迭代中，可以看到在城市的南部有一个多边形，对应于这个城区的游客数量非常高。该区域仅部分包含在缓冲集水区中，完全包含在我们刚刚使用人员移动数据构建的集水区中。

# 使用移动性数据定制集水区

如上所述，Vodafone Analytics 数据可以按活动类型(在家/工作)、星期几和一天中的时间(上午/下午/晚上)等变量进行分类。这提供了很大的灵活性，根据业务部门甚至用例，使用这些信息来构建定制的汇水区可能会很有趣。一个例子是为工作日和周末建立不同的集水区。

在下图中，对于同一个目标位置，我们使用所有访问构建的集水区(左)，仅使用周一至周四的访问(中)，以及仅使用周五至周日的访问(右)。非常有趣的是，人们在周末会比平时走更远的路。

![](img/8b61a269494804ee9fd796c7d763e2cc.png)

*图 7。该图显示了目标位置的集水区，从左至右考虑了所有访问、周一至周四的访问以及周五至周日的访问。原始集水区在最上面一行，其对应的 alpha 图形在最下面一行，就在它们的正下方。*

这种粒度级别允许更强大的业务洞察力。使用这种方法的房地产公司可以向潜在的投资者提供更多的细节。对于零售商来说，这种更准确的收集可以为员工和位置管理、库存等决策提供信息。

例如，如果我们更深入地分析这最后一个层次的洞察力，我们可以看到使用工作日访问构建的集水区非常符合 20 分钟车程等时线，而基于周末访问构建的集水区则不符合(见下图)。这些信息可以用来确定投放广告的正确位置，或者根据一周中的不同日子制定不同的营销策略，因为客户来自不同的地方。

![](img/96cb8de2377b08a6e02375d4b3551338.png)

*图八。该图用橙色显示了工作日访问(左)和周末访问(右)的集水区，并与 20 分钟车程等时线(紫色)进行了对比。*

沃达丰分析数据也可以按社会人口统计变量分类:年龄范围、性别和经济地位。这允许集中于目标客户简档的集水区的构建。这可以在决定商店形式和零售类别时提供更深入的见解。

# 更深入地了解集水区的人员流动情况

了解和理解一家公司的大部分业务来自的领域的特征对他们的成功至关重要。当开始一项新业务或扩大现有业务时，历史数据的缺乏使得知道客户将来自哪里非常具有挑战性。

人类移动数据，加上其他[位置数据流](https://carto.com/platform/location-data-streams/)，可以在应对这一挑战时发挥作用，帮助企业从竞争对手中脱颖而出。

*本文原载于* [*CARTO 博客*](https://carto.com/blog/calculating-catchment-human-mobility-data/) *。这项工作是与Á·阿尔瓦罗·阿雷东多一起完成的。*

*特别感谢*[*Mamata Akella*](https://twitter.com/mamataakella?lang=en)*，CARTO 的制图主管，对她在本帖地图创作中的支持。*