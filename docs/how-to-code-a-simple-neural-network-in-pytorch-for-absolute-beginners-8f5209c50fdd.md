# 如何用 PyTorch 编写一个简单的神经网络？—适合绝对的初学者

> 原文：<https://towardsdatascience.com/how-to-code-a-simple-neural-network-in-pytorch-for-absolute-beginners-8f5209c50fdd?source=collection_archive---------11----------------------->

## 这是一个简单易懂的教程，使用 PyTorch 和 Kaggle 上流行的 Titanic 数据集来构建神经网络

![](img/917e9a2c5696d5ab7a2c78626255d91c.png)

图片来自 [Unsplash](https://unsplash.com/photos/m_HRfLhgABo)

在本教程中，我们将看到如何使用 PyTorch 框架为分类问题构建一个简单的神经网络。这将帮助我们掌握基础知识和框架的基本语法。同样，我们将使用 Kaggle 的泰坦尼克号数据集。

## 安装 PyTorch

```
## For Windows
pip install torch===1.5.0 torchvision===0.6.0 -f [https://download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)## For Linux
pip install torch torchvision
```

如果您的计算机配置不同(基于 Conda 的库或 Mac 系统)，您可以从这个[链接](https://pytorch.org/get-started/locally/)中检查合适的命令。

## 数据集准备

首先，通过参加比赛从 [Kaggle](https://www.kaggle.com/c/titanic/data) 下载数据集，或者你也可以从其他来源获得(简单的谷歌搜索会有帮助)。一旦你设置好数据集和 PyTorch 包，我们就可以开始深入研究了。在设计架构之前，首先要做的是根据 PyTorch 的要求准备数据，这可以使用 PyTorch 本身提供的数据集模块来完成。如果你觉得很难理解，让我给你解释一下。您将处理的大多数数据都是 Numpy 结构。现在，这不能直接输入网络，因为它们不是张量。Pytorch 要求您以这些张量的形式输入数据，这类似于任何 Numpy 数组，只是它也可以在训练时移动到 GPU。你所有的梯度，你的网络处理的权重，都是相同的张量数据结构。随着你进一步阅读博客，你将能够得到更好的理解。现在，让我们加载数据。

现在我们导入***Dataset****模块来继承***_ _ getitem _ _()***、 ***__len__()*** 等库中预定义的各种函数。这些函数将帮助我们创建自定义类来初始化数据集。下面的代码显示了如何创建数据集类。*

***注意:**在上面的代码中，我们的数据帧的最后一列包含目标类，而其余的是输入特征，因此我们将其拆分为到 ***self.inp*** 和 ***self.oup*** 变量，如果我们要训练，我们需要输入和输出，否则只需要输入数据。*

****__init__()*** 函数读取*。csv* 文件，我们稍后会对其进行一些预处理(这与本教程无关)。***_ _ len _ _******()***函数返回示例的数量，而 _ _***getitem _ _()***用于通过使用其索引来获取数据。从上面这段代码中需要注意的重要一点是，我们已经使用 ***torch.tensor*** 函数将我们的训练示例转换为张量，同时使用它的索引调用它。所以在整个教程中，无论我们在哪里取例子，都是以张量的形式。*

*现在，既然数据已经准备好了，让我们将它分批加载。这可以使用如下的 ***数据加载器*** 功能轻松完成。*

*您必须将前一个函数产生的数据集对象作为参数传递。根据批次的数量，结果将是一个形状为 ***(no_of_batches，batch_size，size_of_the_vector)的多维张量。*** 现在，对于其他类型的数据，如图像或序列数据，其维数会根据其性质而相应变化。但是现在，只要理解有多个批次，并且每个批次包含一些等于批次大小的示例(不管使用什么数据)。*

*现在深呼吸…你已经完成一半了。:)*

## *神经网络体系结构*

*现在，既然我们已经为训练准备好了数据，我们必须在开始训练之前设计神经网络。任何具有常规使用的超参数的模型都可以(Adam 优化器、MSE 损失)。为了给我们的神经网络编码，我们可以使用 ***nn。模块*与**创建相同。*

****nn。线性()，nn。继承 ***nn 后，BatchNorm1d()*** 全部变为可用。模块类()。然后你可以简单地通过调用它来使用它们。由于我们使用简单的表格数据，我们可以使用简单的密集层(或全连接层)来创建模型。对于激活，我使用了自定义定义的***【swish()***。你也可以选择雷鲁。ReLu 在***nn . functional()***模块中可用。你可以简单地用 ***F.relu()* 替换 ***swish()*** 。**由于这是一个二进制分类，所以没有必要在最后一层使用 softmax。我已经使用 sigmoid 函数对我的例子进行了分类。在上面的代码中， ***__init__()*** 帮助您在调用构造函数时立即初始化您的神经网络模型，并且 ***forward()*** 函数控制通过网络的数据流，使其负责前馈。当我们进入训练循环时，你将看到我们如何调用 forward 函数。****

## *训练模型*

*您的培训过程可以安排如下:*

*   *你可以定义你的训练参数，比如次数，损失函数，优化器。所有的优化器在***torch . optim()****中都有。*您的优化函数将网络的权重作为其参数。在下面的代码中，net 变量包含我们在上面的小节中创建的神经网络模型，***net . parameters()***引用网络的权重。*

*   *每一批数据都被输入网络。基于损失函数，我们计算该特定批次的损失。一旦计算出损失，我们通过调用*函数来计算梯度。一旦你计算出梯度，我们就更新现有的权重。每个时期的每个批次都会发生相同的过程。正如我前面提到的，我们可以简单地绕过神经网络的输入作为参数来进行前馈。(就像下面代码中的 ***型号(x)*** )。**

*****optimizer . step()***用于使用计算出的梯度更新权重。**

*   **在纪元结束时，我们对验证数据进行预测。最后，我们根据训练预测和验证数据计算准确度。**

*   **为了得到一个整体的想法，我把我的整个训练循环贴在了下面。**

*   **基于可用的计算资源，您可以使用下面的代码将您的数据和网络移动到 GPU。记住，无论你使用哪个设备，所有的输入、输出数据以及网络都应该在同一个设备上(否则，它会抛出一些愚蠢的错误:p)。**

**你完成了教程…:)为自己感到骄傲。**

**参考**

**[1][https://py torch . org/tutorials/beginner/deep _ learning _ 60min _ blitz . html](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html)**