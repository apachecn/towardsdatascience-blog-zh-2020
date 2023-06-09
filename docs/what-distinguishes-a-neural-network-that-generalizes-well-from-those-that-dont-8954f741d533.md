# 是什么将泛化能力强的神经网络与泛化能力差的神经网络区分开来？

> 原文：<https://towardsdatascience.com/what-distinguishes-a-neural-network-that-generalizes-well-from-those-that-dont-8954f741d533?source=collection_archive---------56----------------------->

## 理解深度学习需要重新思考泛化

![](img/860675afd4a116e508c4fd2693407826.png)

蒂娜·西尼亚在 [Unsplash](https://medium.com/s/photos/cat-in-a-bowl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

最近偶然看到这篇被广泛谈论的论文，“[理解深度学习需要重新思考泛化(张等 2016)](https://bengio.abracadoudou.com/cv/publications/pdf/zhang_2017_iclr.pdf) ”。这篇论文已经获得了 2017 年 ICLR 最佳论文奖。这提出了一个非常重要的问题“尽管有足够的能力来记忆输入，为什么深度神经网络会泛化？”

在这篇文章中，我将分享我的理解，并讨论不同的实验执行和结果以及影响。

在直接进入本文之前，我将解释几个有用的概念。

*   泛化误差
*   模型容量
*   显式和隐式正则化

## 泛化误差

![](img/aa300c568feea2b888c059dd774bade9.png)

泛化误差被定义为训练误差和测试误差之差。

绿色曲线表示训练误差，红色曲线表示测试误差。这里我们可以看到模型过拟合，泛化误差逐渐增加。

## 模型容量

模型容量定义为模型适应不同类型输入的灵活程度。

[通用逼近定理](https://en.wikipedia.org/wiki/Universal_approximation_theorem)

*具有单层的前馈网络足以表示任何函数，但是该层可能大得不可行，并且可能无法正确学习和概括。*

*—伊恩·古德菲勒，* [*DLB*](http://www.deeplearningbook.org/contents/mlp.html)

[VAP Nik–Chervonenkis VC 尺寸](https://en.wikipedia.org/wiki/Vapnik%E2%80%93Chervonenkis_dimension)

*一个分类模型* ***f*** *带有一些参数向量* ***θ*** *被说成*[](https://en.wikipedia.org/wiki/Shattered_set)*****(x1，x2，…。，xn)*** *如果对于这些点的所有标签赋值，存在一个* ***θ*** *使得模型* ***f*** *在评估该组数据点时不会出错。***

***模型* ***f*** *的 VC 尺寸是可以排列的最大点数，以便* ***f*** *粉碎它们。再正式一点，就是最大基数***这样一些数据点集合的基数*****D****可以被* ***f*** *粉碎。*****

**我们可以完美标记的数据点的最大数量称为模型的 VC 维。**

**![](img/01abc59ea21fb4b5efc8a2e625b226fb.png)**

**[https://en . Wikipedia . org/wiki/VAP Nik % E2 % 80% 93 chervonenkis _ dimension](https://en.wikipedia.org/wiki/Vapnik%E2%80%93Chervonenkis_dimension)**

**在上面的例子中，我们有一个简单的线性分类器，我们希望将两个组(蓝色加号和红色减号)分开。对于四个输入数据点，存在一些可能的数据点组合，这些数据点不可能使用线性分类器分成两组。因此，线性分类器的 VC 维将是 3。**

**VC 维预测分类模型的测试误差的概率上界。**

**![](img/034accbb68e0bb52994f7945a8749ba0.png)**

**这里， ***D*** 是模型中的参数个数， ***N*** 是训练集的大小。**

**以上条件仅在 ***D < < N*** 时有效。这个概率上界对于深度神经网络是没有用的，在深度神经网络中，参数的数量通常多于数据点的数量***(N<<D)***。**

## **显式和隐式正则化**

**本文引入了两个新的定义，显式正则化和隐式正则化。辍学，数据增加，重量共享，常规正则化(L1 和 L2)都是显式正则化。隐式正则化是早期停止、批量正则化和 SGD。虽然论文中没有定义这种区别，但我觉得隐式正则化是指那些我们作为其他过程的副作用而实现正则化的过程。例如，我们使用 L1 专门用于正则化，因此显式。然而，我们使用批量规范化来规范化不同输入的激活，并且作为副作用，它也碰巧执行某种正则化，所以它是隐式正则化。**

***注:以上部分是我的理解，如有错请指正。***

## **不同的随机化测试**

**在论文中，作者进行了以下随机测试:**

*   **真实标签:未经修改的原始数据集。**
*   **部分损坏的标签:独立于概率 ***p*** ，每个图像的标签被损坏为均匀随机类。**
*   **随机标签:所有的标签都被替换成随机标签。**
*   **混洗像素:选择像素的随机排列，然后将相同的排列应用于训练集和测试集中的所有图像。**
*   **随机像素:不同的随机排列独立应用于每个图像。**
*   **高斯:高斯分布(具有与原始图像数据集匹配的均值和方差)用于为每个图像生成随机像素。**

## **随机测试的结果**

**![](img/8aba9f7009db97af096b21262b8a9140.png)**

**[https://bengio . abracadoudou . com/cv/publications/pdf/Zhang _ 2017 _ iclr . pdf](https://bengio.abracadoudou.com/cv/publications/pdf/zhang_2017_iclr.pdf)**

**结果看起来非常有趣，因为该模型可以完美地拟合噪声高斯样本。它还可以完美地拟合带有完全随机标签的训练数据，尽管这需要更多的时间。这表明具有足够参数的深度神经网络能够完全记忆一些随机输入。这个结果非常反直觉，因为这是一个被广泛接受的理论，即深度学习通常会发现较低级别的特征、中级别的特征和较高级别的特征，如果模型可以记住任何随机输入，那么如何保证模型会尝试学习一些建设性的特征，而不是简单地记住输入数据。**

## **正则化测试的结果**

**![](img/1ddd2a3aa2b6e71feb65776a2dbd13f4.png)**

**[https://beng io . abracadoudou . com/cv/publications/pdf/Zhang _ 2017 _ iclr . pdf](https://bengio.abracadoudou.com/cv/publications/pdf/zhang_2017_iclr.pdf)**

**第一张图显示了不同的显式正则化对训练和测试精度的影响。这里，关键的要点是使用正则化和不使用正则化在泛化性能上没有非常显著的差异。**

**第二张图显示了批处理规范化(隐式正则化)对训练和测试准确性的影响。我们可以看到，使用批量标准化的训练非常顺利，但并没有提高测试精度。**

**通过实验，作者得出结论，显式和隐式正则化都有助于提高泛化性能。然而，**正则化不太可能是泛化的根本原因**。**

## **有限样本表达能力**

**作者还证明了以下定理:**

***存在一个具有 ReLU 个激活值和* ***2n+d*** *个权值的两层神经网络，它可以在一个大小为* ***n*** *的* ***d*** *维样本上表示任何函数。***

**这基本上是[通用逼近定理](https://en.wikipedia.org/wiki/Universal_approximation_theorem)的扩展。这个证明相当沉重，如果有兴趣可以参考[论文](https://bengio.abracadoudou.com/cv/publications/pdf/zhang_2017_iclr.pdf)附录中的 C 部分。**

## **隐式正则化:线性模型的吸引力**

**在最后一节中，作者表明，基于 SGD 的学习赋予了正则化效果，因为 SGD 收敛于具有最小 L2 范数的解。他们的实验还表明，最小范数并不能确保更好的泛化性能。**

## **定论**

*   **几个成功的神经网络架构的有效容量足以[粉碎](https://en.wikipedia.org/wiki/Shattered_set)训练数据。**
*   **模型复杂性的传统度量对于深度神经网络是不够的。**
*   **即使泛化能力很差，优化仍然很容易。**
*   **SGD 可以通过收敛到具有最小*-范数的解来执行隐式正则化。***

***随后的一篇论文“[深入研究深层网络中的记忆](https://dl.acm.org/doi/pdf/10.5555/3305381.3305406?download=true)”对这篇论文中指出的一些观点提出了挑战。他们令人信服地证明了学习随机噪声与学习实际数据之间的定性差异。***

***![](img/f8a0a221d15690d835abb867bf5cd88e.png)***

***[https://dl.acm.org/doi/pdf/10.5555/3305381.3305406?下载=真](https://dl.acm.org/doi/pdf/10.5555/3305381.3305406?download=true)***

***上面的实验显示，尝试记忆随机噪声的深度神经网络相对于实际数据集需要明显更长的学习时间。它还显示了拟合一些随机噪声会导致更复杂的函数(每层有更多的隐藏单元)。***

***![](img/760f00fde183742605c4a737ff266801.png)***

***【https://dl.acm.org/doi/pdf/10.5555/3305381.3305406? 下载=真***

***这个实验表明正则化子确实控制了 DNNs 记忆的速度。***

***因此，总结来说，深度神经网络首先试图发现模式，而不是蛮力记忆，以适应真实数据。然而，如果它没有发现任何模式(如在随机噪声的情况下)，网络能够以仅记忆训练数据的方式简单地优化。鉴于这两种情况，该论文建议我们需要找到一些更好的工具来控制概括和记忆的程度，像正则化、批量归一化和辍学这样的工具并不完美。***

***如果你有任何想法、评论或问题，请在下面留下评论或在 [LinkedIn](https://www.linkedin.com/in/ratulghosh1/) 上联系我。快乐阅读🙂***