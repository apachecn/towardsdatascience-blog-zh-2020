# 如何在 Julia 中从零开始构建人工神经网络

> 原文：<https://towardsdatascience.com/how-to-build-an-artificial-neural-network-from-scratch-in-julia-c839219b3ef8?source=collection_archive---------8----------------------->

## 如何在没有机器学习库的情况下建立神经网络模型

我经常从喜欢“*从零开始构建算法*”系列的读者那里收到的一个流行的请求是关于深度学习或神经网络的报道。神经网络模型可能非常复杂，但在其核心，大多数架构都有一个共同的基础，从这个基础上出现了新的逻辑。这个核心架构(我称之为*香草神经网络*)将是这篇文章的主要焦点。因此，这篇文章旨在构建一个香草神经网络 ***，而不是*** 任何 ML 包，而是用 Julia(一种我觉得是数值计算的完美伴侣的语言)实现这些数学概念。目标是从头实现一个神经网络模型来解决二分类问题。

![](img/96ddc8d8544452376e5ab29bdf25247c.png)

作者拥有的版权

## 神经网络的简要背景

那么什么是神经网络呢？神经网络的起源被广泛归因于沃伦麦卡洛克(神经病学家)和沃尔特皮茨(数学家)在 1934 年的论文。在这篇论文中，他们利用电路模拟了一个简单的神经网络，灵感来自人类大脑的工作方式。

## 什么是神经网络？

在某种基础水平上，神经网络可以被视为一个系统，它试图从生物神经元如何相互共享信息中获得灵感，以试图在一些提供的数据中发现模式。神经网络通常由互连的层组成。香草神经网络的层是:

*   输入层
*   隐藏层
*   输出层

输入层接受传递到隐藏层的原始数据，隐藏层的工作是试图在原始数据中找到一些潜在的模式。最后，输出层将这些学习到的模式结合起来，得出一个预测值。

![](img/83ef4d054657987f6cd83c1f64c8f915.png)

