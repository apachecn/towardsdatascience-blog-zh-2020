# 将人工智能应用于商业，去神秘化

> 原文：<https://towardsdatascience.com/applying-ai-in-business-demystified-1d18e3e8652b?source=collection_archive---------39----------------------->

## 如何将你的人工智能项目分解成容易理解的、有经济意义的部分

![](img/2c681805eb23f10b4ec3dd9c1de9cc46.png)

图片来源:[pexels.com](https://www.pexels.com/photo/star-wars-r2-d2-2085831/)

人工智能和数据科学领域一直在经历一个极端的炒作周期。这项技术有着巨大的前景，但所有嘈杂的宣传都使筛选出价值实际在哪里，以及如何利用已经容易获得和访问的现有人工智能组件变得令人生畏或令人生畏。

虽然每个人都在谈论人工智能是商业和人们生活的下一次飞跃，但对于大多数各级商业领袖来说，自然的情感问题如下:

1.  我的组织如何确保我们不会错过一些持续加速的重要事情？
2.  我如何才能拥抱这些新技术，让它们给我的公司带来高价值的影响，同时又不会在这个过程中冒太多金钱或其他宝贵资源和精力的风险？

在这篇文章中，我试图通过分离炒作的情绪来勾勒出一个在人工智能和数据科学中取得成功的真正战略。我将尝试用一个简单易懂的方法来展示一个成功的人工智能或数据科学项目的研发过程。它将基于从许多项目中吸取的艰难教训。

## 1.澄清大术语:人工智能、数据科学、机器学习、大数据……还是什么？

在开始商业案例驱动的研发过程之前，我将试着澄清一下“大术语”,这样我们就都在同一页上了。围绕着他们每个人都有很多议论，但是不要让你自己被这些所吓倒或冲昏头脑。尤其是因为这些对不同的人来说意味着不同的东西，因为大肆宣传和过度使用。

**人工智能**

你可能已经注意到我在上面交替使用了术语 **AI(人工智能)**和**数据科学**。我故意这样做的。当谈到数据科学应用时，人工智能作为一个术语似乎出现在许多炒作中，它是一个注意力抓取器，它有一种冷静，让我们感觉我们生活在科幻世界的边缘。但从技术上来说，“AI”是一个相当模糊的术语，没有明确的界限，是一种让机器看起来和行为(有点)智能的每个学科的总称。

**数据科学**

这个[名词](https://en.wikipedia.org/wiki/Data_science)是家里最小的。它指的是任何涉及数据分析和算法的东西，尤其是它们背后的科学:大数据分析/数据挖掘、机器学习、统计学、数学、信息和计算机科学。

**那是 AI 还是 DS？**

从现在开始，在这篇文章中，我将更多地使用“数据科学”这个术语，以达到“综合”的目的。

某个智者(我不记得具体是谁了)曾经说过，只要有东西被称为 AI，我们就在和“科幻小说”打交道。但一旦它在现实生活中实现，它就变成了一门“计算机科学”，而不再是人工智能了。这可能解释了为什么人工智能似乎总是关于未来，而不是过去或现在，尽管我们在日常生活中已经使用的许多东西在十年前肯定会被认为是科幻小说中的东西。

可能出于同样的原因，我个人在和朋友开玩笑、谈论人工智能奇点或处于“推销员模式”时会使用人工智能这个术语😉试图引起注意。当我在家做黑客、做实验、学习、参加 [Kaggle](https://www.kaggle.com/) 比赛，或者与团队讨论项目和策略时，我会谈论并查找数据科学。

这也适用于命名团队——最有可能的是，你会有一个**数据科学团队**为你的任何人工智能或数据科学商业机会工作。这样的团队将由**数据科学家**(能够处理数据探索、研究和商业机会验证的科学方面的数据科学博士)和**数据工程师**组成，他们知道如何处理大数据框架，如何将研究成果实施到运营环境中，等等。

**机器学习**

机器学习听起来几乎像人工智能，但在数据科学社区中，它是一个更具体的技术术语，指的是人工智能中专注于机器智能的**学习**部分的特定组件或过程。有许多机器学习算法，如(深度)神经网络、决策树、贝叶斯等，以及这些算法可以应用的应用领域或数据。数据可以是任何东西，从交易数据到图像、视频、音频和振动模式分析，甚至是音乐、自然语言处理(NLP)、用于预测性维护用例的感官诊断数据等。本质上，这些算法都是基于某种统计程序。

**大数据**

该术语实质上是指任何存在的数据量太大，以至于无法通过单台计算机中的“传统”数据处理工具进行处理或分析，这反过来需要特定的方法来解决与处理大量数据相关的问题。例如，重负载问题可能来自所需数据存储的大小(要求分布式存储和检索系统)，或者来自近乎实时地处理信息的需要(要求机器学习方法)，等等。

**其他条款**

显然，在研究这个主题时，您可能会遇到很多更密切相关的术语，包括数据挖掘、大数据分析、商业智能(BI)等，但为了简洁起见，我将把自己限制在今天装饰炒作场景的几个最大胆的术语上。

**2。制定数据科学战略——先决条件理解**

建立数据科学战略始于理解其基本前景、适用性和局限性。

**2.1 商业数据科学的基本前景**

就商业而言，数据科学的用处有两个主要原因。它帮助您寻找新的收入来源，并帮助您避免因效率低下、欺诈或人为错误而损失金钱，它通过查看您的数据并对其应用数据分析和机器学习技巧来实现这一点。

**举个例子。**早在 2005 年，我就曾在 Skype 早期担任后端开发人员。当 Skype 推出其第一项高级功能 SkypeOut calls 并大幅提升其收入时，它也开始因信用卡欺诈退款请求和罚款而损失约 10%的收入，并受到支付提供商的威胁，如果我们不找到减少欺诈的方法，就将被关闭。最初，我们开发了不同种类的硬编码欺诈检查，以阻止最明显的欺诈模式，但这是一场与风车的斗争——欺诈者擅长调整他们的行为，以至于在程序部署后几天，人工分析和硬编码的欺诈模式检查就变得无关紧要了。在某个时候，我开始开发一个基于朴素贝叶斯的机器学习管道，并最终成功地实时检测到 90%的欺诈交易，假阳性率保持在 0.1%以下。此外，它能够近乎实时地学习新的欺诈模式，即使欺诈形式不断演变，也能保持效率。

**2.2 AI 在商业中的适用性**

数据科学的好处在于，它的主要实现策略形式与您应用它们的领域无关。无论哪里有数据堆积或流动，都很有可能隐藏着巨大的积极影响的未开发机会。

顶尖的数据科学团队通常能够以相同的方式处理任何类型的数据，无论是处理交易、图像、视频、音频、振动、自然语言文本处理等。基于这些数据的具有重大商业价值的应用可以包括信用评分、欺诈检测、客户终身价值预测、图像识别、预测性维护、自然语言处理(NLP)聊天机器人、入侵检测(网络安全)、转换和流失预测等等。

**2.3 AI 在商业中的局限性**

到目前为止，它看起来就像一个普通的软件项目，对吗？只是加入了一些人工智能带来的酷感，就这样？**错了！**

这就是数据科学项目与普通软件项目的显著区别，如果你不注意它的局限性，它会变得非常混乱，几乎肯定是你浪费时间和金钱的项目；另一方面，如果你充分考虑到这种差异，它会对你的业务战略做出非常可控的成功贡献。

数据科学项目和普通软件项目之间的显著区别在于它的主要局限性:

**1。概率的本质。**在商业用例的背景下，机器学习算法通过概率而不是确定来工作。当考虑到它的答案时，你总是会有准确性的问题。请记住**上面的欺诈检测示例** —总会有一定数量的“假阴性”和“假阳性”结果，但是检测到 90%的欺诈(这意味着避免了 9%的收入损失)仍然会使公司处于一个明显更好的境地，消除了支付提供商停止服务的风险，避免了重大损失，并且为了更大的利益，使欺诈者的日子更难过—即使代价是损失不到 0.1%的合法交易。

如果你的商业案例对“错误”答案零容忍，你就不能应用这些方法。然而，如果您的业务案例能够“足够好”地准确工作，那么它就变成了实现“足够好”结果的问题。

**例如，在自动驾驶汽车的一个非常极端的情况下，**当你有级联的人工智能组件在发挥作用时，人们可能会问，在那里出现错误是怎么回事！？答案是，在系统的传感实时数据分析中可能会有“错误”(用机器学习的术语来说)，但结合某些鲁棒性原则的应用，这些错误可以缩小到单个组件，这些原则要求永远不要依赖单个数据源或传感器，这样这些错误就不会对任何人的财产或健康造成危险。

**2。做能力的问题。**数据科学的概率性质引出了另一个重要的问题:即使你的业务案例能够在行动过程中接受一些“错误”的答案，那么“足够好”的准确性水平到底能不能达到？你可以开发完整的框架软件，将你的机器学习算法无缝集成到你的操作环境中，它可以扩展等，但如果 ML 算法真的无法准确地做出对你的商业案例有意义的决策，那么围绕它的所有产品开发都将是浪费，甚至是适得其反。

这是数据科学项目的一个不变的现实——必要的准确性并不总是可以达到的(至少第一次尝试是不行的)。

## 3.该过程

列出了上面的注意事项后，接下来的事情实际上非常简单明了。

![](img/0bcb60b33dfa54733d4b72694a96af00.png)

图片来源:【mooncascade.com 

**第一步:提出“问题”**

任何数据科学项目的核心都是你希望你的系统回答的既定问题。当你考虑你的第一个(或下一个)人工智能应用时，确保你确切地知道你将回答什么问题，并确定它与你的**业务影响有明确的联系。**

问题示例:

1.  **问题:**我们能否预测保险申请中的欺诈行为？我们能否实时适应欺诈模式的变化？**影响:**避免因诈骗而亏钱。
2.  **问题:**能否检测危险品(放射性物质、武器部件等。)根据对相关文件、物流信息以及海港和机场货物的 x 光扫描结果的分析而被走私？**影响:**更安全的居住社区。
3.  **问题:**我们能否在系统实际崩溃之前预测机械故障？(这被称为预测性维护问题，例如，可以通过收听连接到机器主体的音频传感器并分析振动模式的变化来回答。)**影响:**避免机械故障和收入损失，甚至可能由此产生的损坏成本。

**第二步:确定“足够好”的准确度对你来说意味着什么**

一旦你确定了项目的问题，但在开始投入资金、时间和其他资源进行繁重的开发工作之前，重要的是要确定你必须如何回答这个问题，才能让你的商业案例有意义。换句话说，您需要为您的系统量化某种在业务案例中有意义的关键性能指标(KPI)目标。

**举个例子。**在欺诈检测的情况下，当触发欺诈检测时，您希望在实施自动交易阻止的同时确保可接受的误报率。**KPI 目标**可以是，例如，对于每 10%的检测到的实际欺诈，0.01%的误报是可以接受的，这样自动交易阻止才有意义。这在实践中为数据科学家提供了强有力的指导，他们可能会很容易地隔离相当大一部分欺诈，然后，对于确定性不再那么好的另一部分，可以应用一些其他措施(而不是简单的自动阻止)。

**第三步:数据探索、研究和影响验证**

直到流程的这一步，除了识别问题和建立有意义的 KPI 目标的一些基本工作之外，您几乎没有花费任何资源。

现在关键的问题是:这真的能做到吗？您的问题能否以超过最低 KPI 阈值的质量水平得到回答？**这是业务影响验证步骤。**它的目的是识别所有相关的数据源，探索、操作、重组和整理数据，建立机器学习模型等。这将会产生影响。这一步的结果包括**培训、测试和验证数据集，**允许您在实际的软件产品开发开始之前，就可以明确地确认产品的可行性。

通过使用术语“可论证地”，我指的是根据科学标准和质量的过程的可重复性——记住，我们正在与工作中的数据科学家(通常是博士级)打交道，重点是“科学家”这个词。科学方法的关键品质之一是可重复性。这意味着，从技术上来说，您的研究和数据探索的结果包括所有确切的步骤、脚本和数据字典，这些数据字典准确地显示了数据是如何获得、转换并划分为训练、测试和验证数据集、机器学习模型和演示说明的。

可以想象，这是需要投入一些初始资源的第一步，因为研究和数据探索是需要由有专门技能的人来完成的工作。尽管如此，与接下来的产品开发项目相比，这通常是相当精简和吝啬的。这里的想法是，只要项目的可行性仍然悬而未决，就要避免投资于产品开发。只有在研究证实了影响后，投资产品开发才有意义。你需要愿意冒险投资这些验证周期，对你的基金应用合理的资金管理方法和每个项目的止损决策策略。但是，除非你喜欢混乱的公司过山车，否则你不应该在数据推测中验证你的业务影响之前，冒险投资于产品开发。

**当研究未能验证**最初冲刺阶段的推测影响时，可能有几个原因:

1.  你正在处理的数据可能太肤浅，或者缺乏容易发现和有意义的应用信号。在这种情况下，你还没有开始在产品开发上花费资源，这很好，你可以开始寻找其他想法来产生影响。
2.  也可能是相关信号在您的数据中很明显，但它拒绝越过允许您验证业务案例的预期 KPI 目标阈值。在这种情况下，您可以与您的数据科学团队讨论构建更多您尚不具备的数据功能的可能性。这可能意味着需要几个月的时间让您现有的产品，即生成相关数据的产品，收集和存储额外需要的数据，之后您可以再次尝试您的研究，看看有问题的 KPI 目标是否可以实现。

**第四步:产品开发**

一旦您在步骤 3 中的研究成功，围绕结果开发适当的**数据产品**，使其无缝集成到您的运营环境中，扩展并使您能够创造真正的影响。

这个阶段看起来更像是常规的软件产品开发。在这里，你可以应用同样的原则，从**构思**和**设计冲刺**(如果涉及 UI 交互)开始，来验证目标用户是否会抓住新产品并接受这个想法。然后，您将开发您的第一个 **MVP** (最小可行产品)来进一步验证您是否在正确的轨道上，但这一次有来自现场的确凿证据，并迭代地继续开发您的产品并增加对您的业务案例的影响。

只要产品保持相关性，你通常总会有需要改进的地方。除了产品的常规软件开发部分之外，您还将继续监控产品的数据科学部分的性能，偶尔会重新审视研究周期，以排查数据源中的变化或加强/优化结果的影响。

## 4.大局

希望上面的流程布局能给你一些启发，告诉你如何开始将数据科学引入你的公司。在现实生活中，正如成功的产品一样，将会有更多连续的嵌套开发周期一个接一个地进行，并且您将应用于实现它们的原则将会随着您对该主题的学习和熟悉而发展。然而，一个蓬勃发展的数据科学项目的本质仍然是一样的:成功的数据科学产品是研究优先项目的产品，成功的数据科学产品管道战略是基于这样的项目。

成功的主要驱动力基本上是在整个过程中保持这两个原则，在任何步骤中都不要忘记:

1.  确保你总是知道你想要的影响会是什么。确保你所做的事情确实意义重大，具有积极的影响。这是任何事物在商业环境中生存的基本规则——不仅仅是数据科学。
2.  **尽早并尽可能经常地验证关键假设。**在处理数据科学项目时，验证回答既定问题所需的准确性在经济意义上的影响级别上是可以实现的。

## 5.从这里去哪里？

如果你是一个成功的企业家，你可能已经知道，大多数大事都是从无数的实验中开始的。在数据科学领域也是如此。以下是识别数据科学机会的一些提示。

无论你在哪个领域工作，保持头脑风暴的习惯来寻找新的、令人兴奋的想法通常是一个好主意。因此，定期花一些时间思考你的业务以及你投入的工作，记住好的产品创意可以从最痛苦的问题中产生。

顾名思义，最适合用数据科学方法解决的问题是那些可以用科学严谨性分析数据的问题。如上所述，所讨论的数据可以是任何东西:交易、图像、音频信号、自然语言文本、视频剪辑、温度波动、其他环境传感数据等等。

当遇到一个潜在有趣(有影响力)的想法时，开始考虑量化它的影响(记住 KPI 目标)，你有哪些类型的数据可以分析，以及你可以验证你的推测的方法。