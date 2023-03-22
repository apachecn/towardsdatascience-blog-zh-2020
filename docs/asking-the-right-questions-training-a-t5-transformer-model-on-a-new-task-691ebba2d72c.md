# 问正确的问题:在新任务中训练 T5 变压器模型

> 原文：<https://towardsdatascience.com/asking-the-right-questions-training-a-t5-transformer-model-on-a-new-task-691ebba2d72c?source=collection_archive---------8----------------------->

## T5 转换器将任何 NLP 任务构建为文本到文本的任务，使预先训练的模型能够轻松学习新任务。让我们教老狗一个新把戏！

![](img/db86d1cc34fa6500487e3e2d0ac9a486.png)

图片由 [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=662711) 的 [Katrin B.](https://pixabay.com/users/825545-825545/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=662711) 提供

自从 2019 年 10 月 *way* 推出 T5(文本到文本转换变压器)以来，我就一直渴望尝试它(这是一个漫长的几个月)。我尝试了几次谷歌的开源代码[和](https://github.com/google-research/text-to-text-transfer-transformer)，但是我从来没有让它正常工作过。其中的一些超出了我的理解范围(张量流)😫)所以我想我要等拥抱脸来救援了！和往常一样，[变压器](https://github.com/huggingface/transformers)的实现更容易使用，我对它进行了修改，以便与[简单变压器](https://github.com/ThilinaRajapakse/simpletransformers)一起使用。

在我们开始*精彩内容*之前，先简单介绍一下 T5 车型是什么，以及它为何如此令人兴奋。根据谷歌人工智能博客 T5 上的[文章](https://ai.googleblog.com/2020/02/exploring-transfer-learning-with-t5.html)所述，该模型是一项关于迁移学习技术的大规模研究([论文链接](https://arxiv.org/abs/1910.10683))的结果，旨在了解哪种方法最有效。T5 模型在 C4 ( [巨大干净的爬行语料库](https://www.tensorflow.org/datasets/catalog/c4))上进行预训练，这是一个新的绝对*大规模的*数据集，与模型一起发布。

*预训练是迁移学习的第一步，在这一步中，模型在大量未标记的文本数据上进行自我监督的任务训练。在此之后，该模型在为特定任务定制的较小的标记数据集上进行微调(训练)，与在没有预训练的情况下简单地在较小的标记数据集上进行训练相比，产生了优越得多的性能。关于预训练语言模型的更多信息可以在我下面的帖子中找到。*

[](/understanding-electra-and-training-an-electra-language-model-3d33e3a9660d) [## 理解 ELECTRA 并训练一个 ELECTRA 语言模型

### 变形金刚模型如何学习语言？伊莱克特拉有什么新消息？你如何在一个平台上训练你自己的语言模型

towardsdatascience.com](/understanding-electra-and-training-an-electra-language-model-3d33e3a9660d) 

T5 模型的一个关键区别是所有的 NLP 任务都是以文本到文本的格式呈现的。另一方面，BERT-like 模型将文本序列作为输入，并从输入中输出单个类标签或一段文本。通过在 transformer 模型之上添加相关的输出层，针对特定任务对 BERT 模型进行了改进。例如，为分类任务添加一个简单的线性分类图层。然而，T5 避开了这种方法，而是重新构建任何 NLP 任务，使得输入和输出都是文本序列。这意味着相同的 T5 模型可用于任何 NLP 任务，无需对架构进行任何售后更改。要执行的任务可以通过一个简单的前缀(也是一个文本序列)来指定，该前缀被添加到输入中，如下所示。

![](img/7150693a532d4bba5d91986a0fbc8cde.png)

来自[https://ai . Google blog . com/2020/02/exploring-transfer-learning-with-t5 . html](https://ai.googleblog.com/2020/02/exploring-transfer-learning-with-t5.html)

T5 [的论文](https://arxiv.org/abs/1910.10683)探讨了 NLP 迁移学习的许多最新进展。很值得一读！

然而，本文的重点是调整 T5 模型来执行新的 NLP 任务。由于统一的文本到文本的方法，这变得(令人惊讶地)容易。所以，让我们来看看前面提到的*好东西*！

# 任务

T5 模型在各种各样的 NLP 任务上被训练，包括文本分类、问题回答、机器翻译和抽象概括。我们将教授 T5 模型的任务是**问题生成**。

具体来说，当给定一个上下文时，模型的任务是*询问相关问题*。

*您可以在简单变形金刚回购的* [*示例*](https://github.com/ThilinaRajapakse/simpletransformers/tree/master/examples/t5) *目录中找到本指南使用的所有脚本。*

# 数据集

我们将使用[亚马逊评论数据(2018)](https://nijianmo.github.io/amazon/index.html) 数据集，其中包含亚马逊上各种产品的描述以及与这些产品相关的问答对。

描述和问答配对必须单独下载。您可以按照下面的*描述*和*问答对*中的说明手动下载数据，也可以使用提供的 shell 脚本。本研究中使用的类别列表如下。

## 描述

1.  转到[评论网址](http://deepyeti.ucsd.edu/jianmo/amazon/index.html)。
2.  从页面上的链接下载*元数据*文件(json.gz)。请注意，从**每个类别的数据链接** *(例如*[*http://deepyeti . ucsd . edu/简墨/亚马逊/metaFiles/meta _ AMAZON _ fashion . JSON . gz*](http://deepyeti.ucsd.edu/jianmo/amazon/metaFiles/meta_AMAZON_FASHION.json.gz)*)*下载可能比下载所有产品的完整**元数据**更好。完整的元数据是一个 24 GB 的档案，您将需要一个*lot*RAM 来处理它。
3.  将`*meta_ALL_Beauty.json.gz*` 重命名为 `*meta_Beauty.json.gz*` 以匹配问答文件中的名称。

## 问答配对

1.  转到[问答网址](http://deepx.ucsd.edu/public/jmcauley/qa/)。
2.  下载**每个类别的文件**。请注意，我使用的是没有多个答案的问答配对。

## 命令过程

或者，下面的 shell 脚本应该通过读取下面给出的两个文本文件的链接来下载所有必要的文件(将文本文件放在与 shell 脚本相同的目录`data/`)。它还会将`*meta_ALL_Beauty.json.gz*` 重命名为 `*meta_Beauty.json.gz*` 以匹配问答文件中的名称。

链接到元 JSON 文件

qa JSON 文件的链接

下载 JSON 文件的 Shell 脚本

有了数据文件，我们就可以开始训练我们的模型了！

# 设置

我们将使用[简单变形金刚](https://github.com/ThilinaRajapakse/simpletransformers)库(基于拥抱脸[变形金刚](https://github.com/huggingface/transformers))来训练 T5 模型。

下面给出的说明将安装所有的要求。

1.  从[这里](https://www.anaconda.com/distribution/)安装 Anaconda 或者 Miniconda 包管理器。
2.  创建新的虚拟环境并安装软件包。
    `conda create -n simpletransformers python pandas tqdm`
    `conda activate simpletransformers`
    
3.  如果您使用 fp16 培训，请安装 Apex。请遵循此处的说明[。(从 pip 安装 Apex 给一些人带来了问题。)](https://github.com/NVIDIA/apex)
4.  安装简单变压器。
    `pip install simpletransformers`

*参见安装* [*文档*](https://simpletransformers.ai/docs/installation/#installation-steps)

# 数据准备

我们可以使用下面给出的脚本处理数据文件，并以方便的格式保存它们。这也将把数据分成训练集和评估集。

*改编自亚马逊评论数据* [*页面*](https://nijianmo.github.io/amazon/index.html) *给出的有帮助的脚本。*

*检查您的* `*data/*` *目录中是否有*`*train_df.tsv*`*`*eval_df.tsv*`*文件。**

# *训练模型*

## *数据格式*

*T5 模型的输入数据应该是包含 3 列的 Pandas 数据帧，如下所示。*

*   *`prefix`:表示要执行的任务的字符串。*
*   *`input_text`:输入的文本序列。*
*   *`target_text`:目标序列。*

*在内部，简单的转换器将从熊猫数据帧中构建适当格式化的*输入*和*目标*序列(如下所示)。*

*T5 模型的*输入*具有以下模式:*

```
*"<prefix>: <input_text> </s>"*
```

**目标*序列有如下模式:*

```
*"<target_sequence> </s>"*
```

**前缀*值指定了我们希望 T5 模型执行的任务。为了训练 T5 模型执行新任务，我们简单地训练模型，同时指定适当的*前缀。在这种情况下，我们将使用前缀`ask_question`。即，我们的数据帧中的所有行在前缀列中将具有值`ask_question`。**

## *培养*

*使用简单的变压器训练模型非常简单。*

*正如您可能从培训脚本中观察到的，我们正在使用`t5-large`预培训模型。在`t5-large`模型上使用这些参数需要用一个泰坦 RTX GPU 进行大约 12 个小时的训练。根据你的 GPU 资源，你可以增加`train_batch_size`来加快训练速度，或者你可以减少它来适应带有更少 VRAM 的 GPU(泰坦 RTX 有 24 GB)。*

**注意，您可以通过增加* `*gradient_accumulation_steps*` *来抵消小批量的影响。有效批量大致等于* `*train_batch_size * gradient_accumulation_steps*` *。**

*您还可以通过选择`t5-base`模型来显著提高训练速度和 GPU 内存消耗。这可能会导致*相对*更差(但绝不是*差*)的模型。*

*该训练脚本还将使用[权重&偏差](https://www.wandb.com/)框架自动记录训练进度。你可以在这里看到我的日志。*

# *评估模型*

*评估一个语言生成模型比评估一个分类模型稍微复杂一些。这是因为没有正确的答案可以和分类模型进行比较。评估数据集包含人们对这些产品的描述和问题，但这并不意味着这些是你可以问的唯一*正确*的问题。*

*因此，评估语言生成模型的最佳方式之一是生成文本，并让一个实际的人(或几个人)对其进行评估。*

*说到生成文本，过去几年解码算法令人印象深刻的发展导致了能够生成非常真实的文本序列的模型。(*解码算法用于生成文本)**

*以下部分简要概述了当前使用的流行解码算法。*

## *解码算法*

*这一部分主要基于关于文本生成的拥抱脸[笔记本](https://github.com/huggingface/blog/blob/master/notebooks/02_how_to_generate.ipynb)。我强烈推荐阅读这本笔记本，以便更深入地理解解码算法，因为它很好地解释了算法并展示了如何使用它们。*

1.  *贪婪搜索—在每个时间步长选择概率最高的单词作为下一个单词。T5 论文将该算法用于短序列生成(例如分类)。*
2.  *波束搜索——在每个时间步跟踪`n`最可能的假设(基于单词概率),并最终选择总体概率最高的假设。(`n`是光束的数量)*
3.  *Top-K sampling —在每个时间步从 *K 个*最可能的下一个单词中随机抽取一个单词。每一步可供选择的单词数量是固定的。*
4.  *Top-p 采样—从最小可能单词集中采样一个单词，该单词的累积概率(每个单词的概率之和)超过每个时间步长的概率 *p* 。每一步可供选择的单词数量是动态的。*

*我们将结合使用 Top-K 和 Top-p 抽样技术，通过 T5 模型生成问题。这种策略通常会产生看起来更自然的文本。*

## *问题生成*

*简单变压器 T5 模型的`predict()`方法用于生成预测，或者在我们的情况下，生成问题。*

*这里，我们为`eval_df`数据集中的每个描述生成 3 个问题。*

*让我们来看看一些样品。*

**只是为了好玩，我将生成的问题与数据集中的实际问题混在了一起。每个描述有 4 个问题，其中 3 个是生成的，一个是原始的。看你能不能分辨出哪个是哪个！我很想在评论中看到你的猜测。*😉*

## *样本 1*

*描述:*

> *Smart Solar San Rafael II Solar Mission Lantern 将为任何户外环境提供优雅的氛围，是您的露台、甲板或花园的理想选择:由全天候聚塑料制成，具有种子玻璃效果，15 英寸的灯笼可以放在任何表面上，也可以使用集成的挂环悬挂。Rafael II 由顶部的两个暖白色 LED 照明，灯内有一根蜡烛，灯内有一个琥珀色 LED，产生温暖的发光效果。Rafael II 由一体式单晶太阳能电池板和可充电镍氢电池供电，无需布线或运营成本。灯笼在黄昏时自动打开，在黎明时自动关闭。Smart Living Home & Garden 为从授权分销商和零售商处购买的全部产品提供自最初购买日期起 1 年的有限制造商保修。Smart Solar 成立于 2002 年，提供各种太阳能产品。我们为您的庭院和花园设计、制造和定制所有我们自己的产品。享受我们的太阳能、节能、环保照明解决方案、水景和户外装饰。我们相信你会喜欢太阳能生活——这就是为什么我们近 15 年来一直在创造太阳能产品，发展太阳能生活方式。*

*问题:*

*   *从地面到 LED 灯泡的高度是多少？谢谢*
*   *柱子蜡烛用的是什么电池？*
*   *需要多大尺寸的灯泡？*
*   *它们重吗？我们有很多风，他们会在桌子上*

## *样本 2*

*描述:*

> *带治疗孔耐用狗球*

*问题:*

*   *哈巴狗玩它会安全吗？*
*   *有没有吱吱声？*
*   *狗嚼的时候会爆吗*
*   *这件物品的重量是多少？*

## *样本 3*

*描述:*

> *Petco 河岩石浅溪水族馆砾石 Petco 水族馆砾石是理想的淡水和安全的海洋水族馆。这种高质量的砾石具有彩色、耐用的涂层，专门为其永久性和无毒而开发。砾石被加工以去除潜在的有害碎片和物质。它不会影响水的化学性质，也不会伤害任何鱼类、无脊椎动物或植物。可用于水族馆、池塘、水上花园和水族箱。*

*问题:*

*   *我有一条鱼鳍很精致的斗鱼。我想确保我得到的砾石不会刮伤或撕裂它们。这东西有用吗？*
*   *有人在盐水中尝试过吗，如果有，效果如何？*
*   *袋子和塑料/材料的尺寸是多少？*
*   *这种砾石有利于水族馆中藻类的生长吗？*

## *样本 4*

*描述:*

> *进入一个世界的建设乐趣与乐高城市启动设置具有 3 个标志性的车辆。和骑摩托车的警察一起抓强盗！用消防员的快速消防车灭火。然后比赛在救护车上帮助摔倒的阿飞。年轻的建造者需要所有的灵感来探索拯救世界的有趣方式，创造无限的玩耍可能性！包括 5 个带附件的迷你人:强盗、警察、消防员、救助者和一个阿飞。272 件。5 岁以下。+.，“进入一个充满乐趣的积木世界，乐高城市首发套装包括 3 辆标志性的汽车。和骑摩托车的警察一起抓强盗。用消防队员的快速消防车灭火。然后比赛在救护车上帮助摔倒的阿飞。年轻的建造者需要所有的灵感来探索拯救世界的有趣方式，创造无限的玩耍可能性。包括 5 个带附件的迷你人:强盗、警察、消防员、救助者和一个阿飞。*

*问题:*

*   *当所有的零件都在盒子里时，启动装置会在盒子里占据多少空间？*
*   *积木本身有多大？*
*   *乐高迷你人可以被制作成适合乐高家吗？*
*   *这套是什么颜色的？画面不清晰，看起来很暗。*

## *样品 5*

*描述:*

> *这款电视柜优雅时尚，为您的家庭带来全新的面貌。呈深浓咖啡色。两扇滑动门。四个存储区。*

*问题:*

*   *如果我的电视不是 32 英寸的，有什么方法可以调整这个单元的高度或宽度吗？*
*   *这些架子有多高？我有一个高接收器，想确定它是否合适。*
*   *两个储物格的尺寸是多少？谢谢！*
*   *抽屉是可以拆下来的还是固定的？*

## *样本 6*

*描述:*

> *我们说棉花了吗？你打赌我们做到了。男士充电棉长袖 t 恤可能感觉像一件普通的棉 t 恤，但它绝不是普通的。其独特的制作结合了棉的经典舒适性和全天候装备的内置防水性，创造出世界上第一件真正的高性能棉 t 恤。它摸起来很柔软，但比普通棉干得更快，所以你永远不会被压垮。轻盈舒适。可拉伸的机动性。这是你穿过的最有力量的棉质 T 恤衫。毕竟，这是安德玛。*

*问题:*

*   *你能帮我拿个大号的吗？*
*   *这对跑步/短跑有用吗？我的手臂很小，没有太多的灵活性，但做了很多短跑。我穿 vrs2 可以吗*
*   *12 岁男孩的衬衫尺寸是多少？*
*   *尺寸大是什么胸部尺寸英寸？*

## *额外样品*

*描述:*

> *连接圆点！，“连接打点器！Dotters 是我们的 10 只喜气洋洋的达尔马提亚狗，由我们的超软毛绒材料制成，不仅可爱，而且可机洗！*

*问题:*

*   *你能吃这个吗？*

*👀*

*您还可以在其他产品描述上测试您的模型。下面的脚本使用了我在易贝上找到的一个随机描述。*

*以及由此产生的问题:*

*   *地球仪有多大？*
*   *这盏灯是什么颜色的？*
*   *我能为这盏灯购买更多的球吗？*

# *包裹*

*对我来说，T5 模型最吸引人的方面是通过仅仅改变*前缀*来训练它完成全新任务的能力。在本文中，我们已经训练模型通过查看产品描述来生成问题。然而，通过简单地改变*前缀，完全有可能在其他任务上训练相同的模型，并在不同的任务之间切换。**

*这种灵活性为 T5 型号打开了一个全新的可能性和应用世界。我等不及要看接下来会发生什么了！*

*您还可以通过选择`t5-base`模型来显著提高训练速度和 GPU 内存消耗。这可能会导致*相对*较差(但绝不是*较差*)的性能。*