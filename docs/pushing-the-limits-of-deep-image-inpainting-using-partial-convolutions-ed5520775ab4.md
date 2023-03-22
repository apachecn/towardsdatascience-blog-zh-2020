# 利用部分卷积推进深度图像修复的极限

> 原文：<https://towardsdatascience.com/pushing-the-limits-of-deep-image-inpainting-using-partial-convolutions-ed5520775ab4?source=collection_archive---------11----------------------->

## 基于部分卷积的不规则孔洞图像修复

![](img/1fdff3de676fcaed6aa4a9be7b9d1ab9.png)

图一。使用部分卷积的一些修复结果。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf) [1]

你好。今天我想讲一个好的深度图像修复纸，它打破了以往修复工作的一些局限。简而言之，以前的大多数论文都假设缺失区域是规则的(即一个中心缺失矩形孔或多个小矩形孔)，本文提出了一个**部分卷积(PConv)** 层来处理不规则孔。图 1 显示了使用建议的 PConv 的一些修复结果。他们好吗？大家一起来把握 PConv 的主旨吧！

# 动机

首先，**先前的深度图像修复方法将丢失像素和有效像素视为相同的**，在这种意义上，它们将固定像素值(归一化之前/之后为 255 或 1)填充到图像中的所有丢失像素，并将标准卷积应用到输入图像以完成修复任务。这里有两个问题。 *i)* 将缺失像素的像素值固定为预定义值是否合适？ *ii)* 不管像素是否有效，是否适合对输入图像进行卷积？因此，仅对有效像素执行操作可能是一个好的选择。

![](img/c76361b832f751845f63060036aaabfc.png)

图二。使用规则掩蔽图像和提出的部分 Conv 训练的先前深度修复方法的视觉比较。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf) [1]

其次，**现有方法假设缺失区域是规则的/矩形的**。其中一些采用本地鉴别器来区分生成内容和真实内容。对于固定大小的中心缺失孔的情况，他们将填充的中心孔输入到局部鉴别器以增强局部纹理细节。但是不规则的缺失区域呢？有没有可能在不使用鉴别器的情况下获得精细的局部细节？如果您尝试使用现有的方法来处理不规则的蒙版图像，您会发现修复结果并不令人满意，如图 2 所示。对于实用的修复方法，它们应该能够处理不规则的掩蔽图像。

# 介绍

