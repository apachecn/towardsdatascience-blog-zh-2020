# 音乐的数学:玛丽亚·凯莉的数字

> 原文：<https://towardsdatascience.com/the-maths-of-music-mariah-carey-in-numbers-75f0b56eeac9?source=collection_archive---------35----------------------->

## 数据科学能揭开她成功的秘密吗？

无论是一些最具标志性的歌曲，如《永远是我的宝贝》(T0)或《比天还高》(T1)，还是《T2》的必然性，我想要的圣诞节就是你(T3)在冬天的第一个迹象，甚至是催生了一整类迷因，我们都知道并热爱玛丽亚·凯莉。

歌鸟至尊、流行女王、R&B 女王、梅利斯玛女王、圣诞女王，最重要的是羔羊女王，这只是她所拥有的一些头衔，也是理所当然的，因为她在 20 多年的职业生涯中不断创造和打破记录。至少可以说，她以 19 首歌曲荣登 Billboard Hot 100 排行榜榜首，比任何一位独唱歌手都多，也是第一位在 4 个不同的十年中获得冠军的歌手。除了作为一名歌手的成就，她还创作和制作了专辑中几乎所有的歌曲(上述 19 首冠军歌曲中有 18 首是由她创作的)，这使她成为音乐行业有史以来最多产的音乐家之一。

她的歌曲在荒凉的时代闪耀着普遍的光芒，她的声音风格和歌曲创作激发了新一代的创作歌手，她对混音的热情塑造了 R&B 和嘻哈如何与当今主流流行音乐无缝融合——我们让数字为她讲述这个故事。

**高于天之上**

玛丽亚·凯莉的首张单曲*Love*于 1990 年发行，立即将她推上了音乐世界的上层。她是当时最年轻的获得格莱美金像奖四大奖项(唱片、歌曲、专辑和最佳新人奖)提名的人，凭借《爱的愿景》获得最佳新人奖和最佳流行歌手奖。随着业界的认可巩固了她作为音乐家的地位，她第一张专辑中的 3 首单曲也取得了商业上的成功，登上了公告牌百强排行榜。

她的专辑描绘了玛丽亚·凯莉的排行榜历史，不断推出一首又一首热门歌曲，除了 2018 年广受好评的 *Caution* 在她的声音、歌曲创作和合作者的选择方面看到了她最冒险和创新的一面。这张图表最引人注目的事情显然是*我想要的圣诞礼物是你*的成功，这首歌最初于 1994 年发行，但最终在 2019 年高居榜首，并在 2020 年迎来了它的位置。

![](img/d5e1c86b27ac2f794faf242cf56e88ff.png)

作者图片

鉴于她在排行榜上的主导地位，人们不禁要问，玛丽亚·凯莉是一个开拓者，还是仅仅掌握了当时流行音乐生态系统的脉搏。作为代理，我们使用 Spotify 的音频[功能](https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-features/)来区分她的歌曲与其他歌曲的特征，这些歌曲在她获得第一名前后 6 个月也在 Billboard 热门 100 首歌曲中排名前 10。

在下面的图表中，我们绘制了相关时期其他 10 首顶级歌曲相对于 Mariah 排名第 1 的平均声音、舞蹈性、能量、乐器性、活力、语速和效价。

![](img/24603d0480d6d5b0af64ae3995804bc6.png)

作者图片

![](img/67e41ccc4c392d2b7205d47b973be7a4.png)

作者图片

有趣的是，当时仅有的两首处于其他歌曲平均水平之内的玛利亚·凯莉的歌曲是*《爱的愿景》*和*《我们属于彼此》*。这两首歌都处于她职业生涯的关键时刻，其中*Love Vision*是她的首张单曲*We believe Together*巩固了她的复出和继续统治。

