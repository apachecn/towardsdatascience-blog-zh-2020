# 为什么我有一个数据科学博客？分享代码的 7 个好处

> 原文：<https://towardsdatascience.com/why-do-i-have-a-data-science-blog-7-benefits-of-sharing-your-code-77f2aee53127?source=collection_archive---------57----------------------->

## 通过写作学习，获得反馈，为开源社区做贡献，建立职业关系，等等

![](img/c97c323812ee113e3ac78c1808327112.png)

帕特里克·福尔拍摄的照片

我的博客[statsandr.com](https://www.statsandr.com/)于 2019 年 12 月上线。虽然和其他人相比，9 个月的写作时间很短，但我已经可以说这是一次不可思议且非常丰富的冒险！

随着 [45 篇文章](https://www.statsandr.com/blog/)的发表(在撰写本文时)以及从[描述性统计](https://www.statsandr.com/blog/descriptive-statistics-in-r/)、[概率](https://www.statsandr.com/blog/the-9-concepts-and-formulas-in-probability-that-every-data-scientist-should-know/)、[推断统计](https://www.statsandr.com/blog/student-s-t-test-in-r-and-by-hand-how-to-compare-two-groups-under-different-scenarios/)到 [R Markdown](https://www.statsandr.com/tags/r-markdown/) 和[数据可视化](https://www.statsandr.com/blog/graphics-in-r-with-ggplot2/)的主题，我已经看到了通过技术博客分享我的代码的许多好处。

在这篇文章中，我强调了其中的 7 个(排名不分先后),希望它能给你们一些人以启发和激励。在本文的最后，我还提到了一些创建自己的博客所需的现代解决方案。

请注意，在这 9 个月里，我没有从我的博客谋生，这不是我的目标，因为我需要把它作为一个优先事项。 [1](https://www.statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/#fn1) 不过，我已经从读者那里得到了足够多的正面反馈，更重要的是，我已经学到了足够多的东西来继续写作。

(对于感兴趣的读者，请看一年后对该博客的[评论——以及对未来计划的一些想法。在这篇评论中，我通过分析页面浏览量、会话、用户和与`{googleAnayticsR}`包的互动来追踪它在 R 中的表现。)](https://www.statsandr.com/blog/track-blog-performance-in-r/)

# #1 通过写作学习

我真的很喜欢学习许多不同领域的新东西。作为我在大学的助教职位的一部分，我通过向来自不同背景的学生教授统计学学到了很多东西(我现在仍在学习)。

在创办这个博客之前，我相信我理解了一个统计学概念，只要我能够*把它教给我的学生。如果我不能用清晰易懂的方式解释它，这意味着我需要更彻底地研究它，因为我实际上并没有完全理解它。*

这通常被称为费曼技术。这种学习方法是基于这样一个事实，为了完全掌握一个主题，你需要能够用简单的术语解释给别人听。

通过这篇博客，我实际上意识到，为了学习和**完全理解新的东西**，一个人必须:

*   能够清楚地传达它，并用简单的术语教授它，
*   但是*也*能够**以精确简洁的方式写下来**

因此，尽管这个博客最初是为了分享我最熟悉的统计学概念(希望它对一些人有用)，但我现在也用它来**通过写作**来学习。我认为这种额外的学习方式实际上和教学一样有效，因为写作可以让我巩固我的理解。

显然，我主要是在学习[统计学](https://www.statsandr.com/tags/statistics/)及其在 [R](https://www.statsandr.com/tags/r/) 中的应用，因为它们是博客的主要话题。然而，我从来没有想到我还会学到这么多关于:

*   网络开发和搜索引擎优化/分析(这是当今越来越重要的技能)
*   项目管理(当你从零开始构建一个东西并希望开发它的时候)
*   写作(作为一个非英语母语的人，我仍然需要提高这项技能)
*   交流结果(任何数据科学家都会告诉你，没有适当交流的结果是无用的，写博客是一个很好的练习)
*   营销/公共关系/品牌管理(想想社交网络和如何处理读者的各种问题)
*   等等。

维护博客教会了我一些基本技能，这些技能通常是在全职工作中传授的。有了博客，你负责从内容到读者询问的一切，就像一个负责一个项目的员工，他必须与最终用户打交道和沟通。

不要误解我，除了例外，我不认为博客可以完全取代个人发展方面的工作，但它肯定有助于学习广泛的重要技能。除了工作之外，阅读书籍和完成数据科学在线课程也是获得技能的其他例子，但博客往往更加多样化和实用，使其更加有益(在我看来)。

我学习的另一种方式是通过**对我写的关于**的主题进行研究。

一个例子是我在 R 中关于[离群点检测的帖子。作为任何](https://www.statsandr.com/blog/outliers-detection-in-r/)[描述性分析](https://www.statsandr.com/blog/descriptive-statistics-in-r/)的一部分，我被用来检查潜在的异常值。因为我对这个话题很熟悉，所以我决定写一写。然而，我发现这篇文章不够完整，所以我做了进一步的研究。事实证明，事实上有几个我不知道的统计测试。我写了这些测试，现在每当我检查潜在的异常值时，我都包括这些新技术。

最后但同样重要的是，我经常收到读者的电子邮件，要求写一个他们选择的主题。有时，我从未听说过他们建议的主题，所以出于好奇，我做了一些研究。即使我还没有写出来，因为我对它还不够熟悉，至少我知道它的存在，我或多或少知道这是关于什么的。

如果学习的唯一好处没有说服你开始你的博客，看看我在下面的章节中经历的其他好处。

# #2 获得反馈

从更有经验的用户那里获得反馈、建议和建设性的批评。注释对纠正我代码中的拼写错误和 bug 有很大的帮助，同时也有助于提高我的 R 技能。

你会惊奇地发现，尽管你花了无数的时间来检查你的代码，总有人会发现你漏掉的一个打字错误。例如，来自世界各地人们的宝贵反馈无疑提高了我日常使用的闪亮应用程序的质量和完整性。

因此，博客可以被看作是一种强大的同行评审方法，可以让你了解一个概念、代码或 R 实践。在做一个玩具例子时犯错误并改正它们也比在工作场所的真实项目中犯错误要好。

此外，一些人将他们的博客文章汇总成文章或书籍，因此博客可以被视为一种方式:

*   朝着长期出版目标取得渐进进展，以及
*   在这个长期目标的每一步接受反馈。

# #3 提醒未来自己的个人笔记

有多少次你在电脑的文件夹中搜索一段代码，最终在谷歌上寻找解决方案，因为你不记得你为哪个项目写了这段代码？它每天都发生在我身上。

有了按[主题](https://www.statsandr.com/tags/)组织的博客帖子，现在我花的时间少多了(挫败感也少了！)去**找我几个月前写的代码片段**。这也允许我保持我的**代码和 R 实践是最新的**，因为我只需要在一个地方编辑它们。

这方面的一个例子是我的一篇关于 R 中的[图形与](https://www.statsandr.com/blog/graphics-in-r-with-ggplot2/) `[{ggplot2}](https://www.statsandr.com/blog/graphics-in-r-with-ggplot2/)`的文章。与 R base 中默认可用的图相比，我更喜欢带有`{ggplot2}`包的图，但是我不能记住所有的层和它们的参数。现在每当我使用这个包纠结于一个情节时，我就简单地重温相应的文章来寻找解决方案。我的许多文章也是如此，每次我忘记代码或它如何工作的细微差别。

你可以将你的代码存储在不同的文件中(例如，R Markdown 文档或 R 脚本，就像我过去经常做的那样)，但是博客文章有这样的优势:

*   代码段突出显示，并且
*   通过向全世界公开它，你不得不保持它的整洁、完整和最新。

# #4 为开源社区做贡献

我学到了很多，而且我每天都在学习 R，这要感谢那些相信开源和免费材料的开发者和科学家们免费提供的资源。

在某种意义上，通过博客免费提供我所有的代码和文章是我的方式:

*   “回报”帮助我学习的人，感谢我现在站在这里的人，以及
*   提前付钱，我将来会从谁那里学到更多。

如果你也相信分享你的知识或专长，拥有一个博客绝对是为社区做贡献的一个好方法。你的贡献不一定要巨大，只要增加了什么，就会有人用。请记住，每个人都是从初学者开始的，即使是世界专家也是其他领域的初学者。而且你会看到，随着你不断地与他人分享你的知识，有些人会欣赏它，因为他们可以从中学习。

就我而言，如果我的小小贡献对一些人更好地理解统计学或学习 R 有用，我的目标就达到了。其他对某个话题充满热情的人可能想把这个话题告诉人们，希望更多的人反过来对这个话题做出贡献。你完全可以自由选择你想为社区做的贡献。

# #5 保持谦逊，保持好奇

自从发布我的博客以来，我发现了许多其他高质量的数据科学博客。我越是看到不同主题的新事物，越是看到人们做出不可思议的事情，我就越意识到我其实知道的不多。这让我想起了**保持谦逊的**。

除此之外，通过与来自不同背景和世界各地的科学家分享我的代码，它允许我**考虑其他观点**并练习开放思维，这反过来又帮助我**保持好奇**。

在我看来，谦虚和好奇是保持学习的良好开端。我不想失去好奇心，否则我可能会失去学习的欲望。

供您参考， [R-bloggers](https://www.r-bloggers.com/) 和 [R Weekly](https://rweekly.org/) 是两家专注于 R 的优秀博客聚合商，而[forward Data Science](https://towardsdatascience.com/)在 Medium 上发布了大量高质量的博客文章，涵盖了许多与数据科学相关的主题。如果你有兴趣发现更多的技术博客，请订阅这些博客。

# #6 学会不追求完美，分清主次

无论你在博客上花了多少时间，请记住，不可能事事都完美。作为一个完美主义者，我不能否认我希望生活中的每件事都能完美运行。

在写我的第一篇文章时，我的完美主义倾向有时如此普遍，以至于这是一个真正的弱点:我可以花几分钟思考两个词之间是否需要逗号(这当然不会有任何影响)。然而，在某些时候，**改进某样东西花费了太多的时间和精力，以至于它的附加值不如你花时间生产新东西所能创造的附加值大。**

随着你每天不断学习，情况会变得更糟。因此，一篇过去看似完美的文章今天可能不再被认为是完美的，所以你想改变或增加你以前所有文章的一个小细节。我不是说你不应该编辑一篇博客文章，它甚至是值得推荐的！尽管如此，我还是建议你，只有当它真的增加了一个重要的价值时，才编辑它。否则，我认为最好是把时间和精力花在创造别的东西上。

有了博客，你将逐渐学会把你的努力和时间(这是有限的资源，随着时间的推移似乎越来越少)用在最有成效的地方。换句话说，你将学会**优先考虑**。

# #7 建立联系和职业关系

通过分享你在某个特定领域的实践，你有时会遇到一些人，他们实际上与你从事相同的课题，或者有着相似的研究兴趣。除其他外，以下情况就是如此:

*   我在[收集的关于冠状病毒](https://www.statsandr.com/blog/top-r-resources-on-covid-19-coronavirus/)的顶级 R 资源。它开始只有 5 个资源，然后当我逐渐添加越来越多的资源时，里斯·莫里森(Rees Morrison)联系了我，他正在收集相同主题的博客帖子，我将他的博客帖子添加到了原始收集中。
*   展示由雷南·泽维尔·科尔特斯开发的 R 包，该包可用于在新冠肺炎检疫隔离期间[下载免费的斯普林格图书](https://www.statsandr.com/blog/a-package-to-download-free-springer-books-during-covid-19-quarantine/)。
*   我写了一篇关于分析新冠肺炎在比利时的传播的文章，这篇文章与另外三名研究人员合作，引发了一场研讨会，并制作了代表比利时新冠肺炎医院住院人数的图表。

这些合作扩展了我的专业网络，让我能够与来自不同大学和不同国家的新研究人员建立联系。如果不首先分享我对某个特定主题的分析，我永远不会认识这些人。

我确信一个博客可以带来无数的合作，让整个旅程更加有趣和丰富。谁知道呢，你职业生涯的下一个篇章可能会由你过去共事过的一个人来塑造。

即使你的博客没有带来任何合作，它仍然是一个自我推销的伟大工具**。做一些研究，练习，写一个主题有助于成为(并被视为)该领域的**专家**。此外，在申请工作或项目时，你的博客将成为你的**作品集**。招聘人员肯定会希望看到你的能力。**

**无论你的博客是一些卓有成效的合作的起源还是你工作的展示，它都是你申请理想工作时的宝贵财富。**

# **如何开始自己的博客？**

**自从开始写博客以来，我的学习曲线加速了，对统计学和 R 有了更深的理解，我的沟通技巧也有了很大的提高。我从未意识到维护博客作为一种学习技巧有多么有用。这带来了额外的好处，能够为自己和他人存储信息和代码，这对于获得反馈和与其他研究人员联系是必不可少的。**

**如果这 7 个好处已经说服了你，那么好消息是，现在创建自己的博客比以往任何时候都更便宜、更容易。**

**对于非技术博客，我推荐 Medium 或 WordPress，因为它易于设置，并且不需要代码。对于**技术博客**，有大量的**静态站点生成器**可供选择，但是我强烈推荐使用 [Hugo](https://gohugo.io/) 和`[{blogdown}](https://bookdown.org/yihui/blogdown/)` [包](https://bookdown.org/yihui/blogdown/)(我是在看完这本书后创建我的博客的)。然后你可以把它放在 [GitHub](https://github.com/) 上，并用 [Netlify](https://www.netlify.com/) 发布。 [3](https://www.statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/#fn3)**

**感谢阅读。我希望这篇文章回答了诸如“你为什么有一个博客？”或者“它的目的是什么？”，谁知道呢，给了你开自己博客的动力。如果你仍然犹豫不决，我真心建议你去做，记住最难的部分是开始。如果你对一个话题有耐心和热情，你只需要开始，其余的就会随之而来。**

**和往常一样，如果您有与本文主题相关的问题或建议，请将其添加为评论，以便其他读者可以从讨论中受益。**

1.  **我有意避免在这篇文章中写经济激励，因为我认为这不是开博客的好动机。首先，许多人不会用他们的博客赚钱，也永远不会。第二，确实也有很多人通过他们的博客赚钱，但对他们中的大多数人来说，这些钱不值得花时间。从我的个人经验来看，博客有时非常耗时，我肯定会在别的地方更容易赚钱。此外，正如你所看到的，我选择不放广告或横幅，因为我认为这会恶化阅读体验(当我在其他博客上看到广告和横幅时，我觉得它们非常讨厌)。这当然是我的观点，这仍然是一个个人选择的问题，也是一个权衡的问题:糟糕的阅读体验和更多的钱，还是更好的阅读体验和更少的钱。我也倾向于让读者选择支持我的项目，而不是给他们强加广告或横幅。 [↩︎](https://www.statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/#fnref1)**
2.  **甚至以英语为母语的人也可以通过博客提高写作技巧。 [↩︎](https://www.statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/#fnref2)**
3.  **注意，我不是程序员，也不是计算机科学家，所以我没有创建网站的广泛知识。肯定有更多的选项可用，但我发现这些选项是给定我的计算机技能和我的目标的最佳选择。 [↩︎](https://www.statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/#fnref3)**

# **相关文章**

*   **[R 闪亮中的抵押贷款计算器](https://www.statsandr.com/blog/mortgage-calculator-r-shiny/)**
*   **[如何发布闪亮的应用程序:以 shinyapps.io 为例](https://www.statsandr.com/blog/how-to-publish-shiny-app-example-with-shinyapps-io/)**
*   **[如何在 GitHub 上上传 R 代码:MacOS 上的 R 脚本示例](https://www.statsandr.com/blog/how-to-upload-r-code-on-github-example-with-an-r-script-on-mac-os/)**
*   **[如何在 R 中一次对多个变量进行 t 检验或方差分析，并以更好的方式传达结果](https://www.statsandr.com/blog/how-to-do-a-t-test-or-anova-for-many-variables-at-once-in-r-and-communicate-the-results-in-a-better-way/)**
*   **如何在 R 中创建简历的时间线？**

***原载于 2020 年 9 月 2 日*[*【https://statsandr.com】*](https://statsandr.com/blog/7-benefits-of-sharing-your-code-in-a-data-science-blog/)*。***