# 我是如何闯入数据科学的

> 原文：<https://towardsdatascience.com/how-i-broke-into-data-science-8f782cc200f4?source=collection_archive---------15----------------------->

## **一名软件工程师在 Yelp 和优步的数据科学之旅**

![](img/400bf6882d5a6146059be8375a05d185.png)

由[卢克·切瑟](https://unsplash.com/@lukechesser?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/data?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

我不会讨论成为一名数据科学家所需的具体资格和技能；关于这个主题有很多资源，这取决于你对什么样的工作感兴趣。相反，我将谈谈我进入数据科学(DS)的旅程，以及帮助我进入该领域的一般**思维方式**和**习惯**。最后，不管你的背景如何，我都会回顾一些要点，希望能帮助你打入 DS *。*

本人从未打算过渡到 DS；我也没有这样做的传统背景或教育。幸运的是，我的工程背景教会了我如何批判性地编程和思考，但更重要的是如何学习和坚持。通过阅读论文和做兼职项目，我几乎自学了所有的东西。没有我的导师和他们诚实而有建设性的反馈，我也不可能做到这一点。

在学习了几年软件工程(SE)之后，我作为 SE 实习生加入了 Yelp，从事与 DS 相关的项目。大约一年后，我以 DS 实习生的身份加入了优步，并在那之后不久毕业。这是我如何过渡到 DS 的故事，为什么我决定切换回 SE，以及我在这六年期间学到了什么。

# **开头**

2012 年开始在滑铁卢大学学习[机电一体化](https://en.wikipedia.org/wiki/Mechatronics)工程专业。我总是着迷于如何通过建造直接帮助人们的东西来积极影响他们的生活。我最初认为这只能通过建造实物来实现，比如机器人，但我最终意识到你可以通过软件来实现类似的目标；这也是为什么 2014 年我从机电工程转行做 SE 的原因。

刚开始做 SE 不久，就开始听说机器学习(ML)。我对 ML 的兴趣驱使我在空闲时间开始学习它，尽管只是表面水平。与此同时，我继续学习如何成为一名更好的软件工程师，主要是通过实习。

# **涉足机器学习**

我进入曼梯·里的旅程平安无事地开始了。我没能完成吴恩达臭名昭著的[机器学习](https://www.coursera.org/learn/machine-learning)课程；并且没能完成一个本科计算机视觉研究项目。至少我通过了统计学入门课程，这是我在大学里唯一上过的统计学课程。由于统计学是 ML 和 DS 的基础组成部分，至少有一件事是对的。

在我向 DS 过渡的过程中，这是一段没有收获的时期。我更关注的是获得在美国的 SE 实习机会。2015 年冬天，我终于在加州山景城的一家初创公司找到了实习机会。我用[的 k-NN](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) 和一个分析仪表板构建了一个简单的推荐系统。在这些项目中的工作向我展示了如何利用数据和分析来获得有助于制造优秀产品的见解。这激起了我足够的兴趣，最终我对 DS 和 ML 变得更加认真。

# **钻研数据科学和机器学习**

2015 年秋天，我在 Yelp 找到了一份 SE 实习工作。我加入了流量质量团队，该团队有一个广泛的目标，即识别和防止欺诈和滥用。我很幸运能够从事与 DS 相关的项目，尽管我是作为 SE 实习生被聘用的。

我在实习期间有些挣扎，但我在那里学到了很多东西。了解了[有监督](https://en.wikipedia.org/wiki/Supervised_learning)和[无监督](https://en.wikipedia.org/wiki/Unsupervised_learning) ML，统计[建模](https://en.wikipedia.org/wiki/Statistical_model)，如何进行严谨的探索性分析，以及用于管理大量数据的基础设施。我认识到理解你的数据和分析方法是至关重要的，否则事情可能不会像预期的那样进行。作为一名工程师，通常将方法和数据视为黑盒和抽象就足够了——但这在 ds 中并不总是有效。例如，一些方法及其参数仅适用于特定类型的数据，并且需要某些假设。

当时，我开始阅读 ML 论文，以便在实习期间更有效地使用这些工具，如[随机森林](https://en.wikipedia.org/wiki/Random_forest)、 [k-means](https://en.wikipedia.org/wiki/K-means_clustering) 和[逻辑回归](https://en.wikipedia.org/wiki/Logistic_regression)。我真的不认为这是一次真正的 DS 实习，因为我缺乏基础知识，没有与许多同事合作，并且在实习期间需要很多指导。

我在 Yelp 的经历给了我处理更具挑战性项目的信心。在我们的 Yelp 黑客马拉松上，我和我的团队构建了一个逻辑回归分类器来识别 [SLAPP](https://en.wikipedia.org/wiki/Strategic_lawsuit_against_public_participation) 企业。这让我明白，检索和处理你的数据与程序或算法一样重要——如果不是更重要的话。在另一个黑客马拉松上，我和我的团队为 Messenger(在 [Messenger 的虚拟助手](https://en.wikipedia.org/wiki/M_(virtual_assistant))出现之前)构建了一个[聊天机器人](https://github.com/htn-chio)；它能够回答查询和执行命令。2016 年，我与一名博士后合作了几个月，利用新颖的深度学习方法构建了一个在移动设备上运行的[面部识别系统](https://github.com/chrisjluc/FRS)。对于一个学校项目，我们的团队选择在 Messenger APIs 上构建一个[对话分析工具](https://github.com/chrisjluc/MinervaMetrics)，它可以洞察不同的对话，如[情感](https://en.wikipedia.org/wiki/Sentiment_analysis)，主题和常用词。

在成功完成这些项目并于 2016 年夏天在 Snap 进行了另一次 se 实习后，我决定终于是时候追求一些新的东西了。我以为可以是 ML 和*里的东西而不是* DS。

# **认真考虑数据科学**

2016 年秋天，我考虑的只有 SE 和 ML 实习。在参加了优步 DS 信息会议后，我意识到这可能是一个很好的机会，因为数据科学家们从事的项目很有趣，人们看起来很有才华。我决定申请。这将是我申请的唯一一个副主任职位。

出于几个原因，我仍然没有投入到优步 DS 实习中。我专注于获得 SE 和 ML 实习机会；我没有时间为 DS 面试做准备。我知道 DS 的实习机会非常抢手；只有一个职位，但有数百名申请人(这在我们大学的求职公告板上可以看到)。我与许多有正式 DS 背景的有能力和热情的同行竞争。尽管如此，不被*太投入的一个好处是，在面试过程中，它给了我很多内心的平静；通常我一想到面试就会变得焦虑。*

在申请优步大学后不久，我接受了 DS 挑战。它包括编写 SQL、设计实验和进行探索性分析——所有这些都与优步有关。这使得它新颖有趣；在做这个挑战的时候，我确实学到了一些东西。在提交了我的解决方案后，招聘人员主动安排了一个小时的面试，我觉得一切顺利。几周后，招聘人员告诉我，我是他们实习的第一人选——我既惊讶又欣喜若狂！

我意识到我的经历终于有了回报——从各种 SE 实习、ML 副业项目和 Yelp 的 DS 工作中。我想说这些经历弥补了我传统 DS 背景的不足；他们*是*让我的 DS 背景独一无二。

# 进入数据科学领域

此时，我必须在 SE 或 DS 实习之间做出选择。我将 DS 视为一种增长技能的方式，这种方式使*将*与其他软件工程师区分开来，比如学习更多关于分析、最新研究、ML 和统计学的知识。我把 DS 看作是一个学习比我最初打算的更广阔领域的机会。凭借我在过去几年学到的一切，我突然意识到我已经做好了在优步取得成功的准备。出于这些原因，我决定接受优步 DS 2017 年冬季实习的邀请。

这是一次很棒的实习。我向业内一些最优秀的人学习，并有机会解决有趣且具有挑战性的问题。这和我在 Yelp 上的经历很相似，除了更加强调独立性、演示、交流结果和协作。在优步，我对自己的 DS 能力更有信心。这种信心帮助我在实习结束后从事更雄心勃勃的 DS 项目，比如我们的 [SE 班级简介](https://medium.com/uwaterloo-voice/university-of-waterloo-software-engineering-2018-class-profile-aae48c2075a0)。在这一点上，我认真考虑进入 DS 全职。

# **在数据科学和软件工程之间抉择**

2017 年秋天，我的最后一次实习是在 WhatsApp 的 SE 实习。2018 年，我即将毕业，我要回答的第一个问题是:**我应该进 DS 还是 SE？**

最终我决定和 WhatsApp 的 SE 一起走。SE 满足了我做一些能影响人们的事情的愿望。这种感觉在我在 WhatsApp 实习期间被重新点燃，因为它能够运送即时影响数十亿用户的产品。作为一名数据科学家，我没有这种感觉，因为对最终用户有额外的间接性；但是你确实通过分析和洞察极大地影响了产品。我观察到工程师和数据科学家的比例通常是几比一。SE 仍然是一个需求量很大的领域——有更多的职位，我认为它会提供更多的职业稳定性。

由于我的背景和经验，我觉得我在 SE 比 DS 更有优势。有许多背景非常适合 ds，这使它以自己的方式具有竞争力。我发现，研究最有趣问题的最佳数据科学家通常拥有物理学、经济学或运筹学博士学位。如果我想达到他们的成就，我必须非常努力地工作；我不确定我是否对 DS 有足够的热情去做这件事。我不认为这是放弃 DS，而是*利用*SE 和我的优势。

# **外卖**

我决定进入 SE 已经两年了:我可以自信地说这是一个正确的决定。更重要的是，我不后悔投资 DS 的时间，这仍然是一次很棒的经历，我会毫不犹豫地再做一次。如果我能把我的旅程总结成几个要点，这就是我要说的。

## **学会如何学习**

你应该调整你的[学习风格](https://www.rasmussen.edu/degrees/education/blog/types-of-learning-styles/)以最适合你想要完成的目标。我发现学习 DS 和 ML 的最好方法是阅读[研究论文](https://www.quora.com/What-are-some-must-read-papers-on-machine-learning-for-a-beginner)和参与真正的[项目](https://github.com/chrisjluc)——行动胜于语言。围绕学习建立一致性，比如每天学习。为你想要学习和完成的事情设定具体的目标，比如每周读一篇论文。

## **寻找导师并接受反馈**

向他们寻求诚实和建设性的反馈，尤其是在你想擅长的领域。如果你没有导师，你可以通过[工作](https://www.linkedin.com/)或者通过相互联系找到一个；通常情况下，最好是通过人脉进行介绍，而不是做一封冷冰冰的邮件。确保你开诚布公，设定明确的期望，并与你当前和/或潜在的导师达成一致。

## **当你稳定的时候，冒险更容易**

稳定可能意味着在事业上、经济上、情感上和/或身体上的稳定。我对工程和我在生活中的位置很满意；这给了我在 DS 和 ML 中探索、实验和失败的空间。稳定让你从第一次尝试就匆忙成功的压力中解脱出来。确保你快乐和稳定，如果你有一个安全网，尝试新事物会更容易。

## **拥抱缘分**

我尝试了很多没有太多方向的东西。一旦优步 DS 的机会出现，我意识到我已经做好了抓住机会的准备。保持你的选择开放和耐心，一些伟大的事情可能就在眼前。

## **假装直到你成功**

每个人都必须从某个地方开始。这很有挑战性，因为大多数时候，你被期望知道如何做这份工作，甚至在你被雇佣之前。这可以通过自学足够多的知识来得到这份工作来克服，然后在工作中学习其他一切——就像我在 Yelp 和优步所做的那样。在职学习通常质量更高，因为你可以解决实际问题，获得公司资源，与同事合作并向他们学习。经过足够的时间和毅力，你最终会成为真正的交易者，不再需要伪装。

我希望我的旅程表明，通过一点点努力和意外收获，你可以让自己抓住那些意想不到的机会。祝你一切顺利，我希望这有所帮助！

我很想听听你的意外之旅，你对这篇文章的看法，或者你是否觉得这很有用。请在下面的评论中告诉我你的想法。