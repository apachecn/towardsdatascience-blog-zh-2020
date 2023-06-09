# 14 种深度和机器学习的使用使 2019 年成为一个新的人工智能时代。

> 原文：<https://towardsdatascience.com/14-deep-learning-uses-that-blasted-me-away-2019-206a5271d98?source=collection_archive---------2----------------------->

## 比格根、塞勒根、斯泰尔根、高根、艺术育种家、德奥迪菲等。:我非常私人的清单(包括奖金)。

![](img/a06b7a07e1150dccea0bd60623829092.png)

![T](img/8ebcce6f7ca915ae9b80abcb158c86ad.png)  T   ime 的流动比我们想象的要快。对摩尔定律有好处。但仍有很多要赶上。在下面，我想列出我在机器学习和深度学习领域在 2019 年发生的伟大事情(*和——抱歉作弊——2018 年也有一些*)。这些大多是基于神经网络的模型，让我印象深刻。

首先，这里是伊恩·古德菲勒的一条推文，完美地展示了深度学习的成就。

即使是关于一个特定的话题:生成性对抗网络的进展，这种进展很好地展示了已经发生的事情，以及将要发生的事情。*一图抵千言。*

我有一种感觉，2019 年比往年更加激烈。以下是一些让我惊喜交集的进展，但顺序并不特别。

> *免责声明 1:* 我是数据科学的新手。因此，如果我错过了以下主题的一些重要讨论，请随时用参考链接来补充本文。
> *免责声明 2:* 这是模型、网络、实现和实验的混合。它们通常是相互关联的。其中一些是另一个的核心。《走向数据科学》的作者已经很好地介绍了其中一些。你在这里看到的是过去 1-2 年里给我留下深刻印象的 DL/ML 故事。
> *免责声明 3:* 正如你会注意到的，我列表中的 AI 进步大部分是指视觉媒介(图像生成和修改)。2019 年也是自然语言处理(OpenAI 等的 GPT-2)的重要里程碑。)，但那是我很快会谈到的另一个大话题)。

## 1.比根

