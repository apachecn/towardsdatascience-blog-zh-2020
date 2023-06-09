# 为 CIFAR-10 数据集实现深度神经网络

> 原文：<https://towardsdatascience.com/implementing-a-deep-neural-network-for-the-cifar-10-dataset-c6eb493008a5?source=collection_archive---------22----------------------->

## 使用 PyTorch 和 CIFAR-10 数据集对初学者友好的图像分类

![](img/a10fd6f5c4399a5650ff3472f3244075.png)

约书亚·索蒂诺在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

# **神经网络:它们是如何工作的？**

神经网络是多功能模型，可以学习任何复杂的模式。这些强大的模型是由多层感知器、卷积网络、序列模型等组成的深度学习的核心。在这个简短的项目中，我将探索 [CIFAR-10 数据集](https://www.cs.toronto.edu/~kriz/cifar.html)并实现一个简单的神经网络(多层感知器)。

神经网络的概念其实很简单。类似于神经元在人脑中如何激发或激活，神经网络中一层内的神经元通过激活函数被激活。这个过程返回输出，该输出将被传递到神经网络的下一层，并且循环重复，直到神经网络结束。这一过程被称为前向传递，即在应用权重和激活函数后，您的数据通过网络向前传递。根据您要解决的是回归问题还是分类问题，神经网络的最终输出层将为回归问题输出一个节点，为分类问题输出多个节点。在这个项目中，我们将对图像进行分类，因此神经网络的输出将在每个类中有一个节点，该节点将通过 softmax 函数获得最终预测。

神经网络的本质不是向前传递期间发生的事情，而是向前传递之后发生的事情。前向传递的最终输出值用于通过在网络中反向传递来更新神经网络的权重。这被称为反向传播，这是一种非常强大的算法，它从最后一层到第一层迭代地更新权重。当使用随机梯度下降优化器时，这是训练神经网络的极其有效的方式。

# 准备模型训练

如 CIFAR-10 信息页面所述，该数据集由 10 类 60，000 幅 32x32 彩色图像组成，每类 6，000 幅图像。有 50，000 个训练图像和 10，000 个测试图像。由于我们正在处理彩色图像，我们的数据将由基于 RGB 比例分割的数值组成。

来自 CIFAR-10 数据集的样本图像

对于这个项目，我们将使用数据集的 10%作为验证集，90%作为训练集。损失函数将是交叉熵损失，因为这是一个分类问题。优化器将是随机梯度下降，梯度下降的批量将是 128。随机梯度下降是梯度下降的近似。损失函数的梯度被应用于一批所有的训练点，而不是整个集合，这样计算起来快得多。这种对训练样本的随机批量采样引入了大量噪声，实际上有助于防止算法陷入狭窄的局部极小值。

# 基于 GPU 的基本模型和训练

首先，我们为我们的神经网络创建基础模型，其中我们将为训练过程和验证过程定义函数。

图像分类基础模型

然后，我们将定义 evaluate 函数，以在每个时期后返回我们的模型的进度，并定义 fit 函数，用于更新每个时期的权重。

模型评估函数和拟合函数

由于我们使用 PyTorch，我们可以选择使用 GPU 来训练和评估我们的模型。GPU 在更新和计算权重方面效率更高，因为它们针对矩阵计算进行了优化，而不是 CPU。因此，如果数据可用，我们将把数据转移到 GPU。

将数据移动到 GPU

现在我们准备定义我们的神经网络。对于这个例子，我将为我的神经网络使用 4 个隐藏层，每个层的输入节点分别为 1536、768、384 和 128。正向传递函数将使用整流线性单元激活函数(ReLu ),这是一个将 max(x，0)应用于输入 x 的转换函数。该转换函数对于神经网络很流行，因为它不会激活层内的所有节点，从而使模型成为非线性的。

创建隐藏层和正向传递函数

最后，我们准备对模型进行训练和评估。初始化随机权重后，我们将迭代通过神经网络，并根据我们的学习速率(步长)和时期进行反向传播。这里的目标是获得最终使损失最小化的重量。我们将通过梯度下降来大步前进，直到我们收敛到更接近最小值。一旦我们收敛到更接近最小值，我们将采取更小的步长，直到我们达到尽可能低的最小值。

学习率为 0.1 时的 15 个时期

学习率为 0.01 时的 5 个时期

学习率为 0.001 时的 5 个时期

学习率为 0.0001 时的 5 个时期(损失似乎在这一点上收敛)

我们知道我们已经收敛到最小值，因为我们的精度没有进一步提高，我们的损失没有进一步减少。这是我们的神经网络能想到的最好的模型。这意味着我们的模型有一半以上的时间是正确的。这可能是因为我们的模型着眼于每个像素，而不是整个画面。当我们看图像时，如果我们只看一个像素，相对来说很难概括图像是什么。

损失与时代

准确度与纪元

现在我们知道我们已经得到了可能的最佳模型，让我们用测试集来测试它。

使用测试集进行评估

55%的准确率！这表明，为了找到数据集的最佳模型，选择正确的历元数和学习率是至关重要的，但在这种情况下，使用该模型对任何事物进行分类都是不实际的，因为精度非常低。如前所述，这很可能是因为模型正在逐个查看每个像素。这就是卷积网络的闪光点。这些网络是利用卷积层的深度神经网络，卷积层使用卷积滤波器来处理和产生图像。当我们查看完整的图片或图片的一部分时，人类可以更好地了解图像是什么，卷积网络能够查看图片的一部分，使其保留更多关于图像的信息，而不是查看像素。

# 参考

*   [CIFAR-10 数据集](https://www.cs.toronto.edu/~kriz/cifar.html)
*   [我的 Jovian notebook](https://jovian.ml/allenkong221/03-cifar10-feedforward)