与同龄人相比，她早期的大多数歌曲都有较高的声学分数，略低的舞蹈性，能量和效价分数。这与制作早期对她声音的技术掌握的关注不谋而合。此外，由于 Mariah 的许多歌曲都涉及爱情和心碎，较低的配价分数告诉我们，人们在需要的时候会向她寻求安慰，她的音乐的这一方面是她在职业生涯初期受欢迎的原因之一。虽然 Mariah 显然与《解放咪咪》发布后的声音合拍，但这一时期也见证了她更加自信和创造性地利用不同的音色来实现更低调但同样有效的张力和释放。

她来开派对了

尽管玛丽亚·凯莉是有史以来最多产的歌曲作者之一，但她并没有得到她应得的一半的荣誉，她只是在 2020 年入选了歌曲作者名人堂。众所周知，她是一个了不起的顶级作家，为了实现自己的创作愿景，她召集了越来越多的作家和制片人。

![](img/8c3818870a2c7de5df37f6afbab986ea.png)

作者图片

从上面的情节中，我们可以看到她是如何从少数亲密的合作者开始她的职业生涯的，随着她与越来越多样化的人才合作，最终发展到拥有 40 名其他作家。为了《T2》，玛丽亚·凯莉(Mariah Carey)利用了她和本·马古利斯(Ben Margulies)在高中时创作的歌曲，并通过她的唱片公司，寻求沃尔特·阿法纳西夫(Walter Afanasieff)的帮助。由于这张专辑的成功，她的标签给了她更多的创作自由，在她后来的专辑中寻找新的方向。*白日梦*标志着她开始控制将嘻哈和 R & B 融入她的音乐，以《肮脏的混蛋》为特色的*幻想*混音巩固了她作为融合嘻哈、R & B 和流行音乐的革新者的地位。除了在她的音乐中大量融入说唱元素之外，这张专辑还见证了她对另一位长期合作者杰梅因·杜普利的首次介绍。

2005 年，杰梅因·杜普利创作的歌曲《就像这样》和《我们属于一起》的组合拳《解放咪咪》见证了她重回排行榜首位，并开创了一个实验的新时代。与梦想一起，玛丽亚凭借专辑 *E=MC* 中的 *Touch My Body* 获得了她的第 18 个冠军，这导致了更富有成效的会议，当时他共同创作并制作了*不完美天使回忆录*中的大部分歌曲。她的最新专辑《小心 T21》让她和她以前从未合作过的制作人一起出现在录音棚里，比如《史奇雷克斯》、《便便熊》和《血橙》,该专辑受到了评论界的好评，并且这张专辑出现在许多年终最佳专辑中。

![](img/bab7c0ecf55e37c9f74e1d2a15bbbb6e.png)

作者图片

从她的目录后退一步，我们回到公告牌 100 大热门数据集来衡量她对同龄人的影响。1995 年发行的《幻想》混音版对流行音乐产生了重大的文化影响，因为它为后来产生强烈嘻哈影响的唱片设定了蓝图，并为碧昂斯、克里斯蒂娜·阿奎莱拉、蕾哈娜和今天的许多其他艺术家铺平了道路。作为一个简单的衡量标准，我们统计了具有以下特征的歌曲的数量，很明显在 1996 年有一个巨大的爆炸，并且这几年来一直在持续上升。

![](img/e6b31876f2f6fdcc74abd9636afe86b9.png)

作者图片

**词曲作者的艺术**

如果我们要从玛丽亚·凯莉的歌曲中吸取一点东西，那就是她理解爱情的多面性，无论是它采取的情感形式如此强烈，以至于你相信它不仅仅是一个幻想，而是一个甜蜜的命运，还是分手的细微差别可能导致前情人无限期地成为你的一部分，或者被告知干脆滚蛋。

![](img/cbdad2d3372016c0c67bf8d835081614.png)

作者图片

上面的单词 clouds 确实显示了爱是她每张专辑的中心主题，但是她到底指的是什么样的爱呢？我们转向自然语言处理来深入挖掘她的歌词，在一种叫做非负矩阵分解的技术的帮助下，出现了四个有趣的话题。每个话题的前 10 个单词如下:

