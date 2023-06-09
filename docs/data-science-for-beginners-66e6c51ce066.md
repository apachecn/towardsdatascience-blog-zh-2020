# 初学者的数据科学

> 原文：<https://towardsdatascience.com/data-science-for-beginners-66e6c51ce066?source=collection_archive---------29----------------------->

![](img/d35a8f08fefbac87964d0fc71cd0fd64.png)

来源: [Pixabay](https://pixabay.com/photos/web-network-technology-developer-3963945/)

**进入数据科学，我们需要什么？**

*   像 SQL 这样的查询语言
*   像 R/Python 这样的编程语言
*   可视化工具，如 power bi/Qliksense/Qlikview/Tableau 等。
*   机器学习的基本统计学
*   机器学习算法(确保你在你希望成为专家的领域，如销售、金融、人力资源、运营等领域尝试用例。所有人的用例都不同)
*   实践和实施

**a)查询语言**

**你可以学习的查询语言类型:** SQL 无疑是市场上最好的语言，它不会消失。

您可以学习的另一种查询语言是 elasticsearch。如今它被广泛使用。我通过一门业余课程学会了它。SQL 和 elasticsearch 的区别在于，在 elasticsearch 中，您有一个数据框架，其中不是每一行都有相同的列值。例如数据库车。比方说，对于一些汽车，我们只有型号名称、价格和颜色信息。对于一些，我们可能有颜色，型号，价格，型号数量，母公司等。对于另一种类型的汽车，我们可能只有型号和名称等信息。在 SQL 中，这是通过在缺少字段的地方放置 NAN 值来捕获的。在 elasticsearch 中，没有 NAN 这个概念。

学习来源:你可以从 W3Schools/Tutorialspoint 或任何地方学习，因为学习 SQL 几乎不需要一周时间。如果您无法访问数据库进行练习，您可以加载任何 csv 文件作为数据库进行练习。

可以通过相同的网站学习 Elasticsearch /Kibana。同样，你可以参加 Udemy 的课程，因为这比 SQL 更难学。

**环境:**如果你正在学习 SQL，可以安装 MySQL/PostGRESQL，开始练习。对于 elasticsearch，您可以安装 Kibana 并进行练习。

**为什么查询语言对数据科学很重要？**

在数据科学中，我们有庞大的数据集，有数百万行和数百万列。对于分析，你不需要所有的数据。我们需要使用查询语言提取相关数据，然后进行分析。

**大数据:**还可以学习 Scala、Hadoop/MapReduce 等大数据语言或技术。然而，这对于大多数 D.S .工作来说是好的，而不是必须的。这更像是锦上添花。大数据是数据工程的一部分，通常涉及编码，这与融合了统计学、数学、编码和领域知识的数据科学不同。大数据应该在你彻底掌握数据科学之后学习。

**b)编程语言**

流行的语言:有两种主要的语言:R 和 python。r 是由统计学家和数学家设计的语言。Python 是一种编码语言。两个都好。然而，现在 Python 更受欢迎，因为它有来自编程世界的强大支持生态系统，更好的可扩展性，以及与 API 和其他完整产品代码的更好集成。

**学习来源:**通过 Coursera 学习 Python。课程名称是“数据科学的 Python”也可以通过 tutorialspoint 和 W3schools 学习。不仅仅是课程，我还通过主要和次要的项目了解到我们应该做的，作为我们证书的一部分。

我通过 Udemy 学会了 R。数据科学研究高级课程。深入学习一种语言并对另一种语言有一个大致的了解是有好处的。这是因为在一个团队中，你将与许多数据科学家一起工作。有些人会习惯使用 R，有些人会习惯使用 python。

**环境** : Anaconda Navigator，Pycharm，Spyder 或者 Jupyter 笔记本。

环境是一个你基本上编码和实现你的代码的地方。

我个人最喜欢的环境是 Jupyter 笔记本。Jupyter 笔记本可以让你输入 R/Python/HTML 等等。，因此您可以使用特定语言的最佳库或技术，并在 Jupyter 中使用它。此外，如果两个人使用不同的语言，那么您可以使用 Jupyter 笔记本轻松地进行协作。

查询解析: Stackoverflow 和 Stackexchange 是询问语言问题的好地方。人们通常在 5 分钟到 24 小时内回复。

**c)可视化工具**

**可以学习的工具:**Tableau/PowerBI/Qliksense/Qlikview 是最常见的工具。PowerBI 和 Tableau 应用最为广泛。

PowerBI 几乎就像 excel 的高级版本，非常容易学习。excel 的唯一问题是它会崩溃，并且在处理大量数据时会变得很慢。也没有太多的选项可用于惊人的观想。这一切在 PowerBI 中都是可能的。另一个好处是 PowerBI 是免费的。对于 Tableau，您可以下载 30 天的试用版，但对于 PowerBI，您可以想用多久就用多久(PowerBI 的免费版本中提供了大多数功能)。Apple 不支持 PowerBI/Qliksense/Qlikview，因为它们是基于 windows 的产品。

