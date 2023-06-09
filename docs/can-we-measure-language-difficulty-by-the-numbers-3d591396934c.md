# 我们可以用数字来衡量语言难度吗？

> 原文：<https://towardsdatascience.com/can-we-measure-language-difficulty-by-the-numbers-3d591396934c?source=collection_archive---------25----------------------->

## 数据科学可以帮助衡量学习语言的难度。对困难的感知取决于一种新语言与你所熟悉的语言在结构和语义上的接近程度。但是用数字来衡量这些语言差异会产生一些令人惊讶的结果。

![](img/24c6d838e8eea500ae8b7ffb6062be1d.png)

[Artem Beliaikin](https://unsplash.com/@belart84?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/difficult-language?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) 上的照片

毫无疑问，就我们接触来自其他国家和文化的人和内容而言，世界正在“变得越来越小”。即使是减少国际旅行的新冠肺炎疫情，也导致了越来越多的通过互联网的虚拟互动。然而，流利和熟练的跨语言交流的障碍仍然令人生畏。

# **在线翻译与语言学习**

近年来，由于人工智能方法(如神经网络)的引入，机器翻译的质量有了显著提高。人工智能驱动的翻译优化已经迅速渗透到谷歌翻译和微软翻译等消费者应用程序中，这些应用程序简化了机器翻译的使用，提高了跨越语言边界传达意思的能力。

通过软件翻译一门语言和学习一门新语言之间有着巨大的差异。对大多数成年人来说，学习一门新语言很难。但是有些人喜欢语言挑战:对他们来说，最难学的语言可能是最容易征服的。当然，年轻大脑的神经可塑性使得儿童习得新语言相对容易。但是很少有成年人有这么容易。

# **在线语言学习及其挑战**

据《ICEF》报道，在线语言学习已经成为一个每年 5820 亿美元的产业，对数百万人来说，在线语言学习变得更加方便和容易。英语学习占了其中的大部分。虽然英语的流行并不令人惊讶——它是世界上讲得最多的语言，也是商业的主要语言——但熟练的英语使用者正在快速扩展到其他语言。

领先的语言课程提供商 Rosetta Stone 报告称，西班牙语在 2018 年英国人最渴望学习的语言中排名第一，去年有 23.1%的英国学习者学习该语言。其他四种欧洲语言——法语、英语、意大利语和德语——也位列前五。或许令人惊讶的是，拥有超过一百万人口的最受欢迎的母语普通话不在下一层。

毫无疑问，对这种语言难度的认知是其受欢迎程度相对较低的原因之一。普通话对一个不会说中文的人来说是一个很大的困难。然而，超过 11 亿人能流利地说、读、写和理解英语。所以真的很难吗？或者只是对一个说英语的人来说不熟悉？这个问题提出了一个重大的挑战:对困难的感知是否完全是相对的，每个语言学习者在某种程度上有所不同，取决于背景和教育。

当然，数据科学家面临的挑战是如何衡量语言难度。如果我们要吹毛求疵的话，学习一种语言的困难和它固有的使用困难是有区别的。但是为了本文的目的，我们将把重点放在评估一种测量语言难度的方法的任务上，如果我们可以从体操和其他竞技运动的语言中借用一个术语的话。

# **方法 A:询问外交部门**

近十年前，Voxy 发布了一个信息图(如下所示)，来源于外交服务研究所，它将英语母语者的语言难度分为三个简单的类别:简单、中等和困难。比较的基础是不同语言达到“熟练”需要多长时间——就日历周和学习小时而言。该网站确实对其发现进行了限定，指出难度取决于语言的复杂程度、与学习者母语(在这种情况下是英语)的接近程度、每周学习多少小时以及可用的语言资源。从图表中可以看出，每周学习 25 小时的基本假设。

*   **简单**(22-23 周，575-600 课时):罗曼语(西班牙语、葡萄牙语、法语、意大利语和罗马尼亚语)都属于这一类，还有荷兰语、南非荷兰语、挪威语和瑞典语
*   中等(44 周，1110 课时):俄语、波兰语、塞尔维亚语、芬兰语、泰语和越南语、希腊语、希伯来语和印地语。
*   **硬** (88 周，2220 课时):中文、日文、韩文、阿拉伯文

虽然 Voxy 显然希望图表成为教学工具或讨论主题，但不难挑出其分析方法中的弱点。首先，谁来设定“熟练程度”的标准？如何衡量教学质量？如何解释类似因素的第二语言知识？对于一个数据科学家来说，结果会显得令人失望的武断。

![](img/29029bc1fc7b62773899ebf87aaabb10.png)

[Voxy](https://voxy.com/) 在[上拍摄的照片什么是最难学的语言？](https://voxy.com/blog/2011/03/hardest-languages-infographic/)

# **方法 B:对语言学习难度进行评分:多语种者的方法**

Glossika 的语言学家 Michael Campbell 提出了一个更有趣的方法，至少从数据科学的角度来看是这样的。在一篇名为“语言困难”的详细博客文章中，他设计了一个评分系统，用数字回答我们感兴趣的精确问题:

1.  有没有客观的衡量语言难度的方法？
2.  世界上最难的语言是什么？

区别坎贝尔的方法是其相对论性的基于数据的方法。根据不同的语言复杂性标准，语言难度是基于任何两种语言之间的相对相似性。也许与直觉相反，这种方法实际上使客观评估语言学习困难成为可能，因为它是基于可以客观评估的数字标准。他提出的标准包括:

## **词汇习得**

他考虑到这种语言与学习者的语言有多接近。

语言分为语系、分支和次分支。例如，英语属于印欧语系的原始语言，俄语、亚美尼亚语和希腊语都属于印欧语系。相比之下，阿拉伯语、汉语和日语属于不同的语系。在印欧语系中，英语是一种日耳曼-罗曼语，因此更接近德语和法语。就相似性而言，尽管语法不同，英语在任何方面都与德语最接近。同样，葡萄牙语、西班牙语和意大利语将属于同一个分支，使得语言学习更容易。坎贝尔高度重视这一标准，语言学习困难反映在指数更高的数字。同支行支行:0 分。支行不同:1 分。不同分支:10 分。不同家庭:100 分。

## 流利的句法和语法

职业语言学家坎贝尔。分解成一系列因素，例如

*   语言类型
*   主语-动词-宾语顺序
*   形容词-名词顺序
*   所有格(拥有者)——名词顺序
*   限定词-名词顺序
*   关系从句——名词顺序
*   名词变位
*   时态
*   结合
*   广告位置

对于这些标准中的每一项，如果语言之间存在差异，坎贝尔会给 1 分加或减。他的计算结果呈现在一个矩阵中:

![](img/11181296a9d9bccd252a7c309f0b6e6e.png)

[*矩阵*](https://ai.glossika.com/blog/language-difficulty?utm_source=en_in_blog&utm_medium=rank_of_language_difficulty) *源自* [*博客*](https://ai.glossika.com/blog/language-difficulty?utm_source=en_in_blog&utm_medium=rank_of_language_difficulty)

通过比较这个矩阵中的行，他可以对两种语言之间的句法和语法差异进行评分，从而确定学习一种给定语言的难度。说德语的人学习法语的难度分数是 6 分，说日语的人学习西班牙语的难度分数是 13 分，而说汉语的人学习波兰语的难度分数高达 34 分。

## 流利的音韵学

坎贝尔的计算考虑了总音素(书面声音)和音位变体(人们说的声音)的差异，考虑了 12 个发音点以及元音和语调的数量。

![](img/29fbd959197dd48a80ae7eca7b667ba9.png)

[*矩阵*](https://ai.glossika.com/blog/language-difficulty?utm_source=en_in_blog&utm_medium=rank_of_language_difficulty) *源自*[*The Glossika Blog*](https://ai.glossika.com/blog/language-difficulty?utm_source=en_in_blog&utm_medium=rank_of_language_difficulty)

根据这个矩阵，比较行使你能够计算与这些语音标准相关的语言难度。说德语的人学习法语的难度分数是 1 分，说日语的人学习西班牙语的难度分数是 11 分，而说汉语的人学习波兰语的难度分数高达 15 分。

数据科学家会注意到，为各种参数分配的分数是任意的和主观的，但尝试将难度分解为组成因素是有价值的。

例如，对于说英语的人，以下是根据语系的分数分配:

![](img/21a04281ce99a98d80530c41501acfab.png)

[*矩阵*](https://ai.glossika.com/blog/rank-of-language-difficulty) *源自*[*The Glossika Blog*](https://ai.glossika.com/blog/rank-of-language-difficulty)

德语很难调和 0 分(【to】所以 einfach 是 das？)法语或西班牙语 5 分。格鲁吉亚语的词汇习得难度真的是波兰语的 10 倍吗？因此，具体的枚举当然可以微调，尽管这种方法很有趣——虽然有些粗糙。

# **最终清算:乌比卡有什么独特之处？**

他 2016 年的文章最后列出了一些最难的语言。在这方面，他提到了欧洲吉普赛人的罗姆语，这种语言甚至没有文字记录，还有森蒂内尔语，这是太平洋岛屿上的一种语言，想要成为游客的人在到达时会被杀死，还有多种合成语言，如格陵兰语和 Ubykh，至少有 84 个辅音。荣誉奖颁给了贝拉库拉，一种语言只有语言学家用来记录语法的文字。

两年后，坎贝尔写了一篇[的后续文章](https://ai.glossika.com/blog/rank-of-language-difficulty)，应用他的评分系统并将其与 FSI 排名进行对比。

![](img/22286d193a3d2e306b8805b1dde96ea3.png)

[*矩阵*](https://ai.glossika.com/blog/rank-of-language-difficulty) *源自*[*The Glossika Blog*](https://ai.glossika.com/blog/rank-of-language-difficulty)

非语言学家可能会对作者不屑一顾地将泰语、越南语、土耳其语和芬兰语归类为“简单”感到困惑——他赶紧说，除了这些完全陌生的词汇。他承认很惊讶，根据他的排名系统，韩国人在困难中击败了台湾人。但是他认为已经灭绝的切尔克斯语(Ubykh)甚至让韩语望尘莫及。

在这里，你可以学习 Ubykh 数字，听一个徒劳无功的故事，这个故事应该会吸引每一个数据科学家——用任何语言。