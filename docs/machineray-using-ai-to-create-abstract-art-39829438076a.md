# MachineRay:用人工智能创造抽象艺术

> 原文：<https://towardsdatascience.com/machineray-using-ai-to-create-abstract-art-39829438076a?source=collection_archive---------8----------------------->

## 我如何使用公共领域绘画训练 GAN

![](img/4ba93a088ad8174676ad3bb3ab3057c4.png)

**机器阵列的样本输出**

在过去的三个月里，我一直在探索人工智能(AI)和机器学习(ML)的最新技术来创作抽象艺术。在我的调查中，我了解到创作抽象绘画需要三样东西:(A)源图像，(B)ML 模型，以及(C)在高端 GPU 上训练模型的大量时间。在我讨论我的工作之前，让我们先来看看一些先前的研究。

这是我关于人工智能如何用于创造性努力的系列文章的第一部分。第二部分是关于如何使用 ML 为新的故事生成情节，这里有[的](/got-writers-block-it-s-plotjam-to-the-rescue-e555db9f3272)。

# 背景

## 人工神经网络

早在 1943 年，沃伦麦卡洛克和沃尔特皮茨就为神经网络(NNs)创建了一个计算模型[1]。他们的工作导致了对大脑中生物过程和人工智能中神经网络使用的研究。理查德·纳吉菲在这篇[文章](/the-differences-between-artificial-and-biological-neural-networks-a8b46db828b7)中讨论了人工神经网络(ann)和生物大脑之间的差异。他描述了一个恰当的类比，我将在这里总结一下:**神经对于大脑就像飞机对于鸟类一样**。尽管这些技术的发展受到了生物学的启发，但是实际的实现是非常不同的！

![](img/db57c193e3424e675ca9de94ed9552a7.png)

**视觉类比**mikemacmarketin CC BY 2.0 的神经网络芯片图稿、biologycorner CC BY-NC 2.0 的大脑模型、Moto@Club4AG CC BY 2.0 的平面照片、ksblack99 CC PDM 1.0 的鸟类照片

人工神经网络和生物大脑都从外部刺激中学习，以理解事物和预测结果。一个关键的区别是，人工神经网络处理浮点数，而不仅仅是神经元的二进制触发。对于人工神经网络，它是数字输入和数字输出。

下图显示了典型人工神经网络的结构。左边的输入是包含输入刺激的数值。输入层连接到一个或多个包含先前学习记忆的隐藏层。输出层，在这种情况下只有一个数字，连接到隐藏层中的每个节点。

![](img/5b64e5d2fe1aa6451ad2c33f8d460984.png)

**典型人工神经网络图**

每个内部箭头代表数字权重，这些数字权重用作乘数，在网络中从左到右处理图层时修改图层中的数字。用输入值和预期输出值的数据集来训练该系统。权重最初被设置为随机值。对于训练过程，系统多次运行训练集，调整权重以实现预期的输出。最终，系统不仅能从训练集中正确预测输出，还能预测未知输入值的输出。这就是机器学习(ML)的本质。**智慧在砝码中**。关于人工神经网络培训过程的更详细的讨论可以在康纳麦当劳的帖子中找到，这里。

## 生成对抗网络