与我以前的帖子类似，我假设读者对深度图像修复有基本的了解，如网络架构、损失函数(即 L1 和对抗性损失)，以及相关术语(即有效像素、缺失像素等)。).如果你需要或者想要，请快速回忆一下[我以前的帖子](https://lichutak.medium.com/)。在这一节中，我将简要介绍我认为不太重要的内容，因此我们可以有更多的时间来深入本文最重要的思想，部分卷积。

本文的作者采用了一个具有跳跃连接的类似于 **U-Net 的网络**，其中所有标准卷积层都被提议的部分卷积层所取代。如果你对他们的网络架构感兴趣，你可以参考[的论文](https://arxiv.org/pdf/1804.07723.pdf)，他们提供了他们模型的详细表格。

有趣的是，在这项工作中没有使用鉴别器。**除了标准的 L1 损失和全变差损失(TV 损失)**之外，作者采用了**两种高级特征损失**来完成具有精细纹理的掩蔽图像。后面我会详细介绍这两个损耗。

# 解决方案(聚焦)

正如在 Motivation 中提到的，关键思想是在卷积过程中从有效像素中分离出丢失的像素，使得卷积的结果只取决于有效像素。这就是所提出的卷积被命名为部分卷积的原因。基于可以自动更新的二进制掩码图像，对输入执行部分卷积。

# 方法

# 部分卷积层

让我们定义 **W** 和 *b* 为卷积滤波器的权重和偏差。 **X** 表示被卷积的像素值(或特征激活值), **M** 是相应的二进制掩码，表示每个像素/特征值的有效性(0 表示缺失像素，1 表示有效像素)。计算建议的部分卷积，

![](img/b953a9ea1a264b7435e8c5ebcde7af9a.png)

其中，⦿表示逐元素乘法，而 **1** 是一个与 **M** 形状相同的 1 的矩阵。从这个等式可以看出，部分卷积的结果只取决于有效的输入值(如 **X** ⦿ **M** )。sum(**1**)/sum(**M**)是一个比例因子，用于调整结果，因为每个卷积的有效输入值的数量是变化的。

**在每个部分卷积层**后更新二进制掩码。所提出的更新二进制掩码的规则非常简单。如果当前卷积的结果以至少一个有效输入值为条件，则相应的位置将被视为对下一个部分卷积层有效。

![](img/8f26c4bb653ecba78cabe45c1c084589.png)

正如您在上面看到的，更新规则很容易理解。

![](img/ab9729cfae49bf38298887928576bc06.png)

图 3。提议的部分卷积的图解说明。作者图片

图 3 给出了一个简单的例子来说明所提出的部分卷积。我们考虑一个简单的 5×5 输入及其相应的 5×5 二进制掩模图像(1 代表有效像素，0 代表孔洞像素)和一个具有固定权重的 3×3 **W** 。假设我们希望保持与输入大小 5×5 相同的输出大小，因此我们在进行卷积之前执行零填充。我们先考虑左上角(橙色有界)。该卷积的 **X** 和 **M** 在图中清楚示出，有效输入值的数量为 3。因此，这个位置的输出是-9+ *b* 。此外，更新后的二进制掩码中相应位置的值为 1，因为有 3 个有效输入值。

考虑中间(紫色有界)的框，这一次，如您所见，对于这个卷积没有有效的输入值，所以结果是 0+ *b* 并且更新的掩码值也是 0。右下角(蓝色边框)是另一个卷积示例，用于显示比例因子的作用。通过缩放因子，网络可以区分由 3 个有效输入值计算的-3 和由 5 个有效输入值计算的-3。

为了方便读者，图 3 的右上角显示了部分卷积层之后的更新二进制掩码。可以看到更新后的二进制掩码中的零更少了。**当我们执行越来越多的部分卷积时，二进制掩码将最终更新为全 1**。这意味着我们可以控制信息在网络内部传递，而不管缺失区域的大小和形状。

# 损失函数

总的来说，在它们的最终损失函数中有 4 个损失项，即 L1 损失、感知损失、风格损失和电视损失。

# L1 损失(每像素损失)

**该损失是为了确保逐像素重建精度**。

![](img/8eea3f64884c77e0ba68445b0a254951.png)

其中 **I** _ *out* 和 **I** _ *gt* 分别是网络和地面真实的输出。 *M* 是二进制掩码，0 代表孔洞，1 代表有效像素。*N*_**I**_*gt*是一幅图像中像素值的总数，等于*C*×*H*×*W*， *C* 是通道大小(RGB 图像为 3)， *H* 和 *W* 是图像的高度和宽度 **I** 可以看到 *L* _ *孔*和 *L* _ *有效*分别是孔像素和有效像素的 L1 损失。

# 感知损失(VGG 损失)

![](img/fe481c39aa2b95dd60e16f00a1582bf6.png)

感知损失是由 Gatys 等人[2]提出的，我们之前已经介绍过这种损失。简单地说，**我们希望填充图像和地面真实图像具有由像 VGG-16** 这样的预训练网络计算的相似特征表示。具体来说，我们将地面真实图像和填充图像馈送给预训练的 VGG-16 来提取特征。然后，我们计算所有层或几层的特征值之间的 L1 距离。

上式中， **I** _ *comp* 与 **I** _ *out* 相同，只是有效像素直接被地面真实像素代替。*ψ*^**I**_*p*是预训练的 VGG-16 在给定输入 **I** 的情况下计算出的第 *p* 层的特征图。*n*_*ψ*^**I**_*p*是*ψ*^**I**_*p*中元素的个数。根据 Gatys 等人[2]，当完整的图像在语义上接近其基础真实图像时，这种感知是小的。也许，这是因为更深的层(更高的级别)提供了图像的更多语义信息，并且**相似的高级特征表示表示完成的更好的语义正确性**。供读者参考，VGG-16 *池* 1、*池* 2、*池* 3 层用于计算感知损失。

# 风格丧失

![](img/d253c8b130245dee1fdaba160bb82dbf.png)

除了感知损失，作者还采用了如上所示的风格损失。你可以看到，风格损失也是使用预先训练的 VGG-16 给出的特征图来计算的。这一次，我们首先计算每个特征图的自相关性，它在[2]中被称为 Gram 矩阵。根据[2]， **Gram 矩阵包含图像的风格信息，如纹理和颜色**。这也是这种损失被命名为风格损失的原因。因此，我们计算完整图像和地面真实图像的格拉姆矩阵之间的 L1 距离。注意*ψ*^**I**_*p*的大小为(*h*_*p*×*w*_*p*×*c*_*p*，其克矩阵的形状为*c*_*p*×*c **K* _ *p* 是一个归一化因子，它取决于第 *p* 层特征图的空间大小。**

# 总变异损失

最终损失函数中的最后一项损失是电视损失。在我之前的帖子中，我们已经讨论过这种损失。简单来说，采用这个损失是为了**保证完成图像的平滑度**。这也是很多图像处理任务中常见的损失。

![](img/f29f61e1c673693d9af83b16ffcd1c15.png)

其中*N*_**I**_*comp*是 **I** _ *comp* 中像素值的总数。

# 最终损失

![](img/e625d58992d7be2b02559f94721b755a.png)

这是训练建议模型的最终损失函数。用于控制每个损失项的重要性的超参数是基于对 100 幅验证图像的实验来设置的。

# 消融研究

![](img/ec90d232f5b6bd111cc0438573aa18e7.png)

图 4。使用不同损失项的修复结果。(a)输入图像(b)没有风格损失的结果(c)使用完全损失的结果(d)背景事实(e)使用小风格损失权重的输入图像(f)结果(g)使用完全损失的结果(h)背景事实(I)没有感知损失的输入图像(j)结果(k)使用完全损失的结果(l)背景事实。请放大以便看得更清楚。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf)【1】

作者做了实验来显示不同损失项的影响。结果如上面的图 4 所示。首先，图 4(b)展示了不使用风格损失的修复结果。他们发现**在他们的模型中使用风格损失是必要的，以生成精细的局部纹理**。然而，风格损失的超参数必须仔细选择。正如您在图 4(f)中看到的，与使用完全损失的结果(图 4(g))相比，样式损失的小权重会导致一些明显的伪像。除了风格上的失落，感性上的失落也很重要。他们还发现**知觉损失的雇佣可以减少网格状的人工制品**。请参见图 4(j)和(k)了解使用感知损失的效果。

事实上，**的高级功能损失的使用还没有被充分研究过**。我们不能 100%说感知损失或风格损失一定对图像修复有用。因此，我们必须自己做实验来检查不同损失项对于我们期望的应用的有效性。

# 实验

![](img/29211db4d4c85b495aa3ea689af7b893.png)

图 5。掩模图像的一些例子。1、3、5 具有边界约束，而 2、4、6 没有边界约束。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf)

在他们的实验中，所有的掩模、训练和测试图像的尺寸都是 512×512。作者将测试图像分为两组， *i)* 边缘附近有孔的掩模。 *ii)* 靠近边框无孔口罩。具有距离边界至少 50 个像素的所有孔洞的图像被分类到第二组。图 5 显示了这两组掩码的一些示例。此外，作者根据孔与图像的面积比生成了 6 种类型的掩模:(0.01，0.1)，(0.1，0.2)，(0.2，0.3)，(0.3，0.4)，(0.4，0.5)，和(0.5，0.6)。这意味着最大的蒙版将遮蔽 60%的原始图像内容。

