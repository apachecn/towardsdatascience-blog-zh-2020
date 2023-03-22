# 自然语言处理中的文本情感分析

> 原文：<https://towardsdatascience.com/text-sentiment-analysis-in-nlp-ce6baba6d466?source=collection_archive---------6----------------------->

## 问题、用例和方法:从简单到高级

![](img/6531eb3f8e4d883b3b3c3259d9d3b2ae.png)

[Icons8 团队](https://unsplash.com/@icons8?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/angry?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

人们喜欢表达情感。开心还是不开心。喜欢或者不喜欢。表扬或者抱怨。无论好坏。也就是正的或者负的。

*NLP 中的情感分析*就是从文本中解读这样的情感。是*正*、*负，都有，还是都没有*？如果有情感，*文本中的*所指的对象以及实际的情感短语如*差*、*模糊*、*便宜*、……(不仅仅是*正*或*负*。)这也被称为*基于方面的分析*【1】。

作为一种技术，情感分析既有趣又有用。

首先是有趣的部分。判断一个文本的情感是积极的、消极的、两者都有还是都没有并不容易，至少对计算机算法来说是这样的。线索可能很微妙。撇开总体情绪不谈，更难区分文本中的哪些对象是哪种情绪的主题，尤其是当正面和负面情绪都涉及时。

接下来，到有用的部分。这很好解释。卖东西的人想知道人们对这些东西的感受。它叫做*客户反馈*😊。忽视这一点对企业不利。

还有其他的用途。如*意见挖掘*，即试图弄清楚谁持有(或曾持有)什么意见。根据约翰·史密斯的说法，冠状病毒会在六个月内消失。该任务可以形式化为寻找(*源*、*目标*、*意见*)三元组。在我们的例子中，*来源* = *约翰·史密斯*，*目标* = *冠状病毒*，*意见* = *将在六个月内简单消失*。

**(多)例**

情感分析就是你可能会说的长尾问题。许多不同的场景和微妙之处。这类问题通常最好用例子来描述。

首先，让我们看看一些简单的积极因素。

```
Amazing customer service.
Love it.
Good price.
```

接下来，一些积极和消极的东西更难区分。

```
**Positives**:
   What is not to like about this product.
   Not bad.
   Not an issue.
   Notbuggy.
**Negatives**:
   Not happy.
   Not user-friendly.
   Notgood.
**Definitely not positive**:
   Is it any good?
```

上面列表中的积极因素并不是最强的。也就是说，它们特别适合训练 ML 算法来进行关键区分，因为我们绝对不希望这些正面预测为负面。

```
**Positives**:
  Low price.
**Negatives**:
  Low quality.
```

这些实例对于训练 ML 算法进行关键区分特别有用。

```
**Positives**:
   **Quick** turn-around.
**Negatives**:
   **Quick** to fail.
```

同样的观点也适用于此。

```
**Positives**:
  Inexpensive.
**Negatives**:
  cheap.
```

同样的观点也适用于此。

最后，一些比较难破译的底片。

```
I didn’t get what I was promised.
My package hasn’t arrived yet.
No one in your team has been able to solve my problem.
I was put on hold for an hour!
Why is this so hard to use?
Why does it fail so easily?
```

**用例**

很容易想象很多。下面是一些主要的具体的。

1.  发现对你的产品或服务的负面评价。在博客帖子、电子商务网站或社交媒体上。更广泛地在网络上的任何地方。
2.  对金融工具的总体情绪。比如具体的股票。最近市场对 xyz 股票的看法如何？此外，基于方面的变体。例如*根据金融公司 xyz 的分析师预测，abc 的股票很可能在未来一年上涨 20%*。辨别是谁的意见提供了更多的信息，可用于评估可信度或缺乏可信度。
3.  确定人们对你的产品或服务的哪些部分有所抱怨？特别强烈。优先考虑战术或长期改进。
4.  跟踪特定产品或服务(或其中一系列)的客户情绪随时间的变化。检查情况是否有所好转…
5.  随着时间的推移，追踪政客们不断变化的观点。个人或团体，如政党。新闻媒体喜欢这么做。为了给诸如*这样的唠叨问题火上浇油，你当时是这么说的，但现在却是这样！*。

**计算问题**

到目前为止，我们所讨论的可以归结为两个不同的计算问题。

1.  文本的整体情绪是什么:*正面*，*负面*，*都*，还是*都不*？
2.  哪种情绪适用于文本的哪一部分。这也被称为基于方面的情感分析。

先说第一个问题，我们称之为*情感分类*。

**情感分类问题**

输入是文本。我们寻求的输出是情绪是*积极*、*消极*、*都是*还是*都不是*。在这个问题的一个变体中，我们将不会在这里讨论，我们感兴趣的是额外预测积极和消极情绪的强度。你可以想象为什么。xyz 手机真烂比*消极多了我对 xyz 手机*有点失望。

**基于字典的方法**

最简单的方法是创建两本词典，分别收录带有积极和消极情绪的词汇。就术语而言，我们指的是一个词或一个短语。基于文本中的术语在这两个字典中的命中，文本被分类为肯定的或否定的。如果一个文本不符合任何一个字典，则该文本被分类为中性的。如果一个文本在两个词典中都找到，则该文本被分类为阳性和阴性。

当一个人希望快速获得某种程度上有效的情感分类器，并且没有足够丰富的标注有情感的文本数据集时，这种方法是值得考虑的。简单是一个原因。更重要的原因是，机器学习替代方案有自己的障碍需要克服。当我们讨论这个主题时，我们将详细研究这些。

尽管存在机器学习障碍，但基于字典的方法迟早会遇到质量问题。因此，如果各种情感类别的高精度和高召回率在您的用例中很重要，您应该考虑提前咬紧牙关投资 ML。如果你能找到一个足够丰富的带标签的数据集，或者想出一些创造性的方法来获得一个数据集，你的任务会变得容易得多，可能需要一些额外的轻量级 NLP(在下一节中讨论)。

**监督学习挑战**

第一个挑战是必须有一个大而多样的文本数据集，这些文本都标有它们的情感类别:*正面*、*负面*、*两者都有*，或者都没有。

问题是。把文本想象成一个向量。目前在通常的向量空间模型中，即作为一个单词包。也就是说，即使在某种程度上，这个挑战也适用于单词嵌入。

向量空间是巨大的。词典中的每个单词都有一个维度。

这个空间中的绝大多数词语都不带感情色彩。训练机器学习分类器需要一个庞大的训练集。它要做的大部分事情是学习哪些单词是“讨厌的”单词。也就是说，抛弃在学习过程中收集到的偏见(见下面的例子)。

让我们看一个例子，从这个例子中，分类器可以学习错误地将中性词与积极或消极的情绪联系起来。

```
xyz phone sucks → negative
```

它将学会把单词 *phone* 与情绪 *negative* 联系起来。显然我们不想这样。要忘记这一点，需要训练带有单词 *phone* 的集合实例，这些实例被标记为*not*(即 *neutral* )。

也就是说，将一个庞大而多样的语料库(如维基百科)分解成句子，并给每个句子标上中性的标签可能会缓解这个问题。直觉是这样的。所有的词最初都会学会中性。在标记为*负面*的文本中重复出现的词语，如*吮吸*，最终将从它们的中性标签中“逃离”。

**超越文字袋功能**

从我们在前面部分看到的带标签的例子来看，似乎一个“？”是情绪的预测者。这在直觉上是有意义的。怀疑论者提出问题。不是真正的信徒。

**利用字典作为特征**

如果我们已经有了与积极或消极情绪相关的短语词典(或者发现它们很容易构建)，为什么不把它们用作附加特征呢？它们不必是完整的。只是策划。所以我们可以利用他们的品质。

更详细地说，这就是方法。说*不好*在否定的字典里。我们将为这个条目创建一个布尔特征。如果*不良*出现在文本中，该特性的值为 1，否则为 0。我们还可以将条目(*不好*，*不好*)添加到我们的训练集中。注意，这里我们是把*不好的*当做全文。

**使用词性？**

感情丰富的词往往是形容词。这让人怀疑使用文本中每个单词的词性信息是否有用？作为附加特征或用于修剪特征。

让我们先来看看各种例子中单词的词性。这一分析是使用在线贴标机[2]完成的。

![](img/5b858c63a004e26bd5d9de1fc71a7616.png)

情感承载句中各种词的词性

这引发了什么思考？词性标签*形容词*似乎与情绪极性(积极或消极)显著相关。词尾副词也。*限定词*、*介词*、*代词*似乎预示着中性阶层。

我们如何利用这一点呢？我们可以在他们的词类上设置词袋特征。例如，过滤掉所有词类标签为限定词、介词或代词的单词。这可以被视为停用词移除的一种精心设计的形式。

**特征工程:一些观察结果**

尽管这些观察是一般性的，但它们特别适用于我们的问题(情感分类)。

首先，在我们添加一个新功能之前，我们不需要强有力的证据。仅仅是一个微弱的信念，认为它可能会有所帮助。机器学习算法将计算出该特征的预测性，可能结合其他特征。随着时间的推移，训练集越来越丰富，如果可能的话，ML 将自动学习更有效地使用这个特性。弱的特征可以叠加。

这样做的唯一缺点是，如果我们做得太过火，即添加太多的功能，功能空间爆炸可能会回来困扰我们。稍后会详细介绍。

让我们扩展一下“认为它可能有帮助的微弱信念”。在这里，“帮助”仅仅意味着该特征是某种情感类别的预测。我们不需要知道是哪一个。军情局会解决这个问题的。即哪个特征值预测哪个情感类。相比之下，当建立一个基于规则的系统(其中字典是一个特例)时，人们必须指定特征值的哪些组合预测哪个情感类别。

这种风险的特点是空间爆炸吗？

我们已经接受了使用单词袋特征会扩大我们的特征空间。由于前面讨论过的原因，我们决定在这方面咬紧牙关。问题是，本节提到的额外特性会让事情变得更糟吗？

实际上他们会做得更好。让我们通过这个来推理。首先是*问号*功能。它是布尔值。这里没有爆炸。接下来，基于字典的特性。这些事实上减少了单词向量空间中的噪音，因为它们表现出了情感丰富的单词和短语。最后，词性特征。如所建议的那样使用它们进行过滤(即去除单词)，修剪特征空间。

**Word k 歌功能？**

我们故意把它放在前一节之后，因为如果做得不好，它会有扩大特征空间的更大风险。字*k*-克即使加上 *k* = 2 的空间也是巨大的。也就是说，明智地修剪这个空间可能会增加这些功能的成本效益比。

以下是一些值得考虑的合理想法。在讨论中，我们将自己限制在 k=2，即二元组，尽管它适用于更普遍的情况。

1.  从模型中删除在训练集中没有足够支持的二元模型。(二元模型的支持度是指它在训练集中出现的次数。)
2.  对于额外的修剪，也要考虑词性。

**盘点…**

我们将通过评估我们在这里讨论的内容及其含义来结束这一部分。首先，我们看到 ML 方法可以被赋予各种各样的特性。我们只是简单地将特性混合在一起。只要每个包含都有合理的理由。我们不担心特性之间的相关性。太复杂了，没法分析。让大联盟来解决。目的证明手段是正当的。只要我们有足够丰富的标记数据集，我们就可以对其进行划分，以训练和测试分裂，并可靠地测量我们称为“结束”的质量。

我们确实需要考虑特征空间爆炸。我们已经做了。

现在来说说学习算法。我们有很多选择。朴素贝叶斯。逻辑回归。决策树。随机森林。梯度推进。甚至可能是深度学习。浮出水面的关键点是，这些选择跨越不同的复杂程度。有些可以自动发现特别能预测情绪的多元特征。这里的风险是，他们发现的许多多元特征也是有噪声的。

好了，现在我们有许多功能选择和许多学习算法选择。潜在的非常强大。但也有风险。如前所述，我们可以通过记住特征空间爆炸来降低风险。

尽管最终我们应该专注于构建尽可能丰富的带标签的数据集，即使只是增量式的。从长远来看，这比战术优化功能更有价值，以弥补没有一个很好的训练集。这是这个问题最重要的一个方面。投资这个。

**目标变量**

至此，我们一直认为情感分类是一个四级问题:*正*，*负*，*兼*，*非*。在某些设置中，类*和*都可以忽略。在这样的设置中，我们将*和*都不解释为*空档*。

在大多数用例中，我们只关心前两个。所以*中立*是讨厌的职业。“讨厌”意味着它需要被考虑，即使这不是我们想要的。为什么需要对其进行说明？嗯，我们不希望中性的文本被归类为积极或消极。换句话说，包括中性类(由足够丰富的训练集支持)，提高了肯定和否定的精确度。

这很容易用一个例子来说明。还记得那个例子吗

```
xyz phone sucks → negative
```

我们不会想要这样的推论*手机* → *烂*。意味着每部手机都很烂。通过添加中性类，以及适当丰富的训练集，这种类型的不必要的推理的风险大大降低。

**概率分类**

无论我们最终选择哪种学习算法——朴素贝叶斯、逻辑回归、决策树、随机森林、梯度推进等等——我们都应该考虑利用各种类别的预测概率。例如，如果一个输入的预测概率大约是 50%(正面)，50%(负面)，0% (0)，那么我们可以将文本解释为既有正面情绪也有负面情绪。

**如何高效构建训练集**

好的，很明显 ML 方法是强大的。现在让我们看看“喂养野兽”，即建立一个丰富的训练集。

这里有一个想法，如何快速组装一个大型文本集，可以有效地手动标记。

1.  选择一个合适的非结构化文本来源。例如电子商务网站上的产品评论。
2.  在电子表格中创建两列，一列用于文本*，一列用于标签*。
3.  将每个文档(例如每个产品评论)放在标签为*文本*的列中自己的单元格中。
4.  手动添加标签。

让我们详细说明第 4 步。考虑一下众包。或者至少在团队成员之间分配工作。另外，采用一种约定，即 label 列中的空单元格表示一个特定的标签。一个好的选择是*既不*，也就是*中立*。

您可能会惊讶地发现，使用这个过程可以如此快速地建立一个丰富的训练集。

如果您的产品评论数据集附带了每个评论的星级，您可以使用该评级来自动标记正面和负面实例。这可以加快贴标过程。也就是说，您应该在自动标记后进行手动检查，并纠正那些错误的标签。

这种自动标记背后的假设是它的质量相当好。因此只有一小部分标签需要固定。你必须看着他们所有人。尽管如此，视觉扫描所有标签比编辑单个标签具有更高的吞吐量。

**训练实例粒度**

一般来说，在可能的范围内，输入实例应该更细粒度而不是更粗粒度。客户产品评论通常足够精细。尤其是如果它们已经被标记了评级，我们可以从评级中自动导出情感目标。在这种情况下，将较长的评论分解成单独的句子，并手动给它们加上适当的情感标签可能会工作量过大，而其好处尚不清楚。

接下来，考虑从更长的文档开始。比如产品类的长篇评论文章。例如，*2020 年最佳 10 款手机*或者*2020 年最佳 10 只股票。*

将它们分解成更精细的粒度，比如段落甚至句子，这种情况更为明显。显然，如果我们能够将文本限制在特定情感适用的区域，它可以帮助提高学习算法的准确性。

举一个极端的例子，假设你有一份 20 页的文件，除了一句带有强烈感情色彩的话外，其余都是中性的。把这句话贴上情绪标签，其余文字贴上中性标签，是有道理的。这可能比用一句话给 20 页的文件贴上情绪标签更有效。

**字段中实例的粒度**

如上所述，对于训练集，训练集中的细粒度实例通常比粗粒度实例更好。这种偏好不适用于分类时间，即分类器在现场的使用。我们应该继续前进，预测给我们的任何文本的情绪，无论是一个句子还是一章。

不像在训练期间，预测一个长文档的情绪没有负面影响。只是期望值的问题。如果用户寻找一个比一个段落更长的文档的情感，她真正的意思是她想要整个文本的总体情感。是整体正面，整体负面，两者都有，还是都没有(中性)？

这很好，有时这就是你想要的。一旦你发现了带有某种情感的文档，你就可以一直深入下去，对它们的单个句子或段落运行情感分类器。

有鉴于此，我们应该记住，对来自标记数据集的测试集的评估不会产生分类器在该领域中工作得如何的准确评估。拒不接受的测试集来自带标签的数据集，由于前面讨论的原因，该数据集由粒度实例组成。字段的输入不一定总是那么精确。

**基于方面的情感分析**

在这里，除了解读文本中的各种情绪，我们还试图找出它们中的哪一个适用于什么。

很明显，这种分析非常有用，如下例所示。

```
The camera on my <xyz-brand> phone sucks. Apart from that, I’m happy.
```

你明明想知道什么是被抱怨的，什么是被喜欢的。

通常，我们也关心提取实际的情感短语。考虑下面的例子，它来自对一台新电视的整体评估。

```
Good price. Sharp image. Vivid colors. Static in Audio. Motion lags a bit.
```

理想情况下，我们希望从中提取(方面，情感短语，极性)三元组。

```
Aspect:           price    image   colors   audio   motion
Sentiment-phrase: good     sharp   vivid    static  lags a bit
Polarity:          +         +       +        —        -
```

极性可以帮助获得总体质量分数(例如，这里是 5 分中的 3 分)。也可能有其他用途。

**提取特征和情感短语**

让我们通过[2]处的 postagger 运行这段文本。

![](img/7ecf5f487e2dc58c7c0d1fe71dbaf68e.png)

回想一下，位置标签图例是

![](img/873f8a38b8b5f425257e67e6b9e90f35.png)

位置标签的图例

你注意到了什么？作为第一次尝试，将文本分成句子，在每个句子上运行词性标注器，如果标注序列是

![](img/197a479f0a4ee960d2b71e145837df0e.png)

认为形容词是情感短语，名词是体

将形容词视为情感短语，将名词视为体，效果出奇地好。确切地说，就是。不记得了，因为这个模式太具体了。例如，它没有检测到*动作中的体貌短语有点滞后*。

那么如何才能尝试延伸上一段的思路来尝试提高召回率呢？将此公式化为序列标记问题。类似问题*命名实体识别*的详细序列标记公式见[3]。

文本被标记为单词序列。与这个序列相关联的是一个标签序列，它指示什么是*方面*以及什么是*情感短语*。

下面是我们早先的例子，在这个惯例中被重新表述，用 A 表示体，S 表示情感短语，N 都不表示。我们把这一对一分为二，因为它不适合放在一条水平线上。

```
**words**   Good price. Sharp image. Vivid colors. Static in Audio.
**labels  ** S    A      S     A      S     A        S    N    A **words** Motionlags a bit.
**labels   ** A     S   S  S
```

在[3]中，我们集中于序列标记的隐马尔可夫模型。这里，更自然的是使用条件马尔可夫模型[4]，原因我们将在下面解释。

一、什么是条件马尔可夫模型？回想一下，我们的推理问题是输入一个单词序列，并为它找到最可能的标签序列。对于令牌序列[ *运动*，*滞后*，*位*，*位*，我们期望最佳标签序列为【A，S，S，S】。

条件马尔可夫模型(CMM)将这个推理问题建模为寻找标签序列 *L* 的问题，该标签序列最大化给定令牌序列 *T* 的条件概率 *P* ( *L* | *T* )。马尔可夫模型做了一些假设，使得这个推理问题易于处理。具体来说，*P*(*L*|*T*)被假设为可因式分解的

*P*(*L*|*T*)=*P*(*L*1 |*L*0，*T*1)**P*(*L*2 |*L*1， *T* 2)*…* *P 【T39*

与其解释，不如用我们的例子来说明。我们添加了一个标签 *B* 表示开始。

P( [B，A，S，S，S] | [B，*运动*，*滞后*， *a* ，*位*)= P(A | B，*运动* )*P(S|A，*滞后* )*P(S|S， *a* )*P(S|S，*位*

我们不描述推理算法。对这篇文章来说太复杂了。另外，这不是我们关注的重点。然而，我们将定性地解释上面例子中的个体概率。有了这样的解释，我们可以想象尝试所有可能的标签序列，计算每个的概率，并找到概率最高的一个。

先说 *P* (A|B，*动作*)。这受两个因素及其相互作用的影响。首先，第一个单词是方面的一部分的可能性。二、*动作*是体词的可能性。

第一个因素的可能性远大于 0。我们可以想象许多第一个词是体词的真实例子。比如*摄像头就是低分辨率的*。

这是第二个因素的可能性，我们想详细讨论。考虑 *P* (A| *运动*)，忽略先前状态 b 的影响。CMM 允许我们将这种概率建模为受我们从 A 和*运动*的组合中选择的任何特征的影响。可能重叠。相比之下，HMM 将根据 *P* ( *运动* |A)来工作。它会把*动作*和 A 视为符号，不让我们利用任何我们认为有用的功能。

实际上，我们可以将 P(A| *运动*)视为一个监督学习问题，其中(A，*运动*)是输入，P(A| *运动*)是输出。这种方法的强大之处在于它能够学习复杂的映射*P*(*L*I |*T*I)，在这些映射中，我们可以使用对( *L* i， *T* i)中我们认为合适的任何特征。

我特别想到了两个特点。单词的词性以及单词是否被标记为在可识别的命名实体中。(参见[3]，它涵盖了自然语言处理中的命名实体识别，有许多真实世界的用例及方法。)

我们看到的例子已经暗示了词类特征，在这些例子中，词性标签*名词*似乎是标签*方面*的预测因子，而*形容词*似乎是情感短语的预测因子。命名实体特性的动机是直觉，方面通常是特定类型的对象。例如，零售产品。一个能够识别零售产品和相关产品特征的 NER，对于从充满感情色彩的评论中挑选出这些方面非常有用。

通常我们设置 NER 来识别细粒度的实体。如*产品名称*。不是名词短语。虽然原则上我们可以，但名词短语太多种多样，无法模仿 NER。位置标签的粒度较粗。有鉴于此，我们可以认为将两个特性结合起来的好处如下。NER 给了我们精确性。发布功能有助于回忆。

**延伸阅读**

1.  [https://monkey learn . com/blog/aspect-based-opinion-analysis/](https://monkeylearn.com/blog/aspect-based-sentiment-analysis/)
2.  [https://parts-of-speech.info/](https://parts-of-speech.info/)
3.  [https://towards data science . com/named-entity-recognition-in-NLP-be 09139 fa 7b 8](/named-entity-recognition-in-nlp-be09139fa7b8)
4.  [https://en.wikipedia.org/wiki/Maximum-entropy_Markov_model](https://en.wikipedia.org/wiki/Maximum-entropy_Markov_model)