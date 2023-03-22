# 在 VGG16 和 VGG19 CNN 模型中提取特征、可视化过滤器和特征地图

> 原文：<https://towardsdatascience.com/extract-features-visualize-filters-and-feature-maps-in-vgg16-and-vgg19-cnn-models-d2da6333edd0?source=collection_archive---------2----------------------->

## 了解如何在 VGG16 和 VGG19 CNN 模型中提取特征、可视化过滤器和特征地图

![](img/fd55c092127512a0a3f83064c658e747.png)

[VGG16 架构](http://www.cs.toronto.edu/~frossard/post/vgg16/)

![](img/aec54a77a380c9117a22ef011eeb24e2.png)

[VGG19 架构](https://miro.medium.com/max/2408/1*6U9FJ_se7SIuFKJRyPMHuA.png)

[**Keras**](https://keras.io/applications/) 提供了一组深度学习模型，这些模型与[**ImageNet**](http://www.image-net.org/)**数据集上预训练的权重一起可用。这些模型可用于预测、特征提取和微调。在这里，我将讨论如何为给定图像的预训练模型 VGG16 和 VGG19 提取特征、可视化过滤器和特征图。**

# **用 VGG16 提取特征**

**![](img/b0185b3c022aa2ab8b36b49683cae10a.png)**

**用 VGG16 提取特征**

**这里我们先从 tensorflow keras 导入 VGG16 模型。导入 image 模块来预处理图像对象，导入 preprocess_input 模块来为 VGG16 模型适当地缩放像素值。numpy 模块是为数组处理而导入的。然后，使用 imagenet 数据集的预训练权重加载 VGG16 模型。VGG16 模型是一系列卷积层，后跟一个或几个密集(或全连接)层。Include_top 允许您选择是否需要最终的密集层。False 表示加载模型时不包括最终的密集图层。从输入层到最后一个 max pooling 层(标注为 7×7×512)作为模型的**特征提取部分**，其余网络作为模型的**分类部分**。在定义了模型之后，我们需要加载模型期望大小的输入图像，在本例中是 224×224。接下来，图像 PIL 对象需要被转换为像素数据的 NumPy 数组，并从 3D 数组扩展为具有[ *样本、行、列、通道* ]维度的 4D 数组，这里我们只有一个样本。然后，需要针对 VGG 模型对像素值进行适当的缩放。我们现在已经准备好获取特性了。**

**![](img/609be669ea950622b428713f0b9eef94.png)**

**输出最后一个最大池图层的要素形状和要素集**

# **用 VGG16 从任意中间层提取特征**

**这里，我们首先从 tensorflow keras 导入 VGG16 模型。导入 image 模块来预处理图像对象，导入 preprocess_input 模块来为 VGG16 模型适当地缩放像素值。numpy 模块是为数组处理而导入的。此外，模型模块被导入以设计新模型，该新模型是完整 VGG16 模型中的层的子集。该模型将具有与原始模型相同的输入层，但输出将是给定卷积层的输出，我们知道这将是该层或特征图的激活。然后，使用 imagenet 数据集的预训练权重加载 VGG16 模型。例如，加载 VGG 模型后，我们可以定义一个新模型，从 block4 池层输出一个特征图。在定义了模型之后，我们需要加载模型期望大小的输入图像，在本例中是 224×224。接下来，图像 PIL 对象需要被转换为像素数据的 NumPy 数组，并从 3D 数组扩展为具有[ *个样本，行，列，通道* ]的维度的 4D 数组，这里我们只有一个样本。然后，需要针对 VGG 模型对像素值进行适当的缩放。我们现在已经准备好获取特性了。**

**例如，这里我们提取 block4_pool 层的特征。**

**![](img/dc27b0aac5c27661834db98a4213351c.png)**

**用 VGG16 提取 block4_pool 图层的特征**

# **使用 VGG19 提取特征**

**![](img/0c385b8bae7df1aa291f2645994c4b0a.png)**

**使用 VGG19 提取特征**

**这里我们先从 tensorflow keras 导入 VGG19 模型。导入 image 模块来预处理图像对象，导入 preprocess_input 模块来为 VGG19 模型适当地缩放像素值。numpy 模块是为数组处理而导入的。然后，使用 imagenet 数据集的预训练权重加载 VGG19 模型。VGG19 模型是一系列卷积层，后跟一个或几个密集(或全连接)层。Include_top 允许您选择是否需要最终的密集层。False 表示加载模型时不包括最终的密集图层。从输入层到最后一个 max pooling 层(标注为 7×7×512)作为模型的**特征提取部分**，网络的其余部分作为模型的**分类部分**。在定义了模型之后，我们需要加载模型期望大小的输入图像，在本例中是 224×224。接下来，图像 PIL 对象需要被转换为像素数据的 NumPy 数组，并从 3D 数组扩展为具有[*个样本、行、列、通道*]维度的 4D 数组，这里我们只有一个样本。然后，需要针对 VGG 模型对像素值进行适当的缩放。我们现在已经准备好获取特性了**

# **用 VGG19 从任意中间层提取特征**

**这里，我们首先从 tensorflow keras 导入 VGG19 模型。导入 image 模块来预处理图像对象，导入 preprocess_input 模块来为 VGG19 模型适当地缩放像素值。numpy 模块是为数组处理而导入的。此外，模型模块被导入以设计新模型，该新模型是完整 VGG19 模型中的层的子集。该模型将具有与原始模型相同的输入层，但输出将是给定卷积层的输出，我们知道这将是该层或特征图的激活。然后，使用 imagenet 数据集的预训练权重加载 VGG19 模型。例如，加载 VGG 模型后，我们可以定义一个新模型，从 block4 池层输出一个特征图。在定义了模型之后，我们需要加载模型期望大小的输入图像，在本例中是 224×224。接下来，图像 PIL 对象需要被转换为像素数据的 NumPy 数组，并从 3D 数组扩展为具有[ *个样本，行，列，通道* ]的维度的 4D 数组，这里我们只有一个样本。然后，需要针对 VGG 模型对像素值进行适当的缩放。我们现在已经准备好获取特性了。**

**例如，这里我们提取 block4_pool 层的特征。**

**![](img/7b5b75db08e10f9f24b5a7cfd88b7d32.png)**

**用 VGG19 提取 block4_pool 图层的特征**

# **总结 VGG16 模型各卷积层中的滤波器**

**![](img/a2a3dad6b73d38c0679cef290f73c5db.png)**

**总结 VGG16 模型各卷积层中的滤波器**

**过滤器是简单的权重，然而由于过滤器的专门的二维结构，权重值彼此具有空间关系，并且将每个过滤器绘制为二维图像是有意义的。这里我们回顾一下 VGG16 模型中的滤波器。这里我们从 tensorflow keras 导入 VGG19 模型。我们可以通过 *model.layers* 属性访问模型的所有层。每一层都有一个 *layer.name* 属性，其中卷积层有一个类似于 *block#_conv#* 的命名卷积，其中“ *#* ”是一个整数。因此，我们可以检查每个层的名称，并跳过任何不包含字符串' *conv* '的层。每个卷积层有两组权重。一个是滤波器模块，另一个是偏置值模块。这些可通过 *layer.get_weights()* 函数访问。我们可以检索这些重量，然后总结它们的形状。上面给出了总结模型过滤器的完整示例，下面显示了结果。**

**![](img/4309f817b50cc0c55b1a745d3a15cfa4.png)**

**VGG16 模型各卷积层中的滤波器**

**所有卷积层都使用 3×3 滤波器，这种滤波器很小，也许很容易解释。卷积神经网络的架构问题是滤波器的深度必须匹配滤波器的输入深度(例如通道的数量)。我们可以看到，对于具有红色、绿色和蓝色三个通道的输入图像，每个过滤器的深度为三(这里我们使用的是通道最后的格式)。我们可以将一个过滤器想象成一个有三个图像的图，每个通道一个图像，或者将所有三个图像压缩成一个彩色图像，或者甚至只看第一个通道，并假设其他通道看起来相同。**

# **在 VGG16 模型的第二层中可视化 64 个过滤器中的前 6 个过滤器**

**![](img/4bd82879326d4463058ecc4f4f278fce.png)**

**在 VGG16 模型的第二层中可视化 64 个过滤器中的前 6 个过滤器**

**这里我们从 VGG16 模型的第二个隐藏层检索权重。权重值可能是以 0.0 为中心的小正值和负值。我们可以将它们的值归一化到 0–1 的范围内，使它们易于可视化。我们可以列举该模块 64 个滤波器中的前六个，并绘制每个滤波器的三个通道。我们使用 matplotlib 库，将每个过滤器绘制为新的一行子图，将每个过滤器通道或深度绘制为新的一列。这里，我们绘制了 VGG16 模型中第一个隐藏卷积层的前六个滤波器。**

**![](img/981f315520d15105fd89a2c985de6a62.png)**

**VGG16 模型第二层 64 个滤波器中的前 6 个滤波器**

**它创建了一个具有六行三个图像或 18 个图像的图形，每个过滤器一行，每个通道一列。我们可以看到，在某些情况下，各通道的滤波器是相同的(第一行)，而在其他情况下，滤波器是不同的(最后一行)。深色方块表示较小或抑制性重量，浅色方块表示较大重量。利用这种直觉，我们可以看到第一行的过滤器检测到从左上角的亮到右下角的暗的渐变。**

# **汇总每个 Conv 图层的要素地图大小**

**激活图称为特征图，捕捉将过滤器应用于输入的结果，例如输入图像或另一个特征图。可视化特定输入图像的特征图的想法是理解在特征图中检测到或保留了输入的什么特征。期望靠近输入的特征地图检测小的或精细的细节，而靠近模型输出的特征地图捕获更一般的特征。为了探索特性图的可视化，我们需要用于创建激活的 VGG16 模型的输入。**

**![](img/fad7d9ed770cfa183aebc7d454be9c08.png)**

**使用 VGG16 汇总每个 conv 图层的要素地图大小**

**我们需要更清楚地了解每个卷积层输出的特征图的形状和层索引号。因此，我们枚举模型中的所有层，并打印每个卷积层的输出大小或特征图大小以及模型中的层索引。**

**![](img/41766c62781d2d57645aed97981af405.png)**

**使用 VGG16 时每个 conv 图层的要素地图大小**

# **可视化输入图像的 VGG16 模型中的第一卷积层的特征图**

**![](img/0b038d08ea2542832d4939c0e3bb23e6.png)**

**可视化输入图像的 VGG16 模型中的第一卷积层的特征图**

**这里，我们设计了一个新模型，它是完整 VGG16 模型中各层的子集。该模型将具有与原始模型相同的输入层，但输出将是给定卷积层的输出，我们知道这将是该层或特征图的激活。加载 VGG 模型后，我们可以定义一个新模型，从第一个卷积层输出特征图。利用该模型进行预测将给出给定输入图像的第一卷积层的特征图。在定义了模型之后，我们需要加载模型期望大小的输入图像，在本例中是 224×224。接下来，图像 PIL 对象需要被转换为像素数据的 NumPy 数组，并从 3D 数组扩展为具有[ *个样本，行，列，通道* ]的维度的 4D 数组，这里我们只有一个样本。然后，需要针对 VGG 模型对像素值进行适当的缩放。我们现在准备好得到特征图。我们可以通过调用 *model.predict()* 函数并传入准备好的单个图像来轻松实现。我们知道结果将是一个 224x224x64 的特征地图。我们可以将所有 64 幅二维图像绘制成一个 8×8 的正方形图像。**

**![](img/702ceaa513fb5b45c1d2e35973240a67.png)**

**输入图像的 VGG16 模型中第一个卷积层的特征映射**

**对于给定的图像，**

**![](img/c93790ec4a8f0e30633628b03e8007b0.png)**

**输入图像**

# ****可视化 VGG16 模型五个主要区块的特征图****

**在这里，我们从模型的每个块中一次性收集特征图输出，然后创建每个块的图像。图像中有五个主要块(例如，块 1、块 2 等。)结束于汇集层。每个块中最后一个卷积层的层索引是[2，5，9，13，17]。我们可以定义一个具有多个输出的新模型，每个块中的每个最后卷积层有一个特征映射输出。使用这个新模型进行预测将会产生一个特征图列表。我们知道在更深的层中的特征图的数量(例如深度或通道的数量)比 64 多得多，例如 256 或 512。然而，为了一致性，我们可以将可视化的特征地图的数量限制在 64 个。这里，我们为输入图像的 VGG16 模型中的五个块分别创建五个单独的图。**

**![](img/4edb0a7d633fd159a35743c165f9ad45.png)**

**可视化 VGG16 模型五个主要模块的特征图**

**运行该示例会产生五个图，显示 VGG16 模型的五个主要模块的特征图。我们可以看到，更接近模型输入的特征映射捕获了图像中的许多精细细节，并且随着我们向模型的更深处前进，特征映射显示的细节越来越少。这种模式是意料之中的，因为模型将图像中的特征抽象成更一般的概念，可用于进行分类。虽然从最终的图像看不出模型看到了一辆汽车，但我们普遍失去了解读这些更深层特征地图的能力。**

**![](img/2444c2bc4285d1a11c68fd11ccd3d589.png)**

**从 VGG16 模型中的块 1 提取的特征图的可视化**

**![](img/8aab83e6fb1a240728bb0bbe7b22ed90.png)**

**VGG16 模型中从区块 2 提取的特征图的可视化**

**![](img/f8f0189853112bd61def1ce084a69c31.png)**

**VGG16 模型中从区块 3 提取的特征图的可视化**

**![](img/787f07f519c9bb5064fd41bba22f3133.png)**

**VGG16 模型中从区块 4 提取的特征图的可视化**

**![](img/fa2b824dba17a186e080a63215a54cba.png)**

**VGG16 模型中从区块 5 提取的特征图的可视化**

**对于给定的图像，**

**![](img/c93790ec4a8f0e30633628b03e8007b0.png)**

**输入图像**

**希望您已经获得了一些关于如何在 VGG16 和 VGG19 CNN 模型中提取特征、可视化过滤器和特征图的良好知识。更多精彩文章敬请期待。**