**训练数据。**与之前的工作类似，作者在 3 个公开可用的数据集上评估了他们的模型，即 ImageNet、Places2 和 CelebA-HQ 数据集。

![](img/c69ee532d0e0bde492f02508afccd856.png)

图 6。ImageNet 上不同方法的视觉比较。(a)输入图像(b) PatchMatch (c) GLCIC (d)上下文注意(e) PConv (f)地面真实。图片来自刘桂林等人的论文

![](img/c8ccf6551e9c50dac2adef85b97d446c.png)

图 7。不同方法在场所上的视觉比较 2。(a)输入图像(b) PatchMatch (c) GLCIC (d)上下文注意(e) PConv (f)地面真实。图片来自刘桂林等人的论文

图 6 和图 7 分别显示了 ImageNet 和 Places2 上不同方法的可视化比较。PatchMatch 是最先进的传统方法。 [GLCIC](/a-milestone-in-deep-image-inpainting-review-globally-and-locally-consistent-image-completion-505413c300df) 和[上下文注意](/a-breakthrough-in-deep-image-inpainting-review-generative-image-inpainting-with-contextual-1099c195f3f0)是我们之前介绍过的两种最先进的深度学习方法。如你所见，GLCIC (c)和上下文注意(d)不能提供具有良好视觉质量的修复结果。这可能是因为这两种先前的深度学习方法是针对规则屏蔽图像而不是不规则屏蔽图像训练的。如果您感兴趣，请放大以更好地查看修复结果。

