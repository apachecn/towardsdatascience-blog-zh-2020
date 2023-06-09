# 动态世界中的静态机器学习模型

> 原文：<https://towardsdatascience.com/static-machine-learning-models-in-a-dynamic-world-ff1ea1b0892c?source=collection_archive---------27----------------------->

## 历史数据正被用于未来将工作的模型。当世界不断变化时，我们的模型保持不变。

![](img/c94763eca6f5fa880916d2b674ede66f.png)

克里斯·劳顿在 [Unsplash](https://unsplash.com/s/photos/change?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

如果你在学术界或工业界工作，你就要解决现实生活中的问题。我们研究的数据不是合成的，它们来自真实世界的读数。在我们的办公室工作时，从与我们的项目、业务或挑战相关的真实事件中抽象出来；我们往往会与我们正在解决的问题失去联系。很容易将项目视为数字。静态数值、字符串和无意义的 id。我们用二进制存储它们，与现实世界脱节。在这种情况下，很容易忘记现实世界是动态的，数据也是如此。当我们忽视或天真地忘记这一现实，并专注于我们心爱的 KPI 时，问题就开始出现了。这个故事是关于我们的机器学习模型如何保持静态，而数据却随着动态世界的变化而每天变化。

在我之前工作的一家公司发生了一次事故后，我开始对我的模特的表现的连续性有点着迷。简而言之，我们的一个直接负责关键引擎输出的模型开始预测荒谬的结果。最糟糕的是，我们没有发现问题，直到我们接到客户愤怒的电话，花了很长时间调试整个管道，才找到根本原因。该模型输出极高或极低的预测值。回想起来，我们发现堆栈中没有故障组件。没有 bug，没有错误。上游数据引起的问题。从上游消耗的数据，真实世界的读数，已经改变了。

**模型是由世界快照建立的**

如果您没有采用某种在线学习方式，即模型定期更新，那么您将使用历史数据。您使用数据存储中的一些数据并训练您的模型。你经常这么做。你获取历史数据，通过管道传输，得到你的模型。这里的关键词是历史性的。您处理的是已经过时的数据。回顾过去的同时，你也在为未来构建解决方案。

有了这些数据，你实际上是在世界的快照上开发了你的解决方案。原始数据，真实世界的读数代表快照。这个快照可以是几周、几个月或几年。快照越长越好。尽管如此，这并不能保证未来会遵循您快照中的相同行为。

**当世界改变时，模型就会失效**

当您处理历史数据时，您就与您的模型签订了合同。您向您的模型保证数据的属性不会改变。作为交换，模型给你一个准确的历史描述。你依赖于你的 KPI。当你超过一个门槛时，庆祝一下。将您的解决方案投入生产。当同样的模型还在那里时，你的合同仍然有效。

现实世界不断变化，我们的上游数据也是如此。如果你不采取额外的步骤，你的模型将会忽略这些变化。你的合同还在。随着变化，当一个重大事件发生时，或者随着时间的推移，您的上游数据开始变化。它可能会发生如此剧烈的变化，以至于上游数据在某个时候可能不再类似于您的模型所依据的历史数据。此时，你违反了你的契约，你的模型开始无声地失败。

**演出的连续性**

随着世界的变化，我们的数据也在变化，我们需要确保我们的模型仍然做得很好。即使我们可能不做任何事情来使模型走上正确的道路，我们也需要知道性能。为了确保我的模型的性能仍然令人满意，我倾向于进行以下检查。请注意，这些检查是为您所服务的模型/解决方案服务的。

**1。上游数据检查**

对于这一个，您根据您的项目定义哪个阶段是上游。这个想法是在进入模型之前观察任何阶段的数据，以做出预测。虽然是这种情况，但在将数据输入模型之前的最后阶段可能是一个很好的阶段。

该检查的目的是确保上游数据仍然类似于训练模型时使用的历史数据的分布或遵循相同的模式。一种简单但有效的方法是计算每个固定时间间隔的上游数据的分布，并将其与历史数据的分布进行比较。如果两个分布的相似性很接近，你就是绿色的。否则，您会发出警报，并让解决方案的所有者知道。

**2。下游输出检查**

下游检查背后的思想与上游数据检查非常相似。在这个例子中，不是检查上游，而是检查模型或服务的输出。与上游检查一样，您可以监控生产中模型输出的分布与历史数据输入时模型输出之间的相似性。监视两个分布之间的相似性，如果它开始偏离，就发出警报。

这两种检查很容易实现。您可以将它们放在一个实时监控仪表板中，或者只是在超过阈值时向存储库的所有者发送一封邮件。就像任何支票一样，知道它们的存在是件好事。

如果你对我在这个故事开始时提到的事件的结局感到好奇，让我继续。变化来自客户端。我们的阅读依赖于运行在客户端的复杂而冗长的框架配置列表。后来很明显，客户改变了一些主要的配置。这一变化对我们的读数影响很大，导致了上游数据的重大变化。因此，输入模型的新数据点与我们用于训练的数据完全不同。只有我们对数据进行一些检查，我们才能意识到这种变化，并采取一些措施使事情朝着正确的方向发展。幸运的是，这一事件没有对业务造成太大影响，几天后一切都恢复了正常。这个有价值的教训让我对我们模型的静态本质更加多疑，并且怀疑我的解决方案在产品中是否仍然如我预期的那样工作。