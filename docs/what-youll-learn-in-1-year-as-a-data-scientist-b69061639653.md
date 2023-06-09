# 作为一名数据科学家，一年后你会学到什么

> 原文：<https://towardsdatascience.com/what-youll-learn-in-1-year-as-a-data-scientist-b69061639653?source=collection_archive---------17----------------------->

![](img/57759a2f4db1fefa0516e79c0b215ed8.png)

蒂姆·范德奎普在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## 区分经验丰富的数据科学家和数据科学爱好者的因素

大约一年前，经过几个学术研究项目和许多数据科学课程的工作，我终于在一家快速发展的电子商务公司获得了一个应用数据科学的职位。我将尝试分享我在工作中学到的、在家的数据科学爱好者事先不太了解的东西。

# 1.在远程服务器上工作

大多数人在他们的计算机上开始他们的数据科学之旅。然而，在实际的数据科学项目中，所需的计算能力和内存远远超过笔记本电脑所能提供的。因此，数据科学家使用他们的计算机访问远程服务器，通常使用 SSH(安全外壳)连接。ssh 允许用户使用私钥(SSH 密钥)安全地访问另一台计算机。一旦建立了连接，就可以像使用计算机外壳一样使用远程服务器。说到 shell，[知道](http://linuxcommand.org/)基本的 shell 命令有助于过渡到在远程服务器上工作。

![](img/ab00119094c8c07ff6146b7697723aa8.png)

照片由[克里斯蒂娜@ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 2.SQL 是王道

数据科学和机器学习是在 Python，Julia 和 R 上完成的吧？错了，是在 SQL 上做的！每个数据科学项目都是从数据开始的，大多数情况下，用于解决问题的数据并不容易获得，应该使用数据库的几个表中的部分数据来创建数据。

SQL 是事实上的标准数据库语言，用于快速连接、聚集和选择所需数据的部分。每个与数据相关的职位都需要熟练使用 SQL，因为它每天都被大量使用。大多数人忽视提高他们的 SQL 知识，如果不是完全忽视学习它的话。很自然，大多数爱好者没有数据库服务器，他们的数据集已经被别人建立了。实际上，数据科学家 90%的时间都花在准备和清理训练数据上。我知道这有点令人失望，但是如果没有数据，就没有数据科学。

应该注意的是，SQL 有许多方言，但是它们彼此相似，不同之处可以很容易地适应。只需选择一种方言并开始学习它！

# 3.功能比模型更重要

线性模型通常被视为简单，不适用于机器学习问题。我的意思是，你能在多大程度上线性增加你的功能并得到正确的结果？其实可以大有作为。

更复杂的模型，如随机森林、xgboost、SVM、DNNs 等。在特征空间(解释变量所在的空间)中寻找非线性边界。他们通过将特征空间划分为更小的部分或将特征映射到更高维的特征空间，然后在这个新空间中绘制线性线来实现这一点。最后(经过极大的简化)，它们都可以被认为是通过新生成的数据点拟合一条直线。由于模型不知道特征的内在含义，它们试图基于某种核或通过优化伪似然函数来创建这种新特征。

![](img/869becfd7ff79675899cf03b15540821.png)

http://songcy.net/posts/story-of-basis-and-kernel-part-2 使用核技巧进行高维映射，来源:

这看起来很复杂，对吗？这就是为什么它们被称为灰/黑盒模型。另一方面，知道特征真正含义的人可以从数据中生成新的有意义的特征。这个特征生成、转换、预处理和选择步骤被称为**特征工程**。基本的特征工程方法包括采用特征的均值-标准差、将连续变量离散化到箱中、添加滞后/差异特征等。

经过适当的特征工程，任何模型都可以获得很好的结果。线性模型因其可解释性而更受青睐。您可以查看所生成要素的显著性和系数，并对模型的有效性做出评论。如果一个系数在逻辑上应该是正的，结果却是负的，那么模型、数据或假设可能有问题。为什么这么重要？因为有一个基本规则，垃圾进垃圾出。

# 4.实验和生产的区别

大部分数据科学都是在 Jupyter 笔记本上完成的，因为它易于实验和可视化。很容易快速尝试新的东西，训练新的模型或在笔记本上看到一些表达的结果，只需打开一个新的单元格，就可以随心所欲了。

然而，当模型准备好投入**生产**时，jupyter 笔记本时代结束，python 文件时代开始。生产(简称 prod)是你的算法在现实生活中运行的地方。最终用户(内部或外部)受生产代码的影响，因此生产级代码应该快速、干净、详细、容错且易于调试。我说的这些是什么意思？

如果您只是在尝试，并且将运行代码一次或两次，那么代码的速度就不那么重要了。然而，在生产中，您的代码可能每天运行多次，其结果将影响生产生态系统的其他移动部分。因此，执行的持续时间变得很重要。

让我们面对现实吧，你的一些(如果不是全部的话)笔记本是无序的，混乱的，有未使用的导入，有实际上不再需要的电池，对吗？没关系，你只是在试验你的想法。现在是时候清理你的代码了，这样除了你自己之外的其他人就可以真正地遵循你的代码的步骤了。如果团队中的任何人都能轻松地查看您的代码并理解每一行的目的，那么您的代码就会变得足够干净。这就是为什么你应该给你的变量和函数起一个有意义的名字，不要用忍者编码。

您应该将代码执行的重要步骤记录到 shell 屏幕以及一个**日志文件**中。控制台日志记录有助于直观地看到在 shell 上运行代码时所采取的步骤，让您随时了解执行情况。另一方面，日志文件有助于识别运行代码时可能遇到的问题。一个好的日志文件应该包括开始和结束时间、结果摘要、遇到的异常和每次执行的问题。

当产品代码由于任何原因开始失败，用户开始看到奇怪的结果时，这是一个令人紧张的事件。好的产品代码应该能够处理可能的异常，并事先做好必要的断言，如果出现意外/无法解决的问题，应该提醒团队。根据具体情况，失败的代码可以被编程为给出前一次运行的结果，不给出任何输出或提供预定义的结果。在出现问题时，花时间舒适地编写容错代码通常比压力编码要好。

即使代码是容错的，代码内部也可能存在一个 bug，从而产生意想不到的结果。在这种情况下，应该调试代码，通常使用调试工具，找到原因。干净的编码使调试更容易，但是这还不够。程序员应该使用函数而不是重复代码，给每个函数一个单一的目的，避免使用[不纯的函数](https://en.wikipedia.org/wiki/Pure_function)。这种做法使得在代码中定位 bug 的来源变得容易。

对于编写产品级代码，我建议使用文本编辑器，如 [VS Code](https://code.visualstudio.com/) ，而不是使用 jupyter notebook。软件开发工具使开发更加容易和快速。如果你仍然想使用 jupyter notebook，有一个名为 [nbconvert](https://nbconvert.readthedocs.io/en/latest/) 的工具可以从 jupyter notebook 创建 python 文件。

# 5.最有价值球员

技术世界竞争激烈，瞬息万变。很多时候，没有时间去等待一个达到最先进性能的完美产品。科技公司不是以完美的产品为目标，而是从一个项目开始，快速构建一个 [MVP](https://en.wikipedia.org/wiki/Minimum_viable_product) (最小可行产品)并迭代。MVP 需要满足项目最基本的需求，不需要任何花哨的东西，仅此而已。

对于完美主义者或注重细节的人(即大多数数据科学爱好者)来说，通常很难进行 MVP。大多数数据科学家努力仔细分析数据，尝试许多不同的功能和模型，并提出最佳模型。数据科学，作为一个领域，本质上是面向研究的，然而，我没有指定**应用**数据科学。

当我第一次开始的时候，这种哲学困扰着我，但是不要担心，这样实际上更好。最重要的资产是时间。一个项目将走的道路无法预先知道，因此投资在项目上的时间不能保证是有价值的。根据用户反馈和 A/B 测试，您正在进行的项目可以暂停或完全取消。通过构建一个 MVP 而不是一个成熟的项目，风险被最小化。即使项目被保证留下，大多数时候足够的数据是不可用的，或者未来可能的复杂情况是未知的。构建一个简单的模型，并用新生成的数据和获得的专业知识对其进行迭代，可以得到更快、更可靠的结果。

# 6.敏捷开发

在团队工作中，科技界的另一个概念是[敏捷开发](https://agilemanifesto.org/principles.html)。敏捷是一种开发哲学，在这种哲学中，项目被划分为小任务，团队成员从积压的任务中获取新任务。在 sprint 规划期间，团队会给每项任务一个估计分数，然后团队会计算 sprint 任务的总分数。其实说起来容易做起来难。敏捷是为软件工程开发的，在软件工程中，任务持续时间更容易估计，路径和实践定义得更好。另一方面，数据科学任务需要反复试验，并且由于高方差，任务持续时间更难估计。具有讽刺意味的是，数据科学家对其他业务问题做出了准确的预测，却不能对他们的任务做出同样的预测。

# 7.A/B 测试

你已经训练和调整了一个新模型，调整了它的超参数，它在每个测试指标上都给出了非常好的结果，远远超过了之前的模型。您需要立即将其部署到生产环境中，对吗？可惜没有。

敏捷和数据科学的核心是 A/B 测试。你的模型可能会在测试和模拟中击败之前的模型，但在现实生活中可能会失败。这就是为什么它被称为模拟，而不是真实的现实。训练数据只是在模型制作中高度处理的过去现实的子集。时代会变，错误会犯，模型无法解释所有的数据变化。只有在 A/B 测试期间，一个模型可以产生显著的提升时，该模型才会被以前的模型所取代。

# 8.与不同学科的人交流

成为一名数据科学家实际上与成为一名软件开发人员或科学家有很大的不同。通常，数据科学家与业务和技术人员密切合作，因此他们需要了解业务和技术两方面。

业务人员通常是数据科学家的内部客户，业务人员不关心模型的复杂程度或代码的优美程度，他们关心的是因果关系。这就是线性和基于树的模型发挥巨大作用的地方。白盒模型易于解释、直观且易于理解。商业人士，尤其是在开始的时候，会想知道为什么 ML 模型会做出一个决定，直到他们相信它是可行的。因为模型是为业务需求而构建的，所以它们应该为业务人员的需求而定制。

在模型的开发和生产过程中，数据科学家与开发人员密切合作。开发人员通常会收集和提供数据管道，并在生产中使用您的算法结果。技术—数据科学集成有多种方式。开发人员可能会将数据科学家的代码转化为生产级代码(使第 4 点变得过时)，为数据科学家提供一个 API 来提供他们的结果，或者调用数据科学家创建的模型的 API。每种方式都有其优点和缺点，并且可能会在生命周期中反复出现。

数据科学家需要能够理解业务需求和开发人员的局限性。他们应该向开发人员传达与业务和数据科学相关的需求，并向业务人员传达技术方面的能力和限制。

# 结论

TLDR:在数据科学部门工作与在《孤独》中为 Kaggle 项目建立机器学习模型截然不同。我已经试图列出那些事先不太为人所知的关键区别。我希望读者会发现它很有用，因为我知道我喜欢写它。