![](img/cb38fd001bfa39920246a653a671d7e7.png)

图 8。CelebA-HQ 上不同方法的视觉比较。(a)输入图像(b)上下文注意(c) PConv (d)背景事实。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf) [1]

图 8 显示了 CelebA-HQ 数据集上的修复结果。您可以放大以更好地查看结果。

![](img/084b5f1c2039f3c04c0cfcb60e8964cb.png)

表 1。各种方法的定量比较。6 列代表 6 种不同的掩模比率。n 表示没有边界(即孔可以靠近边界)，B 表示有边界(即没有孔靠近边界)。刘桂林等人的数据来自他们的论文

表 1 列出了几个客观的评估指标，供读者参考。显然，所提出的 PConv 在几乎所有情况下都提供了最佳数字。注意，IScore 是用作视觉质量估计的初始分数，并且越低，估计的视觉质量越好。

除了定性和定量的比较，作者还进行了人类主观研究，以评估不同方法的视觉质量。感兴趣的读者可以参考[论文](https://arxiv.org/pdf/1804.07723.pdf)进行研究。

# 限制

![](img/54197deca94f4f47571d7e39b6351a41.png)

图 9。当缺失孔洞越来越大时，通过 PConv 进行修复。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf) [1]

![](img/e685e97e734b932b24a4a4cf4fc9c132.png)

图 10。一些失败的案例，尤其是当场景非常复杂的时候。图片来自刘桂林等人的[论文](https://arxiv.org/pdf/1804.07723.pdf)【1】

在文章的最后，作者还指出了现有深度图像修复方法的一些局限性。首先，很难完成如图 9 右侧所示的大面积缺失的图像。第二，当图像包含复杂的结构时，也很难完成如图 10 所示的具有良好视觉质量的图像。**目前还没有一种综合的方法来处理超大尺寸的复杂图像**。因此，你可以尝试提出一个好的解决方案来解决这个极端的图像修复问题。:)

# 结论

显然，部分卷积是本文的主要思想。希望我这个简单的例子能给大家解释清楚，部分卷积是怎么进行的，每一个部分卷积层之后，一个二值掩码是怎么更新的。通过使用部分卷积，卷积的结果将仅取决于有效像素，因此我们可以控制网络内部的信息传递，这对于图像修补任务可能是有用的(至少作者提供了部分卷积在他们的情况下是有用的证据)。除了图像修复，作者还试图将部分卷积扩展到超分辨率任务，因为它与图像修复有相似性。强烈推荐感兴趣的读者参考他们的[论文](https://arxiv.org/pdf/1804.07723.pdf)。

# 外卖食品

毫无疑问，我希望你能明白什么是部分卷积。从本文开始，后来的深度图像修复方法可以处理规则和不规则掩模。再加上我之前跟图像修复相关的帖子，也希望你能对图像修复这个领域有更好的了解。你应该知道一些常见的技术和图像修复的挑战。例如，膨胀卷积、上下文注意层等。当图像中的孔太大并且图像具有复杂的结构时，填充图像也是困难的。

# 下一步是什么？

下一次，我们将看另一篇论文，它利用额外的信息来帮助填充蒙版图像。希望你喜欢！让我们一起学习吧！:)

# 参考

[1]刘桂林、菲特瑟姆·a·瑞达、凯文·j·施、廷-王春、安德鲁·陶和布赖恩·卡坦扎罗，《[利用部分卷积对不规则孔洞进行图像修复》、 *Proc .2018 年欧洲计算机视觉会议* ( *ECCV* )。](https://arxiv.org/pdf/1804.07723.pdf)

[2] Leon A. Gatys，Alexander S. Ecker，and Matthias Bethge，《艺术风格的一种神经算法[》， *arXiv 预印本 arXiv:1508.06576* ，2015。](https://arxiv.org/pdf/1508.06576.pdf)

感谢您阅读我的帖子！如果您有任何问题，请随时给我发电子邮件或在这里留言。欢迎任何建议。再次非常感谢，希望下次再见！:)