从 [NN-SVG 生成的图像](http://alexlenail.me/NN-SVG/LeNet.html)

这些互连的层如何共享信息？神经网络的核心是神经元的概念。所有这些层都有一个共同点，它们都由神经元组成。这些神经元负责信息在网络上的传输，但是这种数据传输使用的是什么样的机制呢？

## 神经元——神经网络的构建模块

与其絮絮叨叨地用一些机器学习理论来解释这种机制，不如让我们简单地用一个涉及单个神经元的非常简单而实用的例子来解释它。假设我们有一个简单的例子，我们想训练一个神经网络来区分海豚和鲨鱼。幸运的是，我们从世界各地的海豚和鲨鱼那里收集了成千上万的信息。为简单起见，我们假设为每个被观察对象记录的唯一变量是'***【X1】***'和' ***【重量】【X2】***'。每个神经元都有自己的参数——‘*权值(W1)*‘和’***偏差(B1)***’——这些参数用于用这些参数处理传入的数据( **X1** & **X2** )，然后与下一个神经元共享这个过程的输出。这一过程直观地表示如下:

![](img/e06a922e139c0dc78e93edd691febf91.png)

作者拥有的图像版权

一个典型的网络由许多层神经元组成(数十亿，在 GPT-3 的例子中)。这些神经元的集合构成了普通神经网络的主要参数。好吧，我们知道神经元是如何工作的，但是一大群神经元是如何学习如何根据一些提供的数据做出好的预测的呢？

## 标准神经网络的主要组件

为了理解这个学习过程，我们将构建自己的神经网络架构来解决手头的任务。为此，我们需要在一个典型的普通网络中通过 5 个组件分解操作序列；

![](img/20a368edd5d7c43a43a38bf00c6398cf.png)

作者拥有的图像版权

网络设计要解决的问题的性质通常决定了这 5 个组件的可用选择范围。在某种程度上，这些网络就像乐高系统，用户插入不同的激活函数、损失/成本函数、优化技术。毫不奇怪，这种深度学习是科学计算中最具实验性的领域之一。记住所有这些，现在让我们跳过有趣的部分，实现我们的网络来解决二进制分类任务。

> **NB** :该实现将用维度为 **(n，m)** 的输入数据进行矢量化，映射维度为 **(m，1)** 的一些输出目标，其中 **n** 是数量，是特征的数量， **m** 是训练样本的数量。

![](img/cdc85ee97b3f6001c0b1812a30156226.png)

从 [NN-SVG 生成的图像](http://alexlenail.me/NN-SVG/LeNet.html)

*   **模型参数的初始化**

这些网络通常由许多层神经元堆叠而成。层和神经元的数量是固定的，并且这些神经元的元素(权重和偏差)最初通常填充一些随机值(用于对称破坏，因为我们有一个优化问题)。这个片段随机初始化给定网络维度的参数:

*   **正向传播算法**

初始化模型/网络的参数后，让我们构建通过网络运行输入数据以生成预测值的函数。如前所述，激活功能在这种信息流中起着至关重要的作用。我们的网络将使用 ReLU activator 来激活输出层和 sigmoid activator。这些激活剂如下所示:

![](img/65852631869783fecd6dacac4f5f0508.png)

作者拥有的图像版权

这两个函数实现了这些激活器；

随着我们的激活器的实现，我们的注意力现在转移到通过正向传递或传播序列将数据从输入层移动到输出层。首先，计算线性输出，然后使用一个激活函数将线性输出转换为非线性输出。

![](img/cd26a6f3b38271b820bb985604eca4df.png)

作者拥有的图像版权

> **注意**:激活的输入和输出被“缓存”或保存，以备以后检索和使用。

下面这两个函数提供了通过网络移动数据的实用程序:

整个前向传播算法的顺序非常简单。我们简单地在网络维度上循环，使得一层的输出成为下一层的输入，直到最后一层给出预测值或分数(使用 sigmoid 激活时的概率分数)。下面的代码片段实现了这个序列；

*   **成本/损失函数**

我们现在有了一个网络，它能够根据随机初始化的参数对我们的训练样本进行一些预测。下一步是看看这些预测有多准确。为此目的，网络需要一个*成本* *或损失函数*。此成本/损失函数有一个简单(关键)的任务，即总结所有训练示例的预测值与实际输出值的接近程度。*对数损失(二元交叉熵)*函数适用于二元分类问题，因此下一个函数实现了成本函数；

![](img/3dd5068b8a542e22772bc9a71c85357d.png)

作者拥有的图像版权

*   **反向传播算法**

我们的网络可以生成一些随机值作为预测，它也可以知道这些预测与实际输出有多远，所以下一个合乎逻辑的步骤将是找出如何提高其决策能力，而不仅仅是进行随机预测，对吗？

使用神经网络的' ***'学习*** '过程的核心是反向传播算法。不出所料，这是新手最难理解的部分。在我们的网络中实现这一步骤之前，让我们尝试用一些高层次的直觉来解释这一步骤。

反向传播序列的目标是理解网络的每个参数( ***所有层*** 的所有权重&偏差)如何相对于成本/损失函数变化。但是我们为什么要这么做呢？这个过程允许我们将学习策略转化为最小化目标，我们希望成本/损失输出尽可能低。此外，我们还知道并能够测量网络中螺栓和旋钮(**权重和偏差**)的变化如何影响损失函数。思考一下这个简化的类比，并意识到这个概念是多么强大！最终，我们所要做的就是调整网络的**参数** — *权重和偏差*，使其在损失/成本函数方面提供最低值，瞧，我们就像在科幻电影中一样做出预测了！

反向传播实现方面的核心是从多元微积分学借用的链规则的概念。事实上，反向传播的整个序列可以被视为每一层的偏导数(以及它们的权重' **W** '和偏差' **b** '以及线性输出， **Z** )相对于成本/损失函数的长链。顾名思义，这个序列链通过从输出层到输入层的反向*T21，使用正向传播序列期间存储的缓存来计算偏导数。为了简洁起见，这里是在我们的网络中实现反向传播所需的矢量化公式。*

![](img/be37e2185c606971a0f3a26d06274fda.png)

作者拥有的图像版权

这两个效用函数实现了我们的 sigmoid 和 ReLu 激活的导数:

利用激活函数的导数，让我们集中于对线性激活输出的存储分量(权重、偏差和前一层的激活输出)进行解包，并利用这两个函数计算它们中的每一个相对于损失函数的偏导数。

结合激活函数的导数和各层激活输出的存储分量，构成具有该函数的网络的反向传播算法。

*   **优化技术**

我们快到了！我们的网络正在形成。当给定一些层作为体系结构时，它可以随机地初始化这些层的参数/权重，生成它们的一些随机预测，并使用该函数量化它与地面事实的总体正确或错误程度；

此外，反向传播步骤现在允许网络测量这些权重中的每一个如何相对于损失函数变化。因此，所有网络需要做的就是调整这些不同的权重，使其预测尽可能与提供给该网络的数据的实际输出相匹配。

理论上，可以尝试网络中所有参数的所有可能范围，并选择给出最佳可能损耗的网络(由损耗函数的输出值确定)。实际上，这种低效的方法是不切实际的，原因很简单:对于寻找具有如此多参数的网络的最佳参数来说，计算成本太高。由于这个和其他原因，使用优化技术来寻找最佳参数。梯度下降是寻找这种网络的最佳参数的最流行的优化技术之一。现在让我们用一个简单的实际类比来解释这种优化技术。

假设你被放在珠穆朗玛峰的顶端，给你一个戴着眼罩寻找山的最低部分的挑战(在那里放了一个装满黄金的袋子作为价格)。一个人能得到的唯一帮助是，在这个旅程的每一个点，他/她都可以通过对讲机与向导交谈，只需要询问在那个点相对于山的最高点(*坡度*)的当前方向。梯度下降作为一种优化技术，提出了一种简单而有效的方法来帮助人们应对这一挑战(给定约束)。这项技术提供的一个潜在的解决方案是，一个人从某个点开始，在不同的步骤使用步话机获得到珠穆朗玛峰最高点的相对方向，然后在给定的相反方向上移动一些步骤(*学习速率*)。重复这些技巧，直到到达珠穆朗玛峰最低处的那袋金子。

![](img/038132da601d38d107f49f926ee1c50c.png)

作者拥有的图像版权

这个代码片段在我们的网络中应用梯度下降来更新网络的参数。

## 培训我们的网络

神经神经的训练基本上是一系列的序列，其中输入数据通过使用该网络的可用参数、与实际训练数据预测相比较的预测，以及最后作为改进预测的方法的参数调整，通过网络被转发。在机器学习行话中，这个序列的每次运行都被称为一个“*时期*”。这个训练阶段的核心思想是试图在各种尝试或迭代(*时期*)中改进网络生成的预测。这个代码片段结合了我们到目前为止已经生成的所有不同的组件:

所有组件就绪后，是时候测试实现是否工作了。为了简洁起见，让我们为这个演示生成一些简单的合成二进制分类数据。这很容易做到，因为:

![](img/90e41b3f8f795bb234fcd6b5413788e5.png)

训练模型的输出。作者拥有的图像版权

## 结论

如曲线图所示，网络以低精度和高成本值开始，但是随着它不断学习和更新网络的参数，精度上升(而成本稳定),直到它在这个超级简单和完美的虚拟数据集上获得完美的分数。可悲的是，数据集在现实生活中很少如此完美！

一如既往，期待反馈！直到下一篇文章，继续玩这个实现，也许实现其他损失函数和优化算法。在下一篇文章中，我们将以这个实现为例，介绍制作和注册一个 Julia 包的过程。