1.  相信，发现，内在，结束，需要，知道，心，爱，理解，伤害
2.  男孩，玩，女孩，好，想，离开，亚，告诉，玛丽亚，意思是
3.  触摸，天堂，梦想，需要，感觉，想要，爱，漫长，等待，今夜
4.  远离，光，开放，远，走，褪色，跑，夜，雨，晴

第一个话题的歌词提醒我们，为什么我们转向玛丽亚:飙升的权力歌谣，以解除我们最黑暗的时刻。第二个话题清楚地展示了她与嘻哈和 R&B 艺术家合作制作俱乐部准备好的果酱的亲和力(玛丽亚可能是一个天后，但她肯定不会唱自己的名字)。第三个主题是想象爱情的典范会是什么样子，而最后一个主题则带有更多反思和渴望的语气。为简明起见，我将它们重命名为:

1.  力量歌谣
2.  R&B/嘻哈音乐爱好者
3.  爱情和浪漫
4.  自省逃避主义

每项中得分最高的热门曲目是:

![](img/794d9f3cc737fb6788c5c49aa0ebdf46.png)

正如我们之前提到的, *Daydream* 是 Mariah 职业生涯的一个转折点，她开始尝试 R & B/hip-hop，并开始创作更多亲密的歌曲，如【星星下的 。我们也看到这些年来，随着她摆脱了传统“流行”艺人的标签束缚，权力民谣的影响力持续下降。

![](img/b808b67c32c04375ebd5e9c7cf1960f7.png)

作者图片

最后，除了上面的主题，我们还使用 Spotify 的音频功能对玛丽亚凯莉的歌曲进行聚类，以查看是否有任何模式出现。我们使用简单的 k-means 聚类算法和 4 个聚类，因为我们希望音频特征与上述主题大致相符。一些音频功能被删除，如乐器，因为这没有太多的变化；活跃度和响度，让每首歌曲都被视为标准的工作室作品；模式已被删除，因为主/次键的任何预期效果都将被化合价封装。

与简单地应用总括规则来对来自上述歌词分析的歌曲进行分类相反，我们保留原始分数并应用 k-means 聚类，以便考虑其他音频特征，这些音频特征也可能对歌曲的整体欣赏产生影响。下面的图是聚类算法的输出，其中每个聚类都被标记在具有最高平均值的抒情类别之后。

![](img/fc199d2b4f5189e279c46d755b55119b.png)

作者图片

不出所料，她的 R&B 学习曲目在可舞性、能量和效价方面得分最高，但爱情和浪漫歌曲也紧随其后。她的力量民谣在声学上得分最高，因为这些歌曲展示了她通过声音的技术运用来传达情感的能力，而不需要任何可能转移注意力的伴奏。

看看她的排名第一的歌曲是如何被分类的，她在权力歌谣、爱情和放纵中拥有同等数量的歌曲，在自省逃避主义中最少。然而，这一类别中有许多小羊最喜欢的，如《七月四日》、《星空下》、《T2》和《闭上我的眼睛》。玛丽亚·凯莉对情感的盛大展示吸引了大众，而她的忏悔引起了粉丝的共鸣。

![](img/4ead9e853f0fde6a25d708ed026475c8.png)

作者图片

**结论**

玛丽亚·凯莉是一个活着的传奇——我们已经知道她是一个破纪录的，不落俗套的开创性创作歌手，但是量化这些成就只会让她的成功看起来更加不可思议。然后，我们试图用数学来分解她的音乐，以了解是否有潜在的模式，并确定了她的歌曲创作和生产中的一些共同主题。这些都不会让她虔诚的粉丝感到惊讶，因为他们已经下意识地将她的音乐的不同方面内化了，但数学给了我们一种从数字上评估这一点的方法。这是一个总结！