# 深度造假的技术对策

> 原文：<https://towardsdatascience.com/technical-countermeasures-to-deepfakes-564429a642d3?source=collection_archive---------25----------------------->

![](img/5b66412e5af103dd5e328de3822c269d.png)

从[Adobe Stock](https://stock.adobe.com/)——[蒂尔尼](https://stock.adobe.com/contributor/202206661/tierney?load_type=author&prev_url=detail)获得许可

## 针对恶意 deepfakes 的有效对策分为四大类:立法行动和法规、平台政策和治理、技术干预和媒体素养。

> [这本书现已在亚马逊上架——https://www . Amazon . com/deep fakes-aka-Synthetic-Media-Humanity-ebook/DP/b0b 846 ycnj/](https://www.amazon.com/Deepfakes-aka-Synthetic-Media-Humanity-ebook/dp/B0B846YCNJ/)

GAN 和 Deepfakes 已经不仅仅是研究课题或工程玩具。开始是作为一个创新的研究概念，现在它们可以被用作一种交流武器。Deepfakes 有许多积极的使用案例，但正如每一项创新一样，deepfakes 或人工智能生成的合成媒体可以被用作对个人和机构造成伤害的武器。

> 任何减轻恶意合成媒体负面社会影响的对策的主要目标必须是双重的。第一，减少对恶意 deepfakes 的暴露，第二，最小化它可能造成的损害。

为了捍卫真理和保障言论自由，我们需要一个多利益攸关方和多模式的方法。跨法律法规、平台政策、技术对策和媒体素养方法的协作行动和集体技术必须对恶意 deepfakes 的威胁提供有效和道德的响应。

**在这篇文章中，我将分享一些对付 deepfakes 的技术对策。**

*我将在未来的帖子中分享我对立法、平台政策和媒体素养对策的想法。*

由于 Deepfakes 是使用 AI 创建的，所以每个人的第一个倾向和一个更简单的假设是找到一个技术解决方案，作为一个技术问题的对策。技术对策并不简单，而且随着技术发展继续超过 AI 和 GANs 的能力，技术对策会立即显现出来。

> deepfakes 的技术解决方案分为媒体认证、来源和检测。

# 认证和出处

媒体身份验证和出处工具可以验证内容的真实性，获取其来源，并识别其创建者。许多行业都在努力建立一套标准并协调认证、证明来源和识别权威来源的技术。这将需要一个像开放媒体联盟(AOM)这样的媒体标准机构和更广泛的行业合作伙伴来实现这个目标。

## 媒体认证

身份验证包括使用水印、介质验证标记、监管链记录和其他工具在介质的整个生命周期中验证真实性的解决方案。专家建议，认证是防止假媒体传播的最有效方法。

数字水印技术和媒体验证标记是商业上可获得的，并且被媒体组织和取证从业者广泛采用。这种技术可以在介质的整个生命周期中对其进行认证和跟踪，或者在终端验证证书。鉴于互联网上公开存在大量未经认证的媒体，媒体认证解决方案的覆盖范围总是有限的。尽管如此，媒体身份认证对广大受众还是有价值的，它为新闻广播等重要媒体提供了高度保证。

> 媒体认证工具还可以帮助平台收集信号，以对非权威内容采取行动。该动作可以包括添加标签或者甚至不允许平台上的内容。

## 媒体出处验证

出处解决方案可以提供有关媒体来源的信息，例如媒体过去发布或张贴的主要新闻和其他站点的列表。互联网上的反向图像搜索是检测单个伪造图像或缩略图的最有效和最简单的方法。必应或[谷歌](https://images.google.com/)反向图片搜索就是一个可以用来确定媒体出处的工具的例子。如果 deepfake 是使用互联网上的另一张图片创建的，那么原始版本应该会出现在该搜索中。

由于逐帧搜索视频文件的固有挑战，反向视频搜索功能目前还没有广泛使用。

虽然今天媒体出处解决方案是可用的，但是由于因特网上可用的大量非结构化的、未适当标记的媒体数据，它们是有限的。

**YouTube 内容 ID**

YouTube 通过一个名为[内容 ID](https://support.google.com/youtube/answer/3244015) 的系统，使版权所有者能够快速识别和管理他们的内容。YouTube 将根据内容所有者已经提交的数据库扫描任何上传的视频。只有符合特定标准的版权所有者才能访问 ContentID。获取 ContentID 的要求规定，所有者必须对他们上传到 YouTube 创作者社区的大量原创材料拥有专有权。对于如何使用内容 ID 有明确的指导原则。YouTube 持续监控内容 ID 的使用和争议，以确保创建者遵循这些准则。如果一个视频的内容与版权所有者的作品相匹配，他们可以决定如何处理这些内容，包括删除。对版权内容的错误声明也可能导致与 YouTube 的合作关系终止并撤销 ContentID。

**Adobe 内容真实性倡议**

Adobe 正在创建一个系统，为数字媒体提供出处和捕捉历史，为创作者提供一个工具来声明作者身份，并使消费者能够评估他们所看到的内容是否可信。[内容真实性倡议](https://contentauthenticity.org/) (CAI)创建了内容归属，随着不真实内容的激增，以及强大的编辑工具变得更容易访问，这对于在线透明度、理解和信任至关重要。CAI 旨在提供客观事实，说明内容是如何在没有判断的情况下产生的。Adobe 在最初的实现中侧重于图像，但打算指定一种统一的方法来创建、附加和显示任何媒体类型的属性数据。

**微软乙醚媒体出处(AMP)**

微软 AMP 是一个通过证明出处来确保媒体认证的系统。AMP 允许发布者为媒体实例创建一个或多个签名清单。这些清单存储在高度可伸缩和高性能的数据库中，以便从浏览器和应用程序中快速查找。舱单也可以由区块链这样的监管链分类账进行登记和签名。保管链解决方案的默认实现是使用 [Azure Confidential Consortium 框架](https://docs.microsoft.com/en-us/azure/confidential-computing/overview) (CCF)。CCF 使用硬件和软件来确保所有注册清单的完整性和透明度。AMP with CCF 将使媒体审计变得容易，并使媒体提供商联盟能够管理该服务。媒体真实性可通过浏览器中的可视元素传达给用户，指示 AMP 清单已被成功定位和验证。

**FuJo 出处**

2018 年 11 月，未来媒体与新闻研究所宣布，它将领导一个价值 240 万€的欧盟项目，[出处](https://fujomedia.eu/provenance/)，开发新的工具，以改善社交媒体上分享和接收信息的方式。出处的使命是为数字内容验证开发一个无中介的解决方案，从而给予社交媒体用户更大的控制权。它还将促进和鼓励信任、开放和公平参与价值观的社会共享。出处验证层将使用高级工具进行多媒体分析，如语义提升、图像取证和级联分析，以记录对内容资产的任何修改并识别类似内容。个性化的数字伴侣将满足最终用户的信息需求。出处将使用一系列监管解决方案，如区块链，以安全和可验证的方式记录内容创作者上传和注册的多媒体内容，或由出处社交网络监控器确定注册的多媒体内容。

# 深度伪造检测

Deepfake 检测通常包括利用多模式检测技术来确定目标媒体是否被操纵的解决方案。到目前为止，大多数检测研究和缓解工作都集中在自动 deepfake 检测上。使用 GANs 和其他技术，生成假冒数字内容的方法已经有了很大的改进。它呈现了一场比网络安全更糟糕的猫捉老鼠游戏[ [1](https://www.brookings.edu/research/fighting-deepfakes-when-detection-fails/) ]。

自动检测技术使用新的和创新的机器学习和人工智能技术来辨别媒体是否被操纵。

## 基于伪影的检测

Deepfakes 经常生成人类很难注意到的伪像。研究人员提出了一些使用机器学习和人工智能的技术来识别这些不一致并检测深度假货。

2019 年，奥尔巴尼大学的 Yuezun Li 和 Siwei Lyu 提出了一种解决方案，通过检测面部扭曲伪影来识别 deepfakes [ [2](https://arxiv.org/abs/1811.00656) ]。他们的检测技术基于这样的观察，即当前的 deepfake 算法需要扭曲技术来匹配从源视频帧中提取的原始人脸。扭曲技术将在产生的 deepfake 中留下独特的伪像，这可以被[卷积神经网络](https://en.wikipedia.org/wiki/Convolutional_neural_network)(CNN)充分捕获。

在一篇论文 fake catcher Detection of Synthetic Portrait video using Biological Signals 中，作者断言，隐藏在人像视频中的心跳、脉搏、血容量模式等生物信号可以用作真实性的隐含描述符，因为它们在虚假内容中既没有空间也没有时间保存[ [3](https://arxiv.org/abs/1901.02212) ]。

微软研究发表了一篇论文，观察被改变的脸作为检测的伪像融入到真实图像中。【 [4](https://arxiv.org/abs/1912.13458) 】。该技术将输入人脸图像转换为灰度图像，可以揭示输入图像是否可以分解为两幅图像的混合。该算法通过识别伪造图像的混合边界和真实图像的不混合来进行检测。

## 基于不一致性的检测

几种用于识别媒体中不一致性的技术可以用于 deepfake 检测。音频语音模式和嘴部动作之间的配音不一致、说话者特征和视觉面部特征(例如，声音变化，但是没有说话面部变化)不一致可以帮助获得深度伪造检测的置信度得分。

在论文《发现被操纵视频中的视听不一致(SAVI)》中，作者提出了通过算法来发现 deepfake 检测中检测到的场景类型之间的差异[ [5](https://staff.fnwi.uva.nl/t.e.j.mensink/publications/bolles17cvprwmf.pdf) ]。

普渡大学的视频和图像处理实验室发表了一篇论文，使用时间感知管道自动检测 deepfake 视频[ [6](https://engineering.purdue.edu/~dgueraco/content/deepfake.pdf) ]。该算法利用卷积神经网络( [CNN](https://en.wikipedia.org/wiki/Convolutional_neural_network) )来提取帧级对象特征。这些特征用于训练一个递归神经网络( [RNN](https://en.wikipedia.org/wiki/Recurrent_neural_network) )，该网络通过发现视频是否受到操纵的时间不一致来学习分类。

生成对抗网络(GAN)正在推动图像处理的极限。甘在其生成的图像中留下特定的指纹，就像现实世界中的相机用其光响应不均匀模式的痕迹来标记获取的图像一样。甘指纹和分析数码相机独特的传感器通知(PNRU)可用于寻找视频的来源，并有助于检测[ [8](https://www.researchgate.net/publication/329814168_Detection_of_Deepfake_Video_Manipulation) ]。

## 语义检测

依赖于统计指纹和异常的算法检测技术可能会被有限的额外资源(算法开发、数据或计算)所欺骗。由于现有的媒体一代，deepfakes 严重依赖纯数据驱动的方法；他们容易犯语义错误。DARPA 的 [SemaFor](https://www.darpa.mil/attachments/SemanticForensics-IndustryDay-2019-08-12.pdf) 计划专注于使用语义不一致进行检测。

来自伯克利的 Shruti Agarwal 和哈尼·法里德提出了一种软生物识别方法。这种法医技术对代表个人说话模式的面部表情和动作进行建模，用于深度伪造检测。虽然在视觉上并不明显，但这些相关性经常被制作的假视频的本质所违背。

## 其他检测方法

深度神经网络(DNN)可以从媒体中学习基本特征，以创建通用分类模型。随着越来越多的新的 GANs 方法的出现，需要使用 GANs 创建图像的泛化能力。

在论文中，关于 GAN 图像取证的推广(Xuan et al .，2019)，作者提出使用预处理的一组图像来训练取证 CNN 模型[ [10](https://arxiv.org/abs/1902.11153) ]。通过对真实和伪造的训练图像应用相似的图像级预处理，取证模型被迫学习更多的内在特征来对生成的真实人脸图像进行分类。在某些情况下，DNNs 在压缩媒体上的表现将优于传统的数字取证工具。

在这篇论文中，FakeSpotter 为识别人工智能合成的假脸建立了一个简单而稳健的基线[ [11](https://arxiv.org/abs/1902.11153) ]。作者提出，监控神经元行为可以作为检测假脸的资产，因为逐层神经元激活模式可能会捕捉到对假脸检测器来说很重要的更微妙的特征。

# 结论

由于 deepfakes 是通过对抗性训练(主要是 GANs)创建的，因此 deepfakes 通过试图欺骗算法检测器并迭代结果变得更加可信。随着它们被引入新的检测系统，它们逃避基于人工智能的检测方法的能力将会提高。它提供了一个倾向于老鼠的“猫和老鼠”的过程，特别是在长期。

所有 deepfake 检测对策都集中在短期内解决问题，期望认证和来源技术将是 deepfake 问题领域的长期解决方案。

*喜欢吗？* [*随便给我买本书*](https://www.buymeacoffee.com/ashishjaiman)

# 参考

[【1】](#_ftnref1)[https://www . Brookings . edu/research/fighting-deep fakes-when-detection-fails/](https://www.brookings.edu/research/fighting-deepfakes-when-detection-fails/)

[【2】](#_ftnref2)[https://arxiv.org/abs/1811.00656](https://arxiv.org/abs/1811.00656)

[【3】](#_ftnref3)[https://arxiv.org/abs/1901.02212](https://arxiv.org/abs/1901.02212)

[【4】](#_ftnref4)[https://arxiv.org/abs/1912.13458](https://arxiv.org/abs/1912.13458)

[【5】](#_ftnref5)[https://staff . fnwi . UVA . nl/t . e . j . mensink/publications/bolles 17 cvprwmf . pdf](https://staff.fnwi.uva.nl/t.e.j.mensink/publications/bolles17cvprwmf.pdf)

[【6】](#_ftnref6)[https://engineering . purdue . edu/~ dgueraco/content/deep fake . pdf](https://engineering.purdue.edu/~dgueraco/content/deepfake.pdf)

[https://arxiv.org/abs/1812.11842](https://arxiv.org/abs/1812.11842)

[【8】](#_ftnref8)[https://www . researchgate . net/publication/329814168 _ Detection _ of _ deep fake _ Video _ Manipulation](https://www.researchgate.net/publication/329814168_Detection_of_Deepfake_Video_Manipulation)

[【9】](#_ftnref9)[https://open access . the CVF . com/content _ CVPRW _ 2019/papers/Media % 20 forensics/Agarwal _ Protecting _ World _ Leaders _ Against _ Deep _ Fakes _ CVPRW _ 2019 _ paper . pdf](https://openaccess.thecvf.com/content_CVPRW_2019/papers/Media%20Forensics/Agarwal_Protecting_World_Leaders_Against_Deep_Fakes_CVPRW_2019_paper.pdf)

[【10】【https://arxiv.org/abs/1902.11153】](#_ftnref10)

[【11】](#_ftnref11)[https://arxiv.org/abs/1902.11153](https://arxiv.org/abs/1902.11153)