**学习来源:**通过 Udemy 学习了 PowerBI。我根据评分来选择课程。任何评分在 4.3 以上的课程都很酷。我通过 Tableau 网站学习 Tableau。

**d)数据科学统计学:**

**你应该知道的基本术语:**标准差、均值、中位数、众数、偏度、假设检验、中心极限定理、总体对样本、z 得分、置信区间、p 值、统计显著性、临界值、比例检验、双尾、单尾、帕累托原理、卡方检验、z 检验、t 检验、正态分布、高斯分布等。

**学习来源:**Kirill Eremko 的 Udemy 数据科学统计课程，R 中的统计学习介绍或任何统计基础书籍。

**e)机器学习算法:**

**最常用的算法类型:** XGBoost、RandomForest、深度学习、神经网络、时间序列、决策树、聚类和分类算法。

**学习来源:**机器学习 Udemy 上的 Kirill Eremko 课程很惊艳。Otxts 书是 ML 可视化算法的好书。这是一个免费的资源，也是网上最好的资源之一。[https://otexts.com/fpp2/graphics-exercises.html](https://l.facebook.com/l.php?u=https%3A%2F%2Fotexts.com%2Ffpp2%2Fgraphics-exercises.html%3Ffbclid%3DIwAR1iFo9tBeCa40HVy1kgplzZIITQZVmB46hEUcPrtfz4stXUYGLAA-fpmeA&h=AT0293daVzIlZpMdgoec5WlQyxl5eP3cDKq3iQOLyJxcrR06-2SAG9wBjvF9lPKMYSpjN21uEsY0VyfshjuSGOHXsQH1MmiYJ__JmIZkOsfrX8dWMWKEZSOLp5YA460ZC2kMr69vixBrFlE_jr_M_A)

R 中的统计学习介绍对 ML 中的统计和应用的基础很有帮助

**如何决定实施哪些算法:**

首先，了解您的问题的用例。你想干嘛?你的产出是连续变量吗？(取值 1、3、10 等。基本上任何值)或者它是二元决策还是你想把人们聚集在一起，为一群人做一些决定？

在一个项目中，我不得不从事金融领域的信用风险分析。你必须决定一个人是否有能力偿还贷款。所以这是一个二元决策。在这种情况下，您需要一个分类算法，因为您希望将一个人分类为违约者或非违约者。所以我使用逻辑回归(当输出为二进制是/否等时使用)、XGBoost 或决策树。你基本上可以使用任何分类算法。这里可以使用的其他分类算法有 SVN、朴素贝叶斯等。(你可以谷歌分类算法获得完整列表)。

如果在一个项目中，我需要预测股票或房子的价值，那么它可以取从 10 卢比到 1，000，000 卢比或更多的任何值，等等。(连续变量)。这里我将使用回归。回归可以是多种类型，简单线性、多元线性、多项式、SVR 等。通过检查 r 平方误差(预测值与实际值相差多远)，可以找到正确的回归技术。

同样，如果我需要找出目标细分市场，我将需要使用聚类算法。k 均值和层次聚类都是聚类算法的例子。

所以首先要学习算法(至少一个分类算法，一个聚类算法，一个回归算法)，然后看看你需要什么算法来解决手头的问题，然后开始分析。

**我应该学习什么类型的项目和算法:**

首先，选择你的域名。例如，我的领域是金融和营销。所以我可以在这里谈论这些。虽然清单是无穷无尽的，我将只写下我学到的最重要的算法

**营销**:时间序列建模(主要是 ARIMA 建模)，预测未来的销量、数量和价值。时间序列建模意味着你有一件事的数据，比如说一家公司一段时间(可能是几个月、几年、几天等)的销售数据，你可以预测该公司未来几年/几个月/几天的销售情况。

聚类算法对目标群体进行聚类，并为每个群体设计单独的类别。

流失建模，以决定有多少现场工作人员将留下，有多少将离开管理工作流程。

**金融:**分类算法像逻辑回归(逻辑回归和线性或多元回归完全不同，只是名字相似)，SVN，朴素贝叶斯，XGBoost 等。进行信用风险分析，找出谁会违约。

资产评估回归(股票价值、抵押资产等。)

**f)实施**

如何运用你的知识:

*   Coursera、Udemy 等课程中的项目
*   Vidhya，Kaggle 等分析的黑客马拉松，看看你在人群中的位置。
*   实时项目
*   在公司和工作中

希望这有所帮助！

![](img/67b92fd9b97baacbc236a50560a0e03b.png)