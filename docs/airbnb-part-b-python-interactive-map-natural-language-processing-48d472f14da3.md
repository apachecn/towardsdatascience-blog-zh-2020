# Airbnb-B 部分(Python-交互式地图，自然语言处理)

> 原文：<https://towardsdatascience.com/airbnb-part-b-python-interactive-map-natural-language-processing-48d472f14da3?source=collection_archive---------24----------------------->

## 通过与华盛顿 DC 的对比研究、回归模型、交互式地图
和自然语言处理来分析西雅图的 Airbnb 情况。向市议会和旅行者提出建设性的建议

![](img/11c4db8bf269e2ea580a30f205a3c92d.png)

**西雅图的可爱明信片(图片由作者提供)**

> 来自[甲部](https://medium.com/@tuonggreenager/airbnb-part-a-python-visualization-comparative-study-regression-7466c0cb5a1d)的介绍

> 自 2008 年以来，Airbnb 帮助客人和主人以更独特、更个性化的方式旅行。该公司从一个出租的充气床垫发展到价值超过 300 亿美元的全球合作，这都要归功于其精力充沛的创始人布莱恩·切斯基。2020 年应该是 Airbnb 的黄金年，因为它将上市并发行世界上最受追捧的股票。悲剧的是，冠状病毒发生了。旅游业被疫情摧毁了。Airbnb 现在面临着烧钱、愤怒的房东和不确定的未来，因为 2000 名员工可能会被解雇，还有数十亿美元的高利率债务，这些债务是为了偿还客户而建立的。[(研 2020)](https://www.wsj.com/articles/airbnbs-coronavirus-crisis-burning-cash-angry-hosts-and-an-uncertain-future-11586365860)
> 
> 尽管如此，随着六月的到来，情况开始好转。Airbnb 报告称，5 月 17 日至 6 月 3 日期间，美国房源的预订量超过了去年同期。在成功抗击病毒的国家，如德国、葡萄牙、韩国和新西兰，国内旅游也有类似的增长。像 Expedia 和 Booking.com 这样的其他公司也见证了国内度假租赁预订的激增。几个月来被压抑的需求导致夏季预订热潮，因为越来越多的人希望逃离他们的家庭冠状病毒避难所。现在，Airbnb 的房源比危机前更多，主要集中在传统的度假租赁市场，美国的顶级目的地。它们是南加州的大熊湖、田纳西-北卡罗来纳边境的烟雾山和德克萨斯州的阿兰萨斯港。[(卡维尔，2020)](https://www.latimes.com/business/story/2020-06-07/airbnb-coronavirus-demand) 尽管如此，任何反弹都来自一个非常低的基数，切茨基在 5 月份的电话会议上表示，他预计今年的收入将达到 2019 年上半年的水平。他说，今年上市仍是一个选择，但他将等待市场稳定下来，然后再做出最终决定。
> 
> 作为一名之前接受过培训、现居住在西雅图的酒店经营者，我想分两部分做一个关于西雅图 Airbnb 现状的分析项目。第一部分是对西雅图和 DC 华盛顿州两个城市的比较研究。西雅图和华盛顿 DC 地区位于美国的两端，因为不同的原因而广为人知:分别是科技和文化中心与政治中心。此外，它们拥有相似的人口规模(刚刚超过 700，000)和多个列表(8740 和 9369)。然后，在第二部分，我们将从政府立场和游客的角度更深入地了解西雅图的市场，并推荐不仅有利于 Airbnb，还有利于这座城市及其市民的解决方案

> *****************************************

在 B 部分，我们将创建一些可视化，交互式地图，并利用西雅图的 Airbnb 2020 房源数据集深入自然语言处理。除了标准库之外，我们还引入了更多专用于创建地图的库(folium，geopandas)，可视化库(plotly，cufflinks)，自然语言处理库(re，nltk)。

![](img/3739e77acf3fc1c8eec1bb1a7e3ac71f.png)

**(图片作者)**

除了主要用于分析的 listings.csv 和 listings_details.csv，我们还使用了“日历”和“review_details”数据集来帮助我们。正如我们在 A 部分提到的，列表基本上是广告的 id。2020 年 4 月，西雅图有 7237 个 Airbnb 房源。“列表”包含 15 个特征，而“列表 _ 细节”包含 96 个特征。我们没有使用所有可能不相关的列，而是有选择地加入了一些对 B 部分的分析有用的变量。我们还从“主机响应速率”功能中去掉了“%”。

![](img/74de55904fb3525315ee2f0f1884821e.png)

**(图片作者)**

# **I/** 探索性数据分析(EDA)

## **1)** **邻里**

市中心是西雅图所有商业和专业活动的中心(1250 个列表)，这解释了为什么它的列表数量在城市之外的其他街区中排名第二。西雅图市中心附近的其他地区似乎也没有那么受欢迎，因为在首都山只有 775 个房源，中心区只有 600 个，其余的都在 500 个以下。有一种理论认为，旅行者决定住在西雅图之外的原因是因为该市目前房地产价格的飙升。我们将揭示这个有趣的事实如何影响其他列表的因素，如价格和客户对 Airbnb 住宿的看法。对于交互式地图，您可以放大集群，最终找到列表的各个位置(下面是 Github 代码)

![](img/9fef40359d484f4681a1521a56531342.png)![](img/b82e7857b479463db89c77dcf9788523.png)

**(图片作者)**

## **2)** **房间类型，物业类型，&每次预订人数**

CBRE 酒店的美国研究表明，Airbnb 在西雅图约 80%的收入来自整间房屋的房源，拥有多间整间房屋房源的房东产生的收入在 2015 年至 2016 年间几乎翻了一番。[(西雅图市议会，2017)](https://www.seattle.gov/Documents/Departments/Council/Issues/RegulatingShortTermRentals/Regulating-Short-Term-Rentals_Policy-Brief_2017-04.pdf) 商业企业喜欢利用在线租赁平台来营销不同位置的多个单元，这可能会加剧西雅图的住房危机定时炸弹，正如你将在本报告稍后看到的那样。不幸的是，2020 年的情况不会更好，整个家庭/公寓占据了绝大多数房源(总共 5700 个)，比私人房间高出 3 倍。然而，西雅图迟迟没有通过任何实质性的法律，不像纽约，纽约积极禁止任何房屋出租超过 30 天，直到 2017 年。[(道尔顿，2017)](https://techcrunch.com/2019/12/09/airbnb-zeus/)

![](img/216bc6cd6781a08191cba76a8bd70dab.png)

**(图片作者)**

值得注意的是，有不同的财产清单，但并不是所有的都广受喜爱。为了排除不流行的物业类型，我们创建了一个名为“total”的附加列，根据房间类型统计每种物业类型的列表，并选择超过 100 个的列表。之后，我删除了“总计”列以获得正常结果。房子和公寓是最常见的财产类型。与公寓相比，房屋似乎是整个家庭/公寓列表中不太受欢迎的财产类型，但当涉及到私人房间租赁时，它们更受欢迎。

![](img/17029a7f4ef6e4cba16234002b4b66c2.png)

**(图片作者)**

一般来说，大多数房源通常喜欢接待少于 5 名客人，其中大多数是 2 人(超过 2700 个房源)。然而，有趣的是，一个 6 人的聚会可以很容易地找到一个合适的过夜场所。这是因为与阿姆斯特丹等其他城市不同，出于对可能的噪音投诉或火灾隐患的担忧，西雅图没有短期租赁的最大容量限制为 4。因此，如果你想开派对，西雅图是最好的选择。

![](img/e6dbb519ce9518c508b79884120d7f01.png)

**(图片作者)**

# **二/给西雅图市长的建议**

众所周知，Airbnb 被指责加剧了全球许多城市的经济适用房危机。[(沙夫罗斯，2016)](https://www.governing.com/columns/public-money/gov-airbnb-affordable-housing.html) 。为了防止这种情况发生，西雅图的财政和行政服务部强制要求每一个 Airbnb 主机在 2019 年 12 月之前获得短期租赁运营商的许可证。 [(Airbnb，2020)](https://www.airbnb.com/help/article/869/seattle-wa) 许可证约为 75 美元/单位，每年更新一次。每个短期合同允许您经营最多两个住宅单元:

*   ***主要居住地:*** “机动车登记、驾驶证、选民登记或其他此类证明文件记载的人的经常居住地”
*   ***第二居所* :** 度假屋或第二居所

然而，该指南并不是对所有房源都强制执行，对最大单元数量有有限的例外，包括 2017 年 9 月 30 日之前合法经营的短期租赁的一些例外。值得注意的是，如果你在 Airbnb 上经营一家酒店或汽车旅馆，主人将不需要注册短期租赁许可证，但需要申请正式的豁免。

## **1)**

正如上面提到的西雅图定律，我们可以忽略整个 home/apt 值，直接进入私人房间，查看仅两个住宅就有太多列表的极端情况。请记住，Airbnb 没有给出房源的地址，尽管数据库中实际上有“街道”字段。这些当然不是完整的真实地址。Airbnb 会主动隐藏房源的地址，只有在你确认预订后才会透露。因此，人们不能说这些列表实际上是否在同一个房子里。

![](img/aef1780bb47ee245a607f7e78397f1c7.png)

**(图片作者)**

通过运行 53 个值中的前 20 个值，可以根据他的列表名称将达里奥的财产分为 4 个不同的组

*   10 分钟车程到市中心
*   距离市中心 5 分钟车程
*   距离西雅图中心 3 个街区
*   私人房间

![](img/1489d1006bfe5ce09543d22418bed438.png)

**(图片作者)**

此外，当您检查实际的经度和纬度本身时，它们彼此高度相似，只是略有不同。Airbnb 房源上的房间和设施图片无法区分开来:

*   [快乐佛房步行 10 分钟到市中心](https://www.airbnb.com/rooms/43434896?source_impression_id=p3_1591925255_WCNBoABCysSUpwiS&guests=1&adults=1)
*   [波普艺术室，距离西雅图中心 3 个街区](https://www.airbnb.com/rooms/43434358?source_impression_id=p3_1591925546_k3B0Utbbpxlwc1cF&guests=1&adults=1)

从各自的角度来看，他似乎在经营一家精品酒店，但归类为短期租赁的许可证，这是专门为 Airbnb 设计的，位于市中心。如果所有的房源都是合法的，达里奥可能会经营一家受到上述不同监管的酒店，或者属于 2017 年 9 月 30 日之前签署的“豁免”团体。如果没有，Airbnb 或市议会应该调查一下情况，并调查达里奥是否违反了规定。不仅是达里奥，还有其他主持人，像维拉，赛义德，香农，李等。应该接受检查。

## **2)** **职业主持人的不良影响**

目前，西雅图没有阻止专业托管活动的规定。这种缺点为 Airbnb 将其平台外包给专业主机(第三方房地产公司)的可能性打开了大门。现在，80%的主机只有少于 5 个列表。我们假设拥有比 1 多几个列表的主机也可能是几个朋友的主机。但也有极端的案例(312)，这让我们怀疑他们是在专业地做这件事。

![](img/0f8dbca2f4fb98ff254b4a69d128b763.png)

**(图片作者)**

下面，我们显示了包含 20 个以上列表的主机。如果你看一下他们在 Airbnb 上的房源，你会被前三名的每一个房源的标准化和专业性所震撼。因此，我们可以有把握地说，这些是专业的主持人。

![](img/715da10e34e630483e6c507d480acccf.png)

**(图片作者)**

深入了解前三名，我们可以了解更多关于 Airbnb 的运营方式。看起来，除了希望获得一些额外收入的传统主持人的非专业房源之外，Airbnb 还经常与中小型房地产公司建立合作关系。Airbnb 允许这些当地公司将其租赁的房产注册为平台上的正常房源，以产生更多的网络流量来换取佣金。如下表所示，公司参与的条款和程度因安排而异:

[***Corp Condos&Apts/Balsa***](https://barsala.com/)

> “我们是一个充满激情的团队，经营着一家现代化的技术支持的公司住房公司，该公司认为装修精美的高端住宅应该是一致的，负担得起的，易于预订的。”

= >尽管在系统上被注册为“Corp Condos & Apts ”,但所有房源都归 Barsala Barsala 所有，这是一家中型房地产公司，专注于在西海岸提供物有所值的租赁合同。关于 Airbnb 和 Barsala 之间的关系没有太多信息

[***宙斯***](https://zeusliving.com/)

> “宙斯正在改造企业住房。我们通过在遍布旧金山湾区、洛杉矶、华盛顿的 1400 多所房屋中的每一所提供独一无二、无忧无虑、高质量的住房体验来实现这一目标。“宙斯已经成为宙斯的永久合作伙伴”

= >随着 Airbnb 吸收越来越多的住房需求，它正在探索如何将度假租赁以外的机会货币化。长期企业住房市场可能是一个巨大的业务，但 Airbnb 没有自己建设，而是战略性地投资与房地产长期租赁市场的领导者之一 Zeus Living 合作。这是一个巧妙的组合:宙斯的可用属性和 Airbnb 的全球推广平台 [(Constine，2019)](https://techcrunch.com/2019/12/09/airbnb-zeus/)

[](https://loftium.com/)

> *“待在有价值的地方。当你预订了阁楼，你就是在为当地社区做贡献。每个阁楼都是当地居民的家，他们就住在这里，确保您的体验是愉快的。所有空间的设计都考虑到了您的舒适度！我们使入住和沟通变得轻而易举，每个家庭都为您的旅行提供了一个美丽舒适的休息场所。每一个 Loftium 家和主人都是独一无二的，在您入住期间，您将获得真正的邻里体验。参观一个新的社区，并在我们的任何一个城市预订 Loftium:西雅图、波特兰、丹佛、圣地亚哥、凤凰城、芝加哥、亚特兰大、达拉斯、夏洛特或奥兰多。我们等不及你来参观了！”*

*= >从只与 Airbnb 合作租房，创始人决定开发自己的房产租赁应用，同时与 Airbnb 合作。他们的商业策略是，如果潜在租户/买家同意成为 Airbnb 的托管人，就在价格昂贵的地区给予他们荒谬的折扣。Hannah Exner 和 Sam Joselyn 在西湖附近以 1000 美元/月的价格获得了一套豪华公寓，价格超过 1500 美元/月 [(Levy，2019)](https://www.geekwire.com/2019/loftium-pivots-real-estate-biz-now-offers-discounts-apartment-tenants-rent-rooms-airbnb/)*

*除了考虑西雅图政府将采取哪些有效措施来确保所有这些商业伙伴关系不会加剧危机之外，这是一个现实和产品差异化的问题。由于一家公司以提供真实体验和当地隐藏的宝石而自豪，这使其在客户眼中的形象高于其他酒店竞争对手，从房地产中介引入这种千篇一律、精心制作的房源可能会削弱该公司独特的价值比例。[(拉利奇&维斯迈尔，2017)](https://doi.org/10.1007/978-3-319-51168-9_56) 。随着时间的推移，即使是大多数死硬的 Airbnb 爱好者也可能会在其他地方寻找“真实性”*

# ***三/给游客的建议***

## ***1)** **每个小区的日均价、点评分数和安全指数***

*在这一部分中，我们比较了两人的平均每日比率(ADR ),并根据社区进行了评估。我们预计到市中心的距离是最重要的因素，因为所有西雅图的地标都位于市中心。距离和评论分数之间可能有很强的相关性。可能影响审查分数和 ADR 的其他因素包括:*

*   *位置的安全指数*
*   *噪音。如果一个房源位于市中心，但在嘈杂的酒吧中，这应该会在位置评论上扣分。*
*   *如果房源位于市中心以外，但公共交通四通八达，那么它们会得到一些加分(西雅图已经发展了火车和公共汽车系统)*
*   *附近的必需品和娱乐设施(超市、酒吧、餐馆等)。)*
*   *包括免费停车。因为在西雅图市中心停车平均要花 20/ 2 小时*

*有趣的是，与其他酒店相比，安女王酒店的价格要高得多(约 285 美元/天)。然后是市中心(约 165 美元/天)，然后是其他街区。令人惊讶的是，不管房源在哪里，平均评论分数都在 9/10 以上，所以不管你选择哪个社区，最大的满意度总是有保证的。我们认为这是因为西雅图总的来说面积小，人口少(总共 100 万)。这座城市的交通也很便利，所以如果他们碰巧住在郊区，往返市中心大约需要 30 分钟*

*![](img/a083d1de916455c4c1adf81392832840.png)*

***(图片作者)***

*尽管没有旧金山那么严重，西雅图仍然深受大量无家可归者和乞丐的困扰。大部分是无害的，不会惹你。尽管如此，它仍然对公众形象产生负面影响，并挫伤了游客参观城市的积极性。此外，游客可能经历的财产犯罪比暴力犯罪多 7 倍。如果你开车去西雅图，即使在停车场，你也可能会遭遇入室盗窃。像大多数城市一样，西雅图最安全的地区在市中心以外，往往是住宅区或商业不发达的住宅区。最安全的社区有日落山、巴拉德、木兰、阿尔基、木兰、下皇后安和沃灵福德。西雅图警察局有一张西雅图地区的地图，用犯罪数量进行颜色编码。深蓝色区域意味着病例较多，而浅色区域病例较少*

*![](img/4b64c8cfc4caa8157be90e70ba8c2509.png)*

***西雅图的犯罪率统计(来源:** [**西雅图警察局**](https://www.seattle.gov/police/information-and-data/crime-dashboard) **)***

*考虑到 ADR、评论评分和犯罪统计数据，建议客户在西西雅图、Magnolia、Ballard、Rainer Valley、Central Area、Seaward Park、Beacon Hill、University District、Interbay 和 Northgate 预订 Airbnb，以获得低廉的租赁价格、最高的安全性和最终的高满意度。我目前住在 Rainer Valley/ Beacon Hill，离市中心开车 20 分钟或坐火车 30 分钟，一切都很近。该地区经历了适度的中产阶级化，因此人们预订 Airbnb 体验既安全又方便。在 Beacon Hill 的一个美丽的星期天烧烤一些令人垂涎的烤肉是生活中最奢侈的事情。*

*![](img/79339a283d3157f11a759576a676f5ec.png)*

***莱纳山谷/比肯山壁画(作者提供图片)***

## *2)如何使用复习分数*

*与书面评论同样重要的是，客人可以提交总体星级和类别星级。评级分为:*

*   *总体体验*
*   *清洁(任何酒店最重要的因素)*
*   *准确性(广告与产品匹配吗？)*
*   *价值(有没有被敲竹杠的感觉？)*
*   *沟通(在你入住之前、期间和之后，主人对你的关注和问题的回应如何？*
*   *抵达(入住过程顺利吗？)*
*   *位置*

*读者可以在下面找到所有这些类别的分数分布。人们不禁对各科的高分感到惊讶。这在 Airbnb 中很常见，因为该公司以向客户提供卓越服务而闻名 [(Plautz，2015)](https://mashable.com/2015/02/25/airbnb-reviews-above-average/?europe=true) 。因为标准如此之高，客人应该只选择在五个因素中至少有四个因素得分为 10 的房源。值是最棘手的一个，因为与其他指标相比，它们的分数明显更高，这使得该因素比其他指标更容易区分。呆在一个在价值上得到 10 分的主机上，即使他们在其他方面可能得分较低，这意味着你可能会中头彩。*

*![](img/db05482fef72fe307cd26e93e3372a03.png)*

***所有类别的分数分布(按作者分类的图片)***

## *3)找到一个好的主人*

*为了对主人的努力表示感谢，Airbnb 授予那些最受尊重的人“超级主人”的地位。成为一个超级主播意味着你可以从你的列表的可见性增加中受益，获得潜在的收入，甚至可以获得独家奖励[(陈，2017)](https://www.nytimes.com/2017/01/11/technology/personaltech/the-guide-to-being-an-airbnb-superhost.html#:%7E:text=In%20the%20process%2C%20I%20have,percent%20of%20hosts%20are%20Superhosts.&text=The%20designation%20as%20a%20Superhost,away%20from%20netting%20a%20profit.) 。Airbnb 在其广告活动中展示了一些超级主机的列表，超级主机甚至被邀请发表演讲或分享如何获得这一酷头衔的技巧。为了成为超级主持人，主持人必须拥有 4.7 或更高的平均综合评分，该评分基于其 Aibnb 客人在过去一年中的评论。他们还需要在前一年组织至少 10 次住宿，或者如果这些预订的期限更长，则需要在至少 3 次住宿中组织 100 次住宿。Superhosts 不得有任何取消，除非有情有可原的情况，并需要在 24 小时内回复他们的客户。尽管要克服很多限制，但西雅图的 Airbnb 房源让他们脱颖而出，目前拥有近 3 万名超级房东(约 45%)。对于 Airbnb 的国际超高住宿率(20.2%)来说，这是一个令人震惊的数字*

*![](img/819762ab2602cca46a56979ef60a8477.png)*

***(图片作者)***

*既然超级旅馆在西雅图如此受欢迎，这就引出了一个问题:超级旅馆是否是选择房间的必要标准之一。一方面，用超高的价格预订可能意味着在住宿上花更多的钱。另一方面，作为一个顾客，我不希望遇到不好的主人，他们经常取消订单，而且总是迟迟不回复。幸运的是，在 Airbnb 上很少会遇到没有回应的主机，大多数主机不到一个小时就能回复，最晚一天之内。如此快速的数字部分解释了为什么西雅图的 Airbnb 充斥着优秀的超级房东。因此，是否是超级主持人是潜在客人不应该大力强调的事情。*

*![](img/b1b4dbab52658835999c60a1335ca5c6.png)*

***(图片作者)***

## *4)可用性和超时平均价格*

*“日历”文件包含 365 条记录，记录了一年中每一天每个列表的价格和可用性。为了得到正确的结果，我们将共享列 listings_id 上的‘calendar’与‘listings’[‘accommodes’]合并，listings _ id 函数作为左边的索引。合并后的表格示例如下所示，需要注意的是,“f”表示业主不想在特定日期出租其房产，或者房源已经被其他人/第三方预订。*

*![](img/e47b80b85c08d30ad94d39899a97e9b3.png)*

***(图片作者)***

*在未来的 6 个月里，在达到最低点之前，可用的住宿数量会更高。记住，数据是在 2020 年 4 月 23 日收集的。这意味着当时正值美国冠状病毒爆发的高峰期。六个月的正数意味着很多客人在意识到疫情的严重性之前就已经确定了未来的发展方向。因此，10 月 16 日的预订量不到 1100 份，到 2021 年 1 月中旬几乎没有预订量。可供住宿的数量发生如此巨大变化的另一个原因是，房东们正在积极寻找这些租赁房产的其他用途，以在面临危机时保持稳定的收入来源。Airbnb 的预订在人们的心目中是次于最后的。对于交互式地图，您可以放大集群，最终找到列表的各个位置(下面是 Github 代码)*

*![](img/ec2a589411021fa40a8943e4d2db00da.png)*

***(图片作者)***

*由于 2 人住宿很受欢迎，我们只选择 2 人的可用房源，并使用 mean()函数计算平均值。7 月 27 日星期六，ADR 达到 127 美元的峰值，这种愤世嫉俗的模式是由于周末的价格更高。随着时间的流逝，价格急剧下降。我怀疑这是 COVID 和 host 最后一刻降价努力的影响，这证明 Airbnb 需要一些时间才能再次盈利。*

*![](img/ed1b8bb3c3a58b9b8985042a27cfe4c9.png)*

***(图片作者)***

*然而，这并不是世界末日。据报道，西雅图的阳性病例和死亡人数已经从曾经的全国冠状病毒中心大幅下降。这都归功于华盛顿人的努力，特别是西雅图人，他们一直遵守州政府的“呆在家里”的命令。幸运的是，覆盖西雅图大部分地区并受到严重影响的金县有足够的信心申请第二阶段的重新开放计划。因此，我们乐观地认为，到 9 月/10 月，一切都会恢复正常*

*令人兴奋的是，这也是游览这座城市的最佳时间。夏季标志着这座城市的旺季，这意味着房价飙升，而冬季则笼罩在无尽的寒冷雨天中，即使是最热情的游客也会望而却步。西雅图的花朵在秋天绽放得最灿烂，夏天的天气随着人群的散去而挥之不去，留下了足够的 Airbnb 空间来抢占 [(USnews，2019)](https://travel.usnews.com/Seattle_WA/When_To_Visit/) 。9 月和 10 月也充满了庆祝活动，如 bumber shoot(9 月)、Earshot 爵士音乐节(10 月-11 月)、西雅图餐厅周(10 月-11 月)。我们建议潜在客户在 10 月 15 日之前预订，因为房价较低，并且仍有许多可用房源。没有什么比走上街头庆祝疫情的结束更好的了，在千变万化的习俗中，享受美味的饼干和温暖人心的杂烩，作为真正的糖果*

*![](img/a6462c953b24a95604a4343753aab9a6.png)*

*著名的派克市场的新鲜农产品(图片由作者提供)*

# ***IV/文字挖掘与评论***

*自然语言处理(NLP)是人工智能的一个分支，它使用自然语言分析计算机和人类之间的关系。NLP 在实现 Deep Leering 的神经神经元网络等应用时非常有用，因为它有助于以有价值的方式阅读、破译、理解和理解人类语言。 [(Yse，2019)](/your-guide-to-natural-language-processing-nlp-48ea2511f6e1) NLP 帮助我根据客人对酒店的评论预测反馈分数。但是在这个练习中，我们只是想看看评论需要什么，并演示 NLP 要经历的步骤，以便为未来的研究建立一个具体的基础。*

*“reviews”文件并不有趣，因为它只包含每个列表的审查日期。“review_details”包括类似的信息，只是多了 4 列，因此，我们将“host_id”、“host_name”与 review_details 文件左合并在一起:*

*![](img/a5ccfafaba542b4fa0e80c343dd91450.png)*

***(图片作者)***

*以下是评论数量最多的 5 位主持人。有趣的是，Loftium 以 4181 条评论再次出现在顶部。我们认为，这是由于该公司独特的商业模式，他们能够产生如此多的建设性评论，以改善他们的产品。*

*![](img/9fa3ca26af9ba2751163c3d424416457.png)*

***(图片作者)***

*为了清理任何自然语言处理数据集，我们需要遵循 5 个步骤:*

*   *取出空注释:with notnull()*
*   *删除数字:用 str.replace('\d+'，'')*
*   *小写:with str.lower()*
*   *移除 windows 新行:with str.replace('\r\n '，"")*
*   *用 nltk 库去掉所有停用词:我们需要用英文指定中的 stop.word()赋值一个变量“stop_english”。然后，我们使用 lambda 函数将整个句子用“”分开，然后在没有停用词的情况下再次连接在一起*
*   *去掉所有标点:用 str.replace('[^\w\s]'，" ")*
*   *将 x 个空格替换为一个空格:with .str.replace('\s+'，' ')*

*最后，我们可以看到索引 1 处的原始审查和清理后的版本之间的巨大差异*

*![](img/249b986003132a60cb3d2678f23f543f.png)*

***(图片作者)***

*请记住，如果我们想要构建一个世界云，实际的过程实际上并没有停止，因为这些评论充满了与我们的分析无关的主机名称。不幸的是，有 1949 个名字可用，在“review_details”数据集中搜索每一个名字将花费很长时间，而且这些名字并不真正影响最终的单词云。因此，我们将从这一点继续前进，未来的研究人员可以试图找出如何处理这个特定的任务。在使用 sklearn 和 WordCloud()的 CountVectorizer()函数后，我们可以看到最常用单词的排名以及单词云本身*

*![](img/facae192646defa7e38c2bc3e5126c66.png)**![](img/271974c250a718a38fab3645c12b319a.png)*

***(图片作者)***

# ***V/结论***

*简而言之，从比较研究的角度和提出解决方案的角度探索西雅图的 Airbnb 情况，让我们对公司如何运作、制定战略和创新性地转变为酒店业不可忽视的力量有了宝贵的见解。我们相信，Airbnb 在今年年底经受住当前的风暴后，将夺回其应有的宝座。*

***Github:**https://Github . com/lukastuong 123/Python-Projects/tree/master/Project-% 20 Airbnb % 20(Python-% 20 interactive % 20 map % 2C % 20 natural % 20 language % 20 processing % 2C % 20 comparative % 20 study % 2C % 20 regression)*

***参考&来源:***

***Airbnb** 。(2020 年 6 月 16 日)。华盛顿州西雅图| Airbnb 帮助中心。从 https://www.airbnb.com/help/article/869/seattle-wa[取回](https://www.airbnb.com/help/article/869/seattle-wa)*

***卡维尔，O.** (2020 年 6 月 8 日)。Airbnb 见证了度假租赁需求的激增。洛杉矶时报。[https://www . latimes . com/business/story/2020-06-07/Airbnb-冠状病毒-需求](https://www.latimes.com/business/story/2020-06-07/airbnb-coronavirus-demand)*

***陈，b . x .**(2017 . 1 . 11)。成为 Airbnb 超级房东指南。检索自[https://www . nytimes . com/2017/01/11/technology/personal tech/the-guide-to-be-an-Airbnb-super host . html #:% 7E:text = In % 20 process % 2C % 20I % 20 have，percent % 20 of % 20 hosts % 20 are % 20 super hosts。&text = The % 20 design % 20 as % 20a % 20 super host，away % 20 from % 20 netting % 20a % 20 profit](https://www.nytimes.com/2017/01/11/technology/personaltech/the-guide-to-being-an-airbnb-superhost.html#:%7E:text=In%20the%20process%2C%20I%20have,percent%20of%20hosts%20are%20Superhosts.&text=The%20designation%20as%20a%20Superhost,away%20from%20netting%20a%20profit)。*

***孔斯蒂内，J.** (2019 年 12 月 9 日)。TechCrunch 现在是威瑞森媒体的一部分。从 https://techcrunch.com/2019/12/09/airbnb-zeus/[取回](https://techcrunch.com/2019/12/09/airbnb-zeus/)*

***道尔顿，A.** (2017 年 2 月 7 日)。纽约市开始打击非法 Airbnb 房源。检索自[https://www . engadget . com/2017-02-07-new-York-city-launch-Airbnb-listings-activation . html](https://www.engadget.com/2017-02-07-new-york-city-illegal-airbnb-listings-crackdown.html)*

***研，K.** (2020 年 4 月 8 日)。 *Airbnb 的冠状病毒危机:烧钱、愤怒的主机和不确定的未来*。华尔街日报。[https://www . wsj . com/articles/airbnbs-coronavirus-crisis-burning-cash-angry-hosts-and-an-uncertainty-future-11586365860](https://www.wsj.com/articles/airbnbs-coronavirus-crisis-burning-cash-angry-hosts-and-an-uncertain-future-11586365860)*

***拉利奇，l .&魏斯迈尔，C.** (2017)。真实在 Airbnb 体验中的作用。旅游业中的信息和通信技术 2017，781–794。[https://doi.org/10.1007/978-3-319-51168-9_56](https://doi.org/10.1007/978-3-319-51168-9_56)*

***利维，N.** (2019 年 5 月 6 日)。房地产初创公司 Loftium 转向租赁，停止为 Airbnb 利润份额提供首付。检索自[https://www . geek wire . com/2019/loft ium-pivots-real-estate-biz-now-offers-discounts-apartment-tenders-rent-rooms-Airbnb/](https://www.geekwire.com/2019/loftium-pivots-real-estate-biz-now-offers-discounts-apartment-tenants-rent-rooms-airbnb/)*

***普劳茨，J.** (2015 年 2 月 25 日)。高于平均评分？95%的 Airbnb 房源评分为 4.5 到 5 星。检索自[https://Mashable . com/2015/02/25/Airbnb-reviews-above-average/？欧洲=真](https://mashable.com/2015/02/25/airbnb-reviews-above-average/?europe=true)*

*西雅图市议会。 (2017 年 4 月)。规管短期租金政策简介。检索自[https://www . Seattle . gov/Documents/Departments/Council/Issues/Regulating shorterm Rentals/Regulating-Short-Term-Rentals _ Policy-Brief _ 2017-04 . pdf](https://www.seattle.gov/Documents/Departments/Council/Issues/RegulatingShortTermRentals/Regulating-Short-Term-Rentals_Policy-Brief_2017-04.pdf)*

***沙夫罗斯，F.** (2016 年 9 月 17 日)。Airbnb 给城市制造了一个经济适用房的困境。检索自[https://www . governing . com/columns/public-money/gov-Airbnb-affordable-housing . html](https://www.governing.com/columns/public-money/gov-airbnb-affordable-housing.html)*

***美国新闻。** (2019 年 11 月 4 日)。游览西雅图的最佳时间。从 https://travel.usnews.com/Seattle_WA/When_To_Visit/[取回](https://travel.usnews.com/Seattle_WA/When_To_Visit/)*

*是的，迭戈·洛佩兹。 (2019 年 1 月 15 日)。自然语言处理(NLP)指南。检索自[https://towards data science . com/your-guide-to-natural language-processing-NLP-48ea 2511 f6e 1](/your-guide-to-natural-language-processing-nlp-48ea2511f6e1)*

*— — —*

***数据集:**http://insideairbnb.com/get-the-data.html*

***灵感来源:**[https://www . ka ggle . com/erikbruin/Airbnb-the-Amsterdam-story-with-interactive-maps](https://www.kaggle.com/erikbruin/airbnb-the-amsterdam-story-with-interactive-maps)*