**这是关于什么的:** [比根](https://medium.com/merzazine/biggan-as-a-creative-engine-2d18c61e82b8?source=friends_link&sk=498b6f23dfa37347ac952e9d209710c4)扩大**生成对抗网络**——并允许你生成新的视觉效果，在巨大的视觉数据库上接受训练。系统的核心是两个神经网络:**生成器**和**鉴别器**。**生成器**创建新的视觉效果，并试图说服**鉴别器**这是真实的镜头。**鉴别器**将生成的图像与其“经验”对齐，并作为“*未通过*”发回给**生成器**。这种反复的相互作用一直持续到某种“共识”。

**尝试一下:**使用这个 [BigGAN 笔记本](https://colab.research.google.com/github/tensorflow/hub/blob/master/examples/colab/biggan_generation_with_tf_hub.ipynb)，你可以使用 ***【类别条件采样】*** 并创建例如*山谷*的图像:

![](img/adb87661310902f408facb9178c07b1c.png)

结果是惊人的:

![](img/fe4dfd1efcb70934c94ed3acc09d6ae6.png)

比根生成的图像

在我这篇文章的标题中，还可以看到 BigGAN 生成的时钟。

![](img/a06b7a07e1150dccea0bd60623829092.png)

如你所见，还是*弱 AI* 。网络不知道*时钟*是什么。他们只是知道，这东西怎么可能长得像:“roundish”，“有字有箭”。

我看到**艾**解释世界的尝试和 [**柏拉图**的形式/理念****](https://en.wikipedia.org/wiki/Theory_of_forms) **理论之间明显的相似之处:**

> ***观念或形式是物质事物的超物质本质。物质的东西不是原创的，只是想法/形式的模仿。***

****我的报道本话题(** [**【朋友链接】**](https://medium.com/merzazine/biggan-as-a-creative-engine-2d18c61e82b8?source=friends_link&sk=498b6f23dfa37347ac952e9d209710c4) **):****

**[](https://medium.com/merzazine/biggan-as-a-creative-engine-2d18c61e82b8) [## 作为创意引擎的比根

### 的确，2018 年可以被称为人工智能创造真正创造力的开始。

medium.com](https://medium.com/merzazine/biggan-as-a-creative-engine-2d18c61e82b8)** 

## **2.和比根一起变形。**

****这是怎么回事:**我们可以走得更远，不仅仅是生成带标签的图像。我们可以使用插值函数用 BigGAN 对事物进行[合并和变形。在 BigGAN 的情况下，生成的图像 A 到生成的图像 B 的转换是可能的，无论它们在语义上如何不同。](https://medium.com/merzazine/biggan-and-metamorphosis-of-everything-abc9463125ac?source=friends_link&sk=fde32a2f24a97d0a651c087709fb8a53)**

****试试看:**用同一个[比根笔记本](https://colab.research.google.com/github/tensorflow/hub/blob/master/examples/colab/biggan_generation_with_tf_hub.ipynb)带**插值**功能。**

**![](img/322fe1776475929ae1e14acbeadf7c7b.png)**

**使用这些设置，可以将约克夏梗转化为航天飞机**

**![](img/8efde2011b29615216b6a82adb73b2da.png)**

**这种方法带来了前所未有的可能性，超出了人类的想象。你甚至可以制作更多渐变的画面——并把它们组合成动画片段(更多信息，请查看扎伊德·阿利亚菲的《可乐布笔记本》)**

****我对这个话题的报道:****

**[](https://medium.com/merzazine/biggan-and-metamorphosis-of-everything-abc9463125ac) [## 比根和万物的变形

### 数字变形

medium.com](https://medium.com/merzazine/biggan-and-metamorphosis-of-everything-abc9463125ac)** 

## **3.风格转移**

****这是怎么回事:** [风格转移](https://medium.com/merzazine/ai-creativity-style-transfer-and-you-can-do-it-as-well-970f5b381d96?source=friends_link&sk=258069284f2cca23ff929283c90fba0e)是在给定一组风格定义图像后，对输入的基础图像进行变换的神经技术:将图像 A 的一种风格转移到图像 b。**

****试试看:** [Colab 笔记本](https://colab.research.google.com/github/tensorflow/lucid/blob/master/notebooks/differentiable-parameterizations/style_transfer_2d.ipynb)。也有各种免费的和商业的基于数字图书馆的应用程序将你的图像转换成世界艺术大师的作品。**

**我用各种艺术家的风格转换了我的用户照片，得到了令人信服的结果:**

**![](img/d4b730b0baf5c12e6e7fc54b299919e8.png)**

**凡·高**

**![](img/e19d1514c19549f865af94b06ba8e79e.png)**

**马格里特**

**![](img/6647bb124e6fef37a2319e4191d14946.png)**

**库尔特·施威特斯**

**你可能对风格转移很熟悉，因为[走向数据科学](https://towardsdatascience.com/)提供了一些关于这个主题的很棒的文章(这里只是其中的一部分，[阅读全部](/search?q=Style%20transfer)):**

**[](/neural-style-transfer-and-visualization-of-convolutional-networks-7362f6cf4b9b) [## 卷积网络的神经类型转移和可视化

### 使用迁移学习在 10 分钟内创建专业外观的艺术品。

towardsdatascience.com](/neural-style-transfer-and-visualization-of-convolutional-networks-7362f6cf4b9b) [](/important-resources-if-you-are-working-with-neural-style-transfer-or-deep-photo-style-transfer-719593b3dbf1) [## 重要的资源，如果你正在与神经风格转移或深层照片风格转移

### 神经风格迁移和深度照片风格迁移是深度学习的有趣领域。他们越来越受欢迎…

towardsdatascience.com](/important-resources-if-you-are-working-with-neural-style-transfer-or-deep-photo-style-transfer-719593b3dbf1) [](/style-transfer-styling-images-with-convolutional-neural-networks-7d215b58f461) [## 用卷积神经网络进行图像风格转换

### 创造美丽的图像效果

towardsdatascience.com](/style-transfer-styling-images-with-convolutional-neural-networks-7d215b58f461) 

甚至视频风格传输也是可能的:

[](/real-time-video-neural-style-transfer-9f6f84590832) [## 实时视频神经类型转移

### 在受限的移动环境中优化视频的艺术风格化

towardsdatascience.com](/real-time-video-neural-style-transfer-9f6f84590832) 

艺术家 Gene Cogan 使用了迪斯尼《爱丽丝梦游仙境》(茶会场景)的风格转换，并将 17 件著名艺术品的风格转换到动画中:

我对这个话题的报道([友链](https://medium.com/merzazine/ai-creativity-style-transfer-and-you-can-do-it-as-well-970f5b381d96?source=friends_link&sk=258069284f2cca23ff929283c90fba0e)):

[](https://medium.com/merzazine/ai-creativity-style-transfer-and-you-can-do-it-as-well-970f5b381d96) [## 人工智能和创造力:风格转换(你也可以做到)

### 人工智能的普及

medium.com](https://medium.com/merzazine/ai-creativity-style-transfer-and-you-can-do-it-as-well-970f5b381d96) 

## 4.风格转换的创造性运用:深度的绘画和谐

**这是关于什么的:**一些艺术家和开发者将风格转移的能力用于[创造性的图像处理](https://medium.com/merzazine/ai-creativity-alien-elements-with-style-27ee7e45df92?source=friends_link&sk=4f8bf8dd08b1e76b3fcaa88676add697)。这个想法就像天才一样简单:

```
1\. take a target image B
2\. transfer its style to the element A you want to build into B
3\. combine and enjoy
```

例如，这种方法允许在数字图像拼贴画中艺术地使用风格转移。

**论文:**作者[付军栾等人](https://arxiv.org/abs/1804.03189)。在他们的 [GitHub 资源库](https://github.com/luanfujun/deep-painterly-harmonization)中，你可以找到令人惊叹的样本:

![](img/e152567f81a5f6f83f49ac5691e3fcf3.png)![](img/2d8070d729ff460993bdafc1ac9d823f.png)![](img/f21f04d04ec666a6e08832ce76fb19fb.png)

Gene Cogan 以自拍的方式运用风格转移，在世界艺术史上无处不在:

我对这个话题的报道([朋友链接](https://medium.com/merzazine/ai-creativity-alien-elements-with-style-27ee7e45df92?source=friends_link&sk=4f8bf8dd08b1e76b3fcaa88676add697)):

[](https://medium.com/merzazine/ai-creativity-alien-elements-with-style-27ee7e45df92) [## 人工智能与创造力:风格迥异的元素。

### AI 用艺术玩变色龙游戏

medium.com](https://medium.com/merzazine/ai-creativity-alien-elements-with-style-27ee7e45df92) 

## 5.喜剧化—将视频转换回故事板

**这是关于什么的:**华沙理工大学的一组研究人员，都对人工智能和漫画艺术着迷，他们将自己的热情结合在一起，实现了一个惊人的项目([阅读更多细节](https://medium.com/merzazine/ai-creativity-transform-a-video-into-a-comic-panel-with-ai-549d1e275a5c?source=friends_link&sk=6c054fc670ca6afb3148540d23c87310)):

```
1\. The model analyzes the video, using intelligent video summarization.
2\. The scenes in the video footage are separated by the DL-powered definition of frames with the most aesthetic impact.
3\. Style Transfer for the specific stylization of images is applied.
4\. Selected frames are put into storyboard / comic layout
```

**尝试一下** : [漫画化](https://comixify.ai/?last=month&sortBy=trend) —选择一个视频并将其传输到漫画中。

我是塔尔科夫斯基电影的超级粉丝，所以我急切地想知道，这部《潜行者》的超级剪辑会发生什么:

结果令人震惊:

![](img/c82b795e362d541066373c66ffbbcb80.png)

尤其是如果你知道——并且喜欢——这部电影，你会发现画面的选择是多么令人惊讶。其实是在刻画 Stalker 的核心思想(不剧透影片)。

我用更多的实验报道了这个话题():

[](https://medium.com/merzazine/ai-creativity-transform-a-video-into-a-comic-panel-with-ai-549d1e275a5c) [## 人工智能与创造力:用人工智能将视频转换成漫画

### Comixify 允许将视频转换成类似漫画的剧本

medium.com](https://medium.com/merzazine/ai-creativity-transform-a-video-into-a-comic-panel-with-ai-549d1e275a5c) 

## 6.CycleGAN —无需输入输出对的图像到图像转换。

**这是怎么回事:**BigGAN 在预训练的基础上生成新的图像， **StyleGAN** 在**两幅**图像之间转换样式， [**CycleGAN** 使用单幅图像将其样式或特征转换成不同的东西](https://medium.com/merzazine/ai-creativity-visual-anarchist-realism-of-cyclegan-and-how-ai-cheats-on-developers-ab2b3cb9eb8d?source=friends_link&sk=310d2fba831b87177a99d793d94e6caa)。实际上，这是一个**不成对的图像到图像的翻译，使用循环一致的对抗网络**(这正是这篇论文的名字):

```
1\. The image is being analyzed by GAN (including pattern and object detection)
2\. Pre-trained feature modification is applied.
3\. The same image as in "1." has new visuals achieved by "2."
```

CycleGAN 在不引用其他图像的情况下更改图像的样式和视觉功能。

**论文:**不成对的图像到图像的翻译使用循环一致的对抗网络 **(** [**主页**](https://junyanz.github.io/CycleGAN/)**/**[**GitHub**](https://arxiv.org/abs/1703.10593)/[**论文**](https://arxiv.org/pdf/1703.10593.pdf) **)**

它不仅可以将艺术家预先训练的风格转移到照片上。它可以使用预先训练好的分割特征知识，将绘画修改为照片般逼真的图像:

![](img/a53b6c0f9f8855a8567b886a60a21d87.png)

来源:论文 [**使用循环一致对抗网络的不成对图像到图像翻译**](https://arxiv.org/pdf/1703.10593.pdf)

你甚至可以循环播放录像。在这种情况下，传输“马= >斑马”被应用于运动图像:

![](img/73b745f7473d0e641de7507e2fbda1ff.png)

([来源](https://junyanz.github.io/CycleGAN/)

但并非没有一些系统缺陷…

![](img/d912634b9be2de736929cc20f0aaf023.png)

普京斑马( [Souce](https://junyanz.github.io/CycleGAN/)

[在《走向数据科学](/search?q=CycleGAN)上有很多相关的文章，我不会深究技术细节。对我来说最重要的是，有了 DL，图像的可修改性达到了一个新的高度。适合艺术使用。因为严重的错误使用而变得危险。

**我的报道本话题(** [**【朋友链接】**](https://medium.com/merzazine/ai-creativity-visual-anarchist-realism-of-cyclegan-and-how-ai-cheats-on-developers-ab2b3cb9eb8d?source=friends_link&sk=310d2fba831b87177a99d793d94e6caa) **):**

[](https://medium.com/merzazine/ai-creativity-visual-anarchist-realism-of-cyclegan-and-how-ai-cheats-on-developers-ab2b3cb9eb8d) [## 人工智能与创造力:CycleGAN 的视觉无政府主义现实主义(以及人工智能如何欺骗开发者)

### 你已经尝试过把照片变成梵高的画了。但是你有没有想过反过来…

medium.com](https://medium.com/merzazine/ai-creativity-visual-anarchist-realism-of-cyclegan-and-how-ai-cheats-on-developers-ab2b3cb9eb8d) 

## **7。StyleGAN 接受绘画训练**

**这是怎么回事:_C0D32_** 结束于[**Reddit**](https://www.reddit.com/r/MachineLearning/comments/bagnq6/p_stylegan_trained_on_paintings_512x512/)**在来自 [kaggle](https://www.kaggle.com/c/painter-by-numbers/data) 的 24k 艺术作品数据集上训练 StyleGAN。随着他修改代码，各种风格的新艺术品产生了。它是这样工作的:**

**StyleGAN 生成具有预先训练的艺术风格的原创艺术品。**

****试用一下:** [谷歌 Colab 笔记本](https://colab.research.google.com/drive/1cFKK0CBnev2BF8z9BOHxePk7E-f7TtUi)。**

**有趣的事情:即使你用这个模型得到了无数独特的艺术作品，用一些艺术史的知识你可以假设，哪些风格，艺术运动甚至艺术家正在通过新的图像闪闪发光。**

**![](img/b623a68b949f56f627f8f82ef6e4b200.png)****![](img/7be7d2a1f3229ce9afa74dfb5446d709.png)****![](img/ed5b921f5d228fbfe1349eb0cb208a7a.png)**

****两个生成的图像**对**“Las Meninas”，迭戈·委拉斯开兹****

**或者是对点彩艺术的模仿。**

**![](img/6df66102841422b285e38d5f741ba00c.png)****![](img/3615478c63f8eec02a89de571c689e72.png)**

****生成的图像**对**乔治·修拉(右图)****

****我的报道本话题，**包括更多图片及分析():**

**[](https://medium.com/merzazine/how-to-train-your-artist-cb8f188787b5) [## 如何培养你的艺人？

### 各位，现在是美术测验时间！(奖品包括)

medium.com](https://medium.com/merzazine/how-to-train-your-artist-cb8f188787b5)** 

## **8.pix2pix:图像到图像的翻译。**

****这是怎么回事:** pix2pix 是由 Phillip Isola 等人开发的，最迟在 2017 年开始病毒式传播。由条件敌对网络完成的图像翻译允许将人造涂鸦渲染成照片般逼真的(或以某种方式类似的)图像。请观看 Karoly Zsolnai-Feher 撰写的这篇著名的**两分钟论文**进行总结:**

****论文:**在 [Pix2Pix 网站](https://phillipi.github.io/pix2pix/)上你可以找到这个方法的文档、论文、例子和演示( [GitHub](https://github.com/phillipi/pix2pix) / [论文](https://arxiv.org/abs/1611.07004))**

**试试看: [Christopher Hesse](https://github.com/christopherhesse) 为 pix2pix 提供了[现场 TensorFlow 演示。你可以把你的猫、门面和其他东西的涂鸦“翻译”成“照片般逼真”的图像。](https://affinelayer.com/pixsrv/)**

**![](img/cdf45a90f9aad26b19be62be57717e0c.png)**

**pix2pix 正尽力从我业余涂鸦的一只猫开始。**

**这当然不仅仅是有趣的草图翻译:通过预定义的设置，你可以将航拍照片转换成地图，将白天的照片转换成夜景等等。条件敌对网络检测模式，并将其翻译成所需的主题(你必须定义你的目标图像任务)。在特定的标记图像数据集上训练网络。**

****NVidia** 用 **GauGAN** 将这种方法带到了另一个层面——他们 [AI 游乐场](https://www.nvidia.com/en-us/research/ai-playground/)的实验之一。您可以使用分段来驱动草图:每种颜色都应用于特定的对象或材料。翻译后生成新图像(具有在各种视觉特征之间切换的类似 CycleGAN 的可能性):**

**![](img/b1c399bc08f2706dea23f0d3dbdaec45.png)**

**图片，是我女儿为我们的人工智能驱动的童话书涂鸦的。**

**你可以在这里试试 GauGAN:[https://nvlabs.github.io/SPADE/demo.html](https://nvlabs.github.io/SPADE/demo.html)
关于 GauGAN 的论文:[https://arxiv.org/abs/1903.07291](https://arxiv.org/abs/1903.07291)**

## **9.pix2pix，face2face，DeepFake 和 Ctrl+Shift+Face**

**深度学习世界充满了实验。人们跳出框框思考，这是 DL 特别是 AI 最鼓舞人心的地方。Gene Cogan 用 dynamic pix2pix 进行了实验:在这种情况下，来源不是素描，而是网络摄像头(他的脸)，目标是在特朗普的照片上训练的:**

**这些实验激发了对 face2face 的研究(在本例中: [Dat Tran](https://medium.com/u/4ff6d2f67626?source=post_page-----206a5271d98--------------------------------) ):**

**[](/face2face-a-pix2pix-demo-that-mimics-the-facial-expression-of-the-german-chancellor-b6771d65bf66) [## face 2 face——模仿德国总理面部表情的 Pix2Pix 演示

### 受吉恩·科岗研讨会的启发，我创建了自己的 face2face 演示程序，将我的网络摄像头图像转换成…

towardsdatascience.com](/face2face-a-pix2pix-demo-that-mimics-the-facial-expression-of-the-german-chancellor-b6771d65bf66) 

原理很聪明:

```
1\. face2face model learns facial features / landmarks
2\. It scans webcam input on facial features
3\. It finally translates it into another face
```

后真相时代的另一个前沿到达了——现在我们不仅可以修改图像，还可以修改电影。就像流行的消息应用程序上的 AR 应用程序一样，AI 以完美的方式解释视频片段并修改它。

像 [Ctrl+Shift+Face](https://twitter.com/ctrl_shift_face) 这样的艺术家将这种方法完善到了令人难以置信的程度:他在 face2face 的帮助下切换了邪教电影中演员俏皮的面孔。比如这里:金凯瑞的《闪灵》。并排比较向你展示了即使是精彩的心理战也能翻译得多好。

这种实现在以下方面具有多种可能性:

**电影制作人**可以在试镜前对演员进行实验。他们还可以将电影本地化，以更好地实现不同语言的唇形同步，就像 Synthesia 对大卫·贝克汉姆所做的那样。

现在想象一下使用人工智能驱动的语言翻译和语音合成的国际视频会议的可能性。

艺术家们可以创作出颠覆性的、超现实的类似“成为约翰·马尔科维奇”的杰作。例如，特朗普、普京等人演唱的这首鼓舞人心、欢快而略带荒诞的《想象》的封面:

**Passed away persons** can be revived. The best example is singer **Hibari Misora**, who preformed new song on annual Japanese New Year TV event [*NHK Kōhaku Uta Gassen*](https://en.wikipedia.org/wiki/70th_NHK_K%C5%8Dhaku_Uta_Gassen) (NHK 紅白歌合戦). She did it this week, **even if she died 30 years ago.** The visuals were reconstructed with the help of AI, the voice was simulated by [Vocaloid](https://en.wikipedia.org/wiki/Vocaloid):

但是 DeepFake 的新方法是开放的。还记得 **ZAO** 吗，中国 DeepFake 趣味 app:转移你和名人的脸。现在你是莱昂纳多·迪卡普里奥。将它与在中国推出的生物识别支付结合起来，你就有无限的欺诈可能性:

[](https://edition.cnn.com/2019/09/03/tech/zao-app-deepfake-scli-intl/index.html) [## 新的中国“deepfake”人脸应用在隐私反弹后后退

### 在遭到用户强烈反对后，一款允许人们与名人交换面孔的中国新应用程序正在更新其政策…

edition.cnn.com](https://edition.cnn.com/2019/09/03/tech/zao-app-deepfake-scli-intl/index.html) 

**我的覆盖范围本话题(** [**友链**](https://medium.com/merzazine/ai-in-motion-3-ways-to-visit-uncanny-valley-some-thoughts-about-the-truth-in-post-truth-ac0cf717be77?source=friends_link&sk=b1e650f3418375375c00b9af3632a570) **):**

[](https://medium.com/merzazine/ai-in-motion-3-ways-to-visit-uncanny-valley-some-thoughts-about-the-truth-in-post-truth-ac0cf717be77) [## 运动中的人工智能:参观恐怖谷的三种方式(关于后真相中“真相”的一些想法…

### 这是一个显而易见的事实:我们生活在假新闻的时代。不太明显的事实是:我们一直都是这样。刚才我们…

medium.com](https://medium.com/merzazine/ai-in-motion-3-ways-to-visit-uncanny-valley-some-thoughts-about-the-truth-in-post-truth-ac0cf717be77) 

## 10.3D 本·伯恩斯效应。

**这是关于什么的:**这款机型，由 [**西蒙·尼克劳斯**](http://sniklaus.com/about/welcome) 开发，将单张图像转换成跟踪拍摄。该模型可以识别背景，模拟深度，用内容敏感的修复技术填充缺失的区域，添加新的角度——简而言之:通过一张图像，您可以制作一个空间 3D 视频镜头。在安迪·拜奥的博客中了解更多信息。

**试试看:** [Colab 笔记本](https://colab.research.google.com/drive/1hxx4iSuAOyeI2gCL54vQkpEuBVrIv1hY)作者[马努·罗梅罗](https://mrm8488.github.io/)。

以下是我的一些实验(在 twitter 帖子中):

我写过这个话题( [Friend-Link](/very-spatial-507aa847179d?source=friends_link&sk=dc49882dea2a713647ba0acc4189be95) ):

[](/very-spatial-507aa847179d) [## 很有空间感！

### 在人工智能的帮助下赋予照片新的维度。

towardsdatascience.com](/very-spatial-507aa847179d) 

## 11.艺术育种者:无限的艺术作品生成

**这是关于什么的:** [Joel Simon](https://medium.com/u/be6acff3480f?source=post_page-----206a5271d98--------------------------------) 将 BigGAN 和其他模型实现到用户友好的 web 应用 ArtBreeder 中。你有许多不同的可能性来创建和修改脸，风景，宇宙图像等。Artbreeder 同时在一个生动的社区中成长和发展，在这个社区中，用户和开发者处于持续的对话中。

**试出来:**https://artbreeder.com/

以下是我用 ArtBreeder 做的一些样本:

![](img/8f7bb8006ea9368ad85784df59ede21b.png)![](img/4ce3ce77ec49f184e0e21d8fa356d64c.png)![](img/6c57a3722a0d015c77da87fdf0b9bf87.png)![](img/64fbf30aecbb9b279022e586e2c17dcd.png)

还可以制作简短的过渡视频:

**我在这里写了 art breader(**[**Friend-Link**](/artbreeder-draw-me-an-electric-sheep-841babe80b67?source=friends_link&sk=2fff2b9e102ce632d725e58bfa4c67dd)**):**

[](/artbreeder-draw-me-an-electric-sheep-841babe80b67) [## 艺术育种家:给我画一只电动羊

### 如何以用户友好的方式应用生成式对抗网络？

towardsdatascience.com](/artbreeder-draw-me-an-electric-sheep-841babe80b67) 

## 12.去彩色化—黑白照片的彩色化

**这是怎么回事:** DeOldify 由 [Jason Antic](https://twitter.com/citnaj) 创作并发布。*这个项目的任务是对旧图像和电影胶片进行着色和恢复。(* [*来源*](https://github.com/jantic/DeOldify) *)。* DeOldify 正在使用**生成对抗网络**，在两个神经网络**生成器**和**鉴别器**之间进行迭代交互(类似于[art breader](/artbreeder-draw-me-an-electric-sheep-841babe80b67?source=friends_link&sk=2fff2b9e102ce632d725e58bfa4c67dd))。但与上一个模型不同的是，DeOldify 中的图像不会以它们的形式被修改或生成。甘的力量带来色彩——**发生器**将颜料涂在他训练过的已识别物体上，**鉴别器**尝试批评颜色选择。

**试试看:**你可以在 [GitHub](https://github.com/jantic/DeOldify) 中找到这个型号，也可以在两个笔记本中找到——图片( [Colab 笔记本](https://colab.research.google.com/github/jantic/DeOldify/blob/master/ImageColorizerColab.ipynb))和视频( [Colab 笔记本](https://colab.research.google.com/github/jantic/DeOldify/blob/master/VideoColorizerColab.ipynb))！

这是我的照片:一张我父亲在 1960 年拍摄的黑白照片。看花的颜色检测的多细致。

当然，颜色不会重复原来的调色板。但它让历史照片充满活力，让它们更贴近我们的时代。

我在这里写了这个话题( [Friend-Link](/deoldify-gan-based-image-colorization-d9592704a57d?source=friends_link&sk=925195b692f4922b90814ff8cc537e1b) ):

[](/deoldify-gan-based-image-colorization-d9592704a57d) [## 基于 GAN 的图像彩色化

### 找回丢失的颜色…

towardsdatascience.com](/deoldify-gan-based-image-colorization-d9592704a57d) 

## 13.人工智能驱动的虚拟现实

**这是关于什么的:** AI 驱动的虚拟现实是可能的。实际上，这是 NVidia 一年前发布的[新闻——而且非常有希望:](https://news.developer.nvidia.com/nvidia-invents-ai-interactive-graphics/)

在这里，城市和视觉效果是在谷歌街景上训练的，所以 VR 城市体验是通过深度学习模型重建的:

> 为了进行训练，该团队在 DGX-1 上使用了[NVIDIA Tesla V100 GPU](https://www.nvidia.com/en-us/data-center/tesla-v100/)和[cud nn](https://developer.nvidia.com/cudnn)-加速 PyTorch 深度学习框架，以及来自城市景观和 Apolloscapes 数据集的数千个视频([来源](https://news.developer.nvidia.com/nvidia-invents-ai-interactive-graphics/))。

你可以想象这种方法的所有潜力:“从零开始”的现实城市模拟，对城市发展、交通管理和物流的帮助，重塑视频游戏景观。

## 14.跑道 ML

**这是关于什么的:** Runway 是一个终极应用，使用各种 ML/DL 模型来满足不同的需求。它可以翻译图像 2 文本，在图像后生成文本(使用 GPT-2)，检测照片和视频镜头中的对象。你也可以将不同的模型结合成连锁反应。而且是免费的。

试试看:[https://runwayml.com/](https://runwayml.com/)

![](img/8db25a75f9a80460aa5f6f3fa1beea9d.png)

我很快会写关于 RunwayML 的文章。

## **即将发布:StyleGAN2**

最近，NVidia 发布了 style gan 2——图像质量有所提高( [GitHub](https://github.com/NVlabs/stylegan2) / [论文](http://arxiv.org/abs/1912.04958) / [视频](https://youtu.be/c-NJtV9Jvp0))。

![](img/9e27a063ac76a133aff936fb0218a0cb.png)

StyleGAN 2 预告([来源](https://github.com/NVlabs/stylegan2))

此外，使用图像的新方法也是可能的。例如，StyleGAN 投影:与来自任何可能图像的目标图像对齐。我强烈建议跟随 Jonathan Fly 对每个最新的 DL/ML 开发进行全面的实验:

《road runner 01》也非常有趣:

(人工智能先驱、艺术家和实验者是我将在 2020 年讨论的另一个话题)

## 奖励:尝试它的资源

冬天(希望)终于过去了。技术就在眼前，我们彼此相连，思想交流前所未有地活跃。而 AI 复兴最好的一点就是:DL/ML 的大众化和民主化。如今，不仅 Python 演讲者和 NVidia GPU 所有者可以享受无限的可能性:每个人都可以做到这一点。作家，艺术家，其他非技术领域的人可以使用 Colab/Jupyter 笔记本，用户友好的应用程序，如 Artbreeder 和 RunwayML 等。

这里有一个小列表供你收藏:基于跨平台网络的人工智能实验。现在没有借口声称人工智能将是一门火箭科学(它仍然存在于各种高科技领域，但不是普遍的)。该列表将被更新。

[](https://experiments.withgoogle.com/collection/ai) [## 人工智能实验|谷歌的实验

### 在过去的 6 个月里，谷歌在悉尼的创意实验室与数字作家节团队合作，并且…

experiments.withgoogle.com](https://experiments.withgoogle.com/collection/ai) [](https://www.nvidia.com/en-us/research/ai-playground/) [## 来自 NVIDIA Research 的交互式演示

### 与基于 NVIDIA 研究的现场演示互动，链接到白皮书和 GitHub 源代码

www.nvidia.com](https://www.nvidia.com/en-us/research/ai-playground/) [](https://colab.research.google.com/) [## 谷歌联合实验室

### 编辑描述

colab.research.google.com](https://colab.research.google.com/) [](https://runwayml.com/madewith) [## 面向创作者的机器学习。

### 机器学习的瑞士军刀

runwayml.com](https://runwayml.com/madewith) 

你也可以关注我的人工智能相关关键人物的 Twitter 列表。这个列表还在增长，这是一件好事！

[](https://twitter.com/Merzmensch/lists/ai) [## 推特上的@Merzmensch/AI

twitter.com](https://twitter.com/Merzmensch/lists/ai) 

*这些只是 2019 年令人惊叹的人工智能发展的一部分。你还有 AI 驱动的 WOWs 吗？请随意将它们写在评论中！*****