2014 年，蒙特利尔大学的 Ian Goodfellow 和七名合著者提交了一篇关于生成性对抗网络(GANs)的[论文](https://arxiv.org/pdf/1406.2661.pdf)[2]。他们想出了一种训练两个人工神经网络的方法，这两个人工神经网络可以有效地相互竞争，以创建像照片、歌曲、散文，是的，还有绘画这样的内容。第一个人工神经网络称为生成器，第二个称为鉴别器。生成器试图创建逼真的输出，在这种情况下，是一幅彩色绘画。鉴别器试图从训练集中辨别真实的绘画，而不是从生成器中辨别伪造的绘画。这是 GAN 架构的样子。

![](img/bf06ad84e772a120d70333f70bd203ac.png)

**生成性对抗网络**

一系列随机噪声被送入发生器，然后发生器使用其训练的权重来生成结果输出，在这种情况下，是彩色图像。通过在处理预期输出为 1 的真实绘画和预期输出为-1 的伪造绘画之间交替来训练鉴别器。在每幅画被发送到鉴别器后，它会发回详细的反馈，说明为什么这幅画不是真实的，生成器会根据这些新知识调整其权重，以尝试下次做得更好。**GAN 中的两个网络以对抗的方式被有效地一起训练**。生成器在试图将假图像冒充为真实图像方面变得更好，鉴别器在确定哪个输入是真实的，哪个是假的方面变得更好。最终，生成器在生成逼真的图像方面变得非常出色。你可以在 Shweta Goyal 的帖子[这里](https://medium.com/analytics-vidhya/gans-a-brief-introduction-to-generative-adversarial-networks-f06216c7200e)阅读更多关于 GANs 的内容，以及他们使用的数学。

## 用于大图像的改进的 GANs

尽管上述基本 GAN 适用于小图像(即 64×64 像素)，但对于大图像(即 1024×1024 像素)存在问题。由于像素的非结构化性质，基本 GAN 架构难以收敛到大图像的良好结果。它从树上看不到森林。英伟达的研究人员开发了一系列改进的方法，允许用更大的图像训练 GANs。第一种叫做【3】。

> 关键的想法是逐步增加生成器和鉴别器:从低分辨率开始，我们添加新的层，随着训练的进行，这些层可以模拟越来越精细的细节。这既加快了训练的速度，又极大地稳定了训练，使我们能够拍摄出前所未有的高质量图像。——**特罗·卡拉斯**等人。艾尔。，英伟达

NVIDIA 的团队继续他们的工作，使用 GANs 生成大的、真实的图像，将他们的架构命名为[StyleGAN](https://arxiv.org/pdf/1812.04948.pdf)【4】。他们以渐进增长的 GANs 作为基础模型，并添加了一个风格映射网络，将不同分辨率的风格信息注入到生成器网络中。

![](img/d0d5baff89d4ac367fcd741484f8a4c4.png)

**StyleGAN 组件图**

该团队利用 [StyleGAN](https://arxiv.org/pdf/1912.04958.pdf) 2 进一步改善了图像创建结果，使 GAN 能够高效地创建高质量的图像，减少不必要的伪影[5]。你可以在 Akria 的帖子“[从 GAN basic 到 StyleGAN2](https://medium.com/analytics-vidhya/from-gan-basic-to-stylegan2-680add7abe82) ”中了解更多关于这些发展的信息。

# 以前的工作，创造艺术与甘斯

自 GAN 于 2014 年推出以来，研究人员一直在寻求使用 GAN 来创作艺术。任伟·谭等人在 2017 年发表了一个名为 ArtGAN 的系统的描述。艾尔。来自日本长野信州大学[6]。他们的论文建议延长 GANs…

> …综合生成更具挑战性和更复杂的图像，如具有抽象特征的艺术品。这与大多数当前的解决方案形成对比，当前的解决方案侧重于生成自然图像，如室内、鸟、花和脸。——**任伟谭**等。艾尔。信州大学

Drew Flaherty 在澳大利亚布里斯班的昆士兰科技大学为他的硕士论文进行了一项关于使用 GANs 创作艺术的更广泛的调查[7]。他尝试了各种 GAN，包括基本 GAN、[cycle gan](https://arxiv.org/pdf/1703.10593.pdf)【8】、[BigGAN](https://arxiv.org/pdf/1809.11096.pdf)【9】、 [Pix2Pix](https://phillipi.github.io/pix2pix/) 和 StyleGAN。在他尝试的所有方法中，他最喜欢斯泰勒根。

> 这项研究的最佳视觉效果来自 StyleGAN。…考虑到模型仅进行了部分训练，输出的视觉质量相对较高，早期迭代的渐进改进显示了更明确的线条、纹理和形式、更清晰的细节以及更全面的构图。昆士兰科技大学的德鲁·弗莱厄蒂

为了他的实验，弗莱厄蒂使用了从各种来源收集的大量艺术作品，包括[WikiArt.org](https://www.WikiArt.org)、[谷歌艺术项目](https://artsandculture.google.com/)、[萨奇艺术](http://saatchiart.com)和 [Tumblr](https://www.tumblr.com/) 博客。他指出，并非所有的源图像都在公共领域，但他讨论了合理使用原则及其对 ML 和 AI 的影响。

# 机器射线

## 概观

在我的名为 MachineRay 的实验中，我从 WikiArt.org 收集了一些抽象画的图像，对它们进行处理，然后以 1024x1024 的尺寸输入到 StyleGAN2 中。我用 Google Colab 在 GPU 上训练了 GAN 三周。然后，我通过调整纵横比来处理输出图像，并通过另一个人工神经网络进行超分辨率调整。生成的图像宽或高为 4096 像素，具体取决于长宽比。这是组件图。

![](img/75cb8bae94f6754893714fac839064ae.png)

**机床部件图**

## 收集源图像

为了收集源图像，我写了一个 Python 脚本来收集 WikiArt.org 的抽象画。请注意，我过滤了图像，只得到被标记为“抽象”流派的绘画，以及被标记为公共领域的图像。这些包括 1925 年之前出版的图像或 1950 年之前去世的艺术家创作的图像。该系列中的顶级艺术家包括瓦西里·康丁斯基、特奥·凡·杜斯堡、保罗·克利、卡齐米尔·马列维奇、亚诺什·马蒂斯·托奇、贾科莫·巴拉和皮特·蒙德里安。下面是 Python 代码的一个片段，完整的源文件是[这里是](https://github.com/robgon-art/MachineRay/blob/master/scrape-wikiart-by-artist.py)。

我收集了大约 900 张图片，但是我删除了那些有代表性的或者太小的图片，把数量减少到了 850 张。这是源图像的随机抽样。

![](img/f61b20c1df6b6ef3479df3861a809963.png)

**公共领域中来自 WikiArt.org 的抽象画**的随机样本

## 移除框架

正如你在上面看到的，一些画在图像中保留了它们的木制框架，但是一些画的框架被裁剪掉了。例如，你可以在亚瑟·多佛的*风暴云*中看到这个框架。为了使源图像一致，并允许 GAN 专注于绘画的内容，我使用 Python 脚本自动移除了帧。下面是片段，完整的脚本是[这里是](https://github.com/robgon-art/MachineRay/blob/master/remove_frames.py)。

该代码打开每幅图像，并在边缘周围寻找与大部分绘画颜色不同的正方形区域。一旦找到边缘，图像将被裁剪以忽略该帧。下面是一些拆框前后的源画图片。

![](img/771a8d2d419cf2f0fd06b7f2bb851b41.png)

**自动裁剪的图片**来自 WikiArt.org 公共领域

## 图像增强

虽然 850 张图片看起来很多，但对于训练一只 GAN 来说，这还远远不够。如果没有足够多种类的图像，GAN 可能会过度拟合模型，这将产生较差的结果，或者更糟糕的是，陷入可怕的“模型崩溃”状态，这将产生几乎相同的图像。

StyleGAN2 具有从左到右随机镜像源图像的内置功能。因此，这将有效地将样本图像的数量增加一倍，达到 1，700 个。这是更好的，但仍然不是很大。我使用了一种称为图像增强的技术，将图像数量增加了 7 倍，达到 11，900 张。下面是我使用的图像增强的代码片段。完整的源文件是这里的。

该增强使用随机旋转、缩放、裁剪和温和的颜色校正来在图像样本中创建更多种类。请注意，在应用图像增强之前，我将图像的大小调整为 1024 乘 1024。我将在这篇文章中进一步讨论长宽比。以下是一些图像增强的例子。原文在左边，右边还有六个附加变奏。

![](img/07104854d6f52620688489f16eb0490d.png)

**图像增强的例子**在公共领域描绘来自 WikiArt.org 的图像

## 训练 GAN

我使用 Google Colab Pro 运行了培训。使用这项服务，我可以在高端 GPU 上运行长达 24 小时，这是一款 16 GB 内存的 NVIDIA Tesla P10。我还使用 Google Drive 来保留运行之间正在进行的工作。训练 GAN 花了大约 13 天的时间，通过系统发送了 500 万幅源图像。这是随机抽样的结果。

![](img/7a86b02d6d2a296cf78b43a21f8b5c9d.png)

【MachineRay 的样本输出

你可以从上面的 28 幅图像样本中看到，MachineRay 创作了各种风格的画作，尽管它们之间有一些视觉上的共性。在源图像中有风格的提示，但是没有精确的拷贝。

## 调整纵横比

虽然原始源图像有各种长宽比，从较薄的肖像形状到较宽的风景形状，但我将它们都做成方形，以帮助训练 GAN。为了让输出图像有多种长宽比，我在放大之前增加了一个新的长宽比。我没有选择一个纯粹随机的纵横比，而是创建了一个函数，它根据源图像中纵横比的统计分布来选择纵横比。这是分布图。

![](img/0c1942d8ca1eafcdcd792cf6eac06d8b.png)

**宽高比分布**来自 WikiArt.org 公共领域的图片。

上图描绘了所有 850 幅源图像的纵横比。它的范围从大约 0.5 到大约 2.0，前者是较窄的 1:2 比率，后者是较宽的 2:1 比率。图表显示了四个源图像，以指示它们在图表上的水平位置。下面是我的 Python 代码，它根据源图像的分布将 0 到 850 之间的一个随机数映射成一个纵横比。

我调整了上面的 MachineRay 输出，使下面的图片具有不同的纵横比。你可以看到这些图像看起来更自然，不那么同质，只有这一点小小的变化。

![](img/e6a1d9e605a41d5ac991179d352328fd.png)

**具有不同纵横比的 MachineRay 的样本输出**

## 超分辨率尺寸调整

从 MachineRay 生成的图像的最大高度或宽度为 1024 像素，这对于在计算机上查看是可以的，但是对于打印来说是不可以的。在 300 DPI 时，它只能以大约 3.5 英寸的尺寸打印。这些图像可以放大，但是如果以 12 英寸打印，看起来会很柔和。有一种使用人工神经网络来调整图像大小并保持清晰特征的技术，称为图像超分辨率(ISR)。更多关于超分辨率的信息，请点击这里查看 Bharath Raj 的帖子。

德国 Idealo 公司有一个很好的开源 [ISR 系统](http://github.com/idealo/image-super-resolution)，带有预先训练好的模型。他们的 GANs 模型使用在照片上训练过的 GANs 进行 4 倍的尺寸调整。我发现在 ISR 之前给图像添加一点随机噪声会产生一种绘画效果。下面是我用来对图像进行后处理的 Python 代码。

你可以在这里看到添加噪声和图像超分辨率调整的结果。注意纹理细节看起来有点像笔触。

![](img/85bc0eb4bd8570a49390811f190e8ae0.png)![](img/bf195cb886243677d43d87df85b68001.png)

**左图:添加噪声和 ISR 后的样本图像。右图:细节特写**

查看附录 A 中的图库，查看 MachineRay 的高分辨率输出示例。

# 后续步骤

其他工作可能包括以大于 1024x1024 的尺寸运行 GAN。将代码移植到张量处理单元(TPUs)而不是 GPU 上运行会使训练运行得更快。此外，来自 Idealo 的 ISR GAN 可以使用绘画而不是照片进行训练。这可能会给图像添加更真实的绘画效果。

# 感谢

我要感谢詹尼弗·林和奥利弗·斯特瑞普对这个项目的帮助和反馈。

# 源代码

这个项目的所有源代码都可以在 [GitHub](https://github.com/robgon-art/MachineRay) 上获得。一个用于生成图像的 Google Colab 在这里[可用](https://colab.research.google.com/github/robgon-art/MachineRay/blob/master/MachineRay_Image_Generation_2.ipynb)。源代码在 [CC BY-NC-SA 许可证](https://creativecommons.org/licenses/by-nc-sa/4.0/)下发布。

![](img/b315d79ed198829e5f3eea208c7bd3f1.png)

**署名-非商业性使用-类似分享**

# 参考

[1] W .麦卡洛克，w .皮茨，“神经活动中内在的思想逻辑演算”，*数学生物物理学通报*。5(4):115-133，1943 年 12 月

[2]伊恩，好伙计。“生成性对抗网络。”让·普吉-阿巴迪、迈赫迪·米尔扎、徐炳、戴维·沃德-法利、谢尔吉尔·奥泽尔、亚伦·库维尔、约舒阿·本吉奥，第一版，2014 年 6 月

[3] T. Karras、T. Aila、S. Laine 和 J. Lehtinen，“为提高质量、稳定性和变化性而逐步种植甘蔗”，CoRR，第 abs/1710.1 卷，2017 年 10 月

[4] T. Karras，S. Laine，T. Aila，“基于风格的生成对抗网络生成器架构”，CVPR2019，2019 年 3 月

[5] T. Karras、S. Laine、M. Aittala、J. Hellsten、J. Lehtinen 和 T. Aila，“分析和提高 StyleGAN 的图像质量”，2020 年 3 月

[6] W. R. Tan、C. S. Chan、H. E. Aguirre 和 K. Tanaka，“ArtGAN:使用条件分类 GAN 的艺术作品合成”，2017 年 4 月

[7] D. Flaherty，“机器学习的艺术方法”，昆士兰科技大学，硕士论文，2020 年

[8]朱军，帕克，伊索拉和，“使用循环一致的对抗网络进行不成对的图像到图像翻译”，2018 年 11 月

[9] A. Brock，J. Donahue 和 K. Simonyan，“高保真自然图像合成的大规模 GAN 训练”，2019 年 2 月

# 附录 A —机器射线结果图库

![](img/712c71ffb822be1374a7b81195350e3f.png)![](img/d70865fdd56d224e2290abdb14ccac4a.png)![](img/0b88531c46a0615f1cd52972d0231141.png)![](img/b03351efea4dd7ec6b8acbdabb262fce.png)![](img/8cac4a3a5501915ffec231f5ef45844d.png)![](img/f77cb1b1595793f0c196ec64c9b7dc57.png)![](img/5913f0e9626e348722536913f7e44eb0.png)![](img/4e167ba93c300366e9390ef8c0305006.png)![](img/1bc032ef667b84cd6f9558d878805b33.png)![](img/547894d5d8a15a541d7758d9e7b3d2dc.png)![](img/e7cbb6ad26d7125cac28d98ca396d652.png)![](img/09dc70d16a0cf001d0915469007cd38d.png)![](img/64e1db6dd3c8e200519323af2ff83ac4.png)![](img/c522adb8beb276ba3c052c078b2b5602.png)

为了无限制地访问 Medium 上的所有文章，[成为会员](https://robgon.medium.com/membership)，每月支付 5 美元。非会员每月只能看三个锁定的故事。