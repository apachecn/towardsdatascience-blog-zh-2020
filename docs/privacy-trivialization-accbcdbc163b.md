# 大数据中的隐私平凡化

> 原文：<https://towardsdatascience.com/privacy-trivialization-accbcdbc163b?source=collection_archive---------61----------------------->

## Zoom 是如何揭示一个更大的技术问题的

![](img/db9c6c930ecd2231a8b171c67c95f491.png)

[连浩曲](https://unsplash.com/@lianhao?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

上周，我写了我们对死亡的恐惧，现在更具体地说是对新冠肺炎的恐惧，是如何被操纵来让我们相信我们的隐私是可以牺牲的和微不足道的。在前几周，我已经讨论了关于[医疗数据](https://medium.com/swlh/death-and-data-science-453ad2bc1371?source=friends_link&sk=83712c7b87b1c5a7b50f0711d6c9f9ac)和 [GDPR](/ethics-and-big-data-8dd52fe6e9b2?source=friends_link&sk=2b623a9077b6532385baeaf9a7c02c3c) 的伦理数据使用。在所有这些文章中，一个共同的主题是，总有人认为维护我们的隐私权将阻碍进步，在医疗数据的情况下，或者从互联网的集体体验中转移，在人们声称 GDPR 正在导致互联网的巴尔干化的情况下。

这些声音所做的是淡化隐私。他们声称，隐私是一个微不足道的问题，至少与其他利害攸关的问题相比是如此，比如医学科学的进步或任何基于数据的研究。通过这种方式来定义隐私，这个想法是，一个人将开始不重视他们的隐私，并且对于放弃隐私更加自满。反过来，这意味着那些建筑技术人员将花更少的时间关注维护用户隐私和保护用户数据，因为没有人会在乎他们是否会这样做。消费者不重视数据安全，因为他们被告知不要重视数据安全，或者期待数据安全是不现实的，这意味着为消费者制造产品的人也没有重视数据安全的动机，即使这些人正是应该关心用户安全的人，即使用户并不关心。

这种情况已经发生多年，其影响是显而易见的。有很多数据泄露，甚至更多的情况是用户没有意识到他们的数据的哪些部分是完全可以被公众访问的(同样，这些新冠肺炎地图制作者[没有分享他们从哪里获得的用户数据](https://www.washingtonpost.com/technology/2020/03/24/social-distancing-maps-cellphone-location/)可能是有原因的)。Zoom 是隐私平凡化及其后果的最新、最显著的例子之一。

![](img/18a5aae3f3215e7bfb5fcf2ac8191c05.png)

不，不是 PBS 的那个(图片来自[r/怀旧](https://www.reddit.com/r/nostalgia/comments/e9m2sa/anyone_watched_zoom_on_pbs/)

在隔离的这个阶段，我认为大多数人至少使用过一次 Zoom 进行某种视频通话。如果人们不是用它来和朋友交谈，他们会用它来上课、举行商务会议，甚至是论文答辩。由于我们都被困在家里，它被使用得更多了，这意味着它突出的隐私问题已经占据了中心舞台。已经发生的一个大现象是 [zoombombing](https://arstechnica.com/information-technology/2020/04/security-tips-every-work-from-homer-needs-to-know-about-zoom-right-now/) ，有人会闯入一个 zoom 会议，做一些事情，包括[大喊种族诽谤](https://thehill.com/homenews/state-watch/490402-virtual-meeting-with-black-university-of-texas-students-cut-off-by-racist-zoom)或暴露自己给会议中的人(在这种情况下[是一群学生)。安全性的缺乏也没有随着 zoombombing 而停止。正如](https://pbs.twimg.com/media/EUmz7feWkAA3Mnh.jpg)[这篇](https://www.npr.org/2020/04/03/826129520/a-must-for-millions-zoom-has-a-dark-side-and-an-fbi-warning) NPR 的文章所指出的:

> 曾在美国国家安全局(National Security Agency)工作的安全研究员帕特里克·沃德尔(Patrick Wardle)说，“你只是想在聊天和视频应用程序中拥有的东西——强大的加密、强大的隐私控制和强大的安全性——似乎完全缺失了。”。
> 
> 他和其他研究人员发现了 Zoom 软件中的缺陷，这些缺陷可能会让黑客通过计算机的网络摄像头或麦克风进行间谍活动。Zoom 表示，它在周三发布了这些问题的修复程序。

Zoom 的问题已经变得如此糟糕，以至于联邦调查局发布了关于 Zoom 的警告，纽约市学校系统的教育工作者被告知不要再使用 Zoom。作为对这些问题的回应，或许更多的是，作为对公众对这些问题的愤怒的回应，Zoom 的首席执行官写了这条[消息](https://blog.zoom.us/wordpress/2020/04/01/a-message-to-our-users/)道歉，并描述了他和他的公司计划采取的措施，以解决用户隐私问题。我认为有一句话很能说明这款应用的发展，以及这款应用的创建文化:

> 首先，一些背景:我们的平台主要是为企业客户——拥有全面 IT 支持的大型机构而构建的。

对我来说，这听起来很像“用户应该关心并确保应用程序的安全性(通过一个专门的 IT 部门)，所以我们创作者不必担心提供它。”这一点，在我看来，在上面链接的 NPR 文章中引用的前美国国家安全局特工帕特里克·沃德尔的话中得到证实:

> 该产品旨在优先考虑隐私和安全之外的事情

当 Zoom 声称为会议提供端到端加密时，我们再次看到了这种琐碎化，而事实上它并没有。正如 Oded Gal 在博客[帖子](https://blog.zoom.us/wordpress/2020/04/01/facts-around-zoom-encryption-for-meetings-webinars/)中所写的:

> 虽然我们从未打算欺骗我们的任何客户，但我们认识到普遍接受的端到端加密定义与我们使用它的方式之间存在差异

因此，虽然有人从未“有意”欺骗，但他们使用了一个常用短语来描述他们实际上并没有的特征，你知道，就像谎言一样。哦，不好意思，一个“差异”

在我上周写的[文章](/death-and-data-science-part-2-2a17c6322c5b?source=friends_link&sk=94ea005960528b1b3a3e3f4ae5a447bc)的结论中，我说:

> 我们对死亡的恐惧已经被操纵来损害我们的隐私权，现在我们的恐惧加剧了，这种操纵只会增加。这就是为什么我们需要对这些私营公司的要求以及他们为保护我们自己的权利而采取或不采取的措施提出更多的批评，因为很明显，如果不被强迫，他们无意保护我们的权利。

我想在这里强调的一点是，公司只有在我们迫使他们这样做时，才会以我们的最佳利益为重。Zoom 现在才开始关注安全性，因为每个人都对此感到非常愤怒。他们以前可以专注于它，但相反，我们现在(谢天谢地)有一个废弃的注意力跟踪器和改变背景的能力。公司不关心人，他们关心客户。事情就是这样。他们是资本主义社会的企业。不管他们说多少次让世界变得更美好，他们所关心的只是他们的底线。因此，激励他们关心你的唯一方法是做一些影响底线的事情。在这种情况下，提出一个关于安全问题的问题显然已经让 Zoom 的业务付出了代价，所以现在他们正在解决这个问题。事实是，Zoom 只是一种更大的技术文化的产物，这种文化轻视隐私，只关心通过酷的闪亮功能(如改变背景)吸引客户。再说一次，因为这是使用资本主义社会创造的产品的一个更大的症状，没有简单的解决办法，所以我要说的是:

永远不要假设一家公司关心你的利益，除非你给他们一个理由。