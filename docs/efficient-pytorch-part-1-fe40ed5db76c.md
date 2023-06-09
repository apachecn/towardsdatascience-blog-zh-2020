# 高效 PyTorch —消除瓶颈

> 原文：<https://towardsdatascience.com/efficient-pytorch-part-1-fe40ed5db76c?source=collection_archive---------8----------------------->

## 什么是高效的 PyTorch 培训渠道？它是产生具有最佳精确度的模型的那个吗？还是跑得最快的那个？还是容易理解和扩展的那个？可能是容易平行的那种？以上都是。

![](img/efdf7bfcad2f44a38f554d03712949d0.png)

哈里·谢尔顿在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

[PyTorch](https://pytorch.org/) 是一款用于研究和生产领域的优秀工具，斯坦福大学、Udacity、SalelsForce、Tesla 等都采用了这一深度学习框架，这清楚地表明了这一点..然而，每种工具都需要投入时间来掌握技能，以便最有效地使用它。在使用 PyTorch 两年多后，我决定总结一下我使用这个深度学习库的经验。

> 高效的—(指系统或机器)以最少的浪费努力或费用获得最大的生产率。(牛津语言)

高效 PyTorch 系列的这一部分给出了识别和消除 I/O 和 CPU 瓶颈的一般技巧。第二部分将揭示一些关于有效张量运算的技巧。第三部分——高效的模型调试技术。

*免责声明*:这篇文章假设你至少对 PyTorch 有所了解。

我将从最明显的一个开始:

![](img/6414439ca7be856a0c5dd034a5283106.png)

[Roshni Sidapara](https://unsplash.com/@roshnisidapara?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

> 建议 0: **知道代码中的瓶颈在哪里**

命令行工具，如`[nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface)`、`[htop](https://hisham.hm/htop/)`、`[iotop](https://linux.die.net/man/1/iotop)`、`[nvtop](https://github.com/Syllo/nvtop)`、`[py-spy](https://pypi.org/project/py-spy/)`、`[strace](https://strace.io/)`等..应该成为你最好的朋友。您的培训渠道是否受限于 CPU？IO 绑定？GPU 绑定？这些工具将帮助你找到答案。

你可能甚至没有听说过它们，或者听说过但没有使用过。没关系。如果你没有立即开始使用它们也没关系。请记住，其他人可能会用它们来训练 5%-10%-15%的模型..比你更快，这最终可能会决定你是赢得还是失去市场，或者在工作岗位上获得批准还是拒绝。

# 数据预处理

几乎每个培训渠道都从`Dataset`班开始。它负责提供数据样本。任何必要的数据转换和扩充都可以在这里进行。简而言之，`Dataset`是一个抽象，它报告其大小，并根据给定索引返回数据样本。

如果您正在处理类似图像的数据(2D、3D 扫描)，磁盘 I/O 可能会成为瓶颈。要获得原始像素数据，您的代码需要从磁盘读取数据，并将图像解码到内存中。每个任务都很快，但是当您需要尽可能快地处理成千上万的任务时，这可能会成为一个挑战。像 NVidia Dali 这样的库提供了 GPU 加速的 JPEG 解码。如果您在数据处理管道中面临 IO 瓶颈，这绝对值得一试。

还有一个选择。SSD 磁盘的访问时间约为 0.08–0.16 毫秒。RAM 的访问时间为纳秒。我们可以将数据直接存入内存！

> 建议 1: **如果可能的话，把你的数据全部或者部分移动到 RAM** 。

如果您有足够的 RAM 来加载并在内存中保存所有的训练数据，这是从管道中排除最慢的数据检索步骤的最简单方法。

这个建议对云实例特别有用，比如亚马逊的`p3.8xlarge`。这个实例有 EBS 磁盘，对于默认设置，它的性能非常有限。然而，这个实例配备了惊人的 248Gb 内存。这足以在内存中保存所有 ImageNet 数据集！你可以这样做:

我亲自面对了这个瓶颈问题。我有一台配备 4x1080Ti GPUs 的家用 PC。有一次，我拿了一个有四个 NVidia Tesla V100 的`p3.8xlarge`实例，并把我的训练代码移到那里。鉴于 V100 比我的老款 1080Ti 更新更快，我预计训练速度会提高 15-30%。当每个时期的训练时间增加时，我感到很惊讶！这是我的教训，要注意基础设施和环境的细微差别，而不仅仅是 CPU 和 GPU 的速度。

根据您的情况，您可以在 RAM 中保持每个文件的二进制内容不变，并“即时”解码，或者解压缩图像并保留原始像素。但是无论你选择哪条路，这里有第二条建议:

> 忠告二:**简介。测量。比较一下。每次你对渠道进行任何改变时，都要仔细评估它会产生什么样的整体影响。**

这个建议只关注训练速度，假设你没有引入模型、超参数、数据集等的变化..您可以有一个神奇的命令行参数(神奇的开关),当指定时，它将为一些合理数量的数据样本运行训练。有了这一功能，您可以随时快速分析您的管道:

```
# Profile CPU bottlenecks
python -m cProfile training_script.py --profiling# Profile GPU bottlenecks
nvprof --print-gpu-trace python train_mnist.py# Profile system calls bottlenecks
strace -fcT python training_script.py -e trace=open,close,read
```

> 建议 3: **离线预处理一切**

如果您正在对 512x512 大小的图像进行训练，这些图像是由 2048x2048 图片组成的，请事先调整它们的大小。如果您使用灰度图像作为模型的输入，请离线进行颜色转换。如果您正在进行 NLP —预先进行标记化并保存到磁盘。在训练中一遍又一遍地重复同样的操作是没有意义的。在渐进式学习的情况下，您可以保存多种分辨率的训练数据，这仍然比在线调整到目标分辨率要快。

对于表格数据，考虑在`Dataset`创建时将`pd.DataFrame`对象转换为 PyTorch 张量。

> 建议 4: **调整数据加载器的工作线程数量**

PyTorch 使用 DataLoader 类来简化为训练模型而生成批处理的过程。为了加快速度，它可以使用 python 的多处理并行处理。大多数情况下，它开箱即可正常工作。有几件事要记住:

每个进程生成一批数据，这些数据通过互斥同步提供给主进程。如果您有 N 个工作线程，那么您的脚本将需要 N 倍多的 RAM 来在系统内存中存储这些批处理。你到底需要多少内存？
我们来计算一下:

1.  假设我们为批量大小为`32`的城市风景和大小为`512x512x3 (height, width, channels)`的 RGB 图像训练图像分割模型。我们在 CPU 端进行图像标准化(稍后我会解释为什么它很重要)。在这种情况下，我们最终的图像张量将是`512 * 512 * 3 * sizeof(float32) = 3,145,728`字节。乘以批处理大小，我们得到`100,663,296`字节，或者大约 100 Mb。
2.  除了图像，我们还需要提供真实的面具。它们各自的大小是(默认情况下，masks 的类型是 long，8 字节)—— `512 * 512 * 1 * 8 * 32 = 67,108,864`或者大约 67 Mb。
3.  因此，一批数据所需的总内存为`167 Mb`。如果我们有 8 个工人，所需的内存总量将是`167 Mb * 8 = 1,336 Mb.`

听起来不算太糟，对吧？当您的硬件设置能够处理的批处理数量超过 8 个工作线程所能提供的数量时，就会出现问题。人们可以天真地放置 64 个工人，但这至少会消耗将近 11 Gb 的 RAM。

如果你的数据是 3D 体积扫描，事情会变得更糟；在这种情况下，即使是单通道卷`512x512x512`的一个样本也将占用 134 Mb，对于批量大小 32，它将是 4.2 Gb，对于 8 个工人，您将只需要 32 Gb 的 RAM 来在内存中保存中间数据。

这个问题有一个部分的解决方案，您可以尽可能地减少输入数据的通道深度:

1.  将 RGB 图像保持在每通道 8 位深度。图像转换为浮点和归一化可以很容易地在 GPU 上完成。
2.  在数据集中使用 uint8 或 uint16 数据类型，而不是 long。

通过这样做，您可以大大降低 RAM 需求。对于上面的例子，内存高效数据表示的内存使用量将是每批 33 Mb，而不是 167 Mb。那就是 5 倍还原！当然，这需要模型本身的额外步骤来将数据规范化/转换为适当的数据类型。然而，张量越小，CPU 到 GPU 的传输时间就越快。

应该明智地选择`DataLoader`的工人数量。您应该检查您的 CPU 和 IO 系统有多快，您有多少内存，以及 GPU 处理这些数据的速度有多快。

# 多 GPU 训练和推理

![](img/061067433811a428e9593a419105c7f5.png)

照片由 [Nana Dua](https://unsplash.com/@nanadua11?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

神经网络模型变得越来越大。如今的趋势是使用多个 GPU 来增加训练时间。幸运的是，它还经常提高模型的性能，使批量更大。PyTorch 拥有在几行代码内实现多 GPU 的所有特性。然而，有些警告乍一看并不明显。

`model = nn.DataParallel(model) # Runs model on all available GPUs`

使用多 GPU 最简单的方法是在`nn.DataParallel`类中包装一个模型。在大多数情况下，它工作得很好，除非你训练一些图像分割模型(或任何其他产生大尺寸张量作为输出的模型)。在正向传递结束时，`nn.DataParallel`将从主 GPU 上的所有 GPU 收集输出，以反向运行输出并进行梯度更新。

有两个问题:

*   GPU 负载不平衡
*   在主 GPU 上采集需要额外的视频内存。

首先，只有主 GPU 在进行损失计算、反向传递和梯度步骤，而其他 GPU 在 60C 下等待下一批数据。

其次，在主 GPU 上收集所有输出所需的额外内存通常会迫使您减少批量大小。事情是这样的，`nn.DataParallel`在 GPU 之间平均分割批处理。假设您有 4 个 GPU，总批量为 32。然后，每个 GPU 将获得其 8 个样本的块。但问题是，虽然所有非主 GPU 都可以轻松地将这些批处理放入其相应的 VRAM 中，但主 GPU 必须分配额外的空间来容纳来自所有其他卡的输出的 32 个批处理大小。

对于这种不均衡的 GPU 利用率，有两种解决方案:

1.  继续使用`nn.DataParallel`并在训练中计算向前传球的损失。在这种情况下，您不会将密集预测掩码返回给主 GPU，而是只返回一个标量损失。
2.  使用分布式训练，又名`nn.DistributedDataParallel`。在分布式培训的帮助下，您可以解决上述两个问题，并享受观看所有 GPU 100%加载的乐趣。

如果您知道要了解更多关于多 GPU 培训的信息，并深入了解每种方法的优缺点，请查看这些精彩的帖子以了解更多信息:

*   [https://medium . com/hugging face/training-large-batches-practical-tips-on-1-GPU-multi-GPU-distributed-settings-EC 88 C3 e 51255](https://medium.com/huggingface/training-larger-batches-practical-tips-on-1-gpu-multi-gpu-distributed-setups-ec88c3e51255)
*   [https://medium . com/@ the accelerators/learn-py torch-multi-GPU-proper-3eb 976 c 030 ee](https://medium.com/@theaccelerators/learn-pytorch-multi-gpu-properly-3eb976c030ee)
*   [https://towards data science . com/how-to-scale-training-on-multi-GPU-DAE 1041 f 49d 2](/how-to-scale-training-on-multiple-gpus-dae1041f49d2)

> 建议 5: **如果你有 2 个以上的 GPU，考虑使用分布式训练模式**

它将节省多少时间在很大程度上取决于您的场景，但我观察到，当在 4x1080Ti 上训练图像分类管道时，时间减少了约 20%。

同样值得一提的是，您也可以使用`nn.DataParallel`和`nn.DistributedDataParallel`进行推理。

# 关于自定义损失函数

编写自定义损失函数是一项有趣且令人兴奋的工作。推荐大家不定期尝试一下。在用复杂的逻辑实现损失函数时，有一件事你必须记住:它都运行在 CUDA 上，你有责任编写 CUDA 高效的代码。CUDA-efficient 的意思是“没有 python 控制流”。在 CPU 和 GPU 之间来回切换，访问 GPU 张量的单个值可能会完成工作，但性能会很糟糕。

前一段时间，我实现了一个定制的余弦嵌入损失函数，用于实例分割，来自“[使用余弦嵌入和递归沙漏网络分割和跟踪细胞实例](https://www.sciencedirect.com/science/article/pii/S136184151930057X?via%3Dihub)”的论文。它的文本形式非常简单，但是实现起来有点复杂。

我写的第一个天真的实现(除了 bug)花了几分钟(！)来计算单个批次的损失值。为了分析 CUDA 瓶颈，PyTorch 提供了一个非常方便的内置分析器。它使用起来非常简单，并且为您提供了解决代码瓶颈的所有信息:

> 建议 9: **如果您正在设计定制模块&损耗—剖析&测试它们**

在对我的初始实现进行概要分析之后，我能够将我的实现速度提高 100 倍。关于用 PyTorch 编写高效张量表达式的更多内容将在高效 PyTorch —第 2 部分中解释。

# 时间与金钱

![](img/ecbc2f97f7b66395169b1f9a324ee6bd.png)

帕特里克·福尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

最后但同样重要的一点是，有时投资于更强大的硬件比优化代码更有价值。软件优化永远是一个高风险的旅程，有不确定的结果。升级 CPU、RAM、GPU 或全部一起升级可能更有效。金钱和工程时间都是资源，正确利用二者是成功的关键。

> 建议 10: **一些瓶颈可以通过硬件升级更容易地解决**

# 结论

充分利用你的日常工具是精通的关键。试着不要走捷径，如果有些事情你不清楚，一定要深入挖掘。总有机会获得新知识。问问你自己或你的伙伴——“我的代码如何改进？”。我真的相信，对于计算机工程师来说，这种完美感和其他技能一样重要。

Eugene 是计算机视觉和机器学习工程师，拥有超过 10 年的软件开发经验。《[掌握 OpenCV 用于实用计算机视觉项目](https://www.amazon.com/Mastering-OpenCV-Practical-Computer-Projects/dp/1849517827/ref=sr_1_2?dchild=1&keywords=Mastering+OpenCV+for+practical&qid=1591877326&sr=8-2)》一书的作者。卡格尔[大师](https://www.kaggle.com/bloodaxe)。[白蛋白](https://github.com/albumentations-team/albumentations)核心团队成员。《pytorch-toolbelt 的作者。OpenCV、PyTorch 和 Catalyst 贡献者。[https://www.linkedin.com/in/cvtalks/](https://www.linkedin.com/in/cvtalks/)