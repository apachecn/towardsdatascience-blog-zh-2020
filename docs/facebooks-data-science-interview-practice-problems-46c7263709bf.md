# 脸书的数据科学面试实践问题

> 原文：<https://towardsdatascience.com/facebooks-data-science-interview-practice-problems-46c7263709bf?source=collection_archive---------11----------------------->

## 一些脸书面试问题的预演！

![](img/685f2f687ecfaf186095f7b4f0296d59.png)

在 [Unsplash](https://unsplash.com/s/photos/facebook?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上 [NeONBRAND](https://unsplash.com/@neonbrand?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄的照片

鉴于我的文章的受欢迎程度…

*   [谷歌数据科学面试脑筋急转弯](/googles-data-science-interview-brain-teasers-7f3c1dc4ea7f)，
*   [40 统计学数据科学家面试问题及答案](/40-statistics-interview-problems-and-answers-for-data-scientists-6971a02b7eee)，
*   [亚马逊的数据科学家面试实践问题](/amazon-data-scientist-interview-practice-problems-15b9b86e86c6)，
*   以及[数据科学家常见的 5 个 SQL 面试问题](/40-statistics-interview-problems-and-answers-for-data-scientists-6971a02b7eee)，

这次我在网上收集了一些脸书的数据科学面试问题，并尽我所能回答了它们。尽情享受吧！

***如果这是你喜欢的那种东西，成为第一批订阅*** [***我的新 YouTube 频道在这里***](https://www.youtube.com/channel/UCmy1ox7bo7zsLlDo8pOEEhA?view_as=subscriber) ***！虽然还没有任何视频，但我会以视频的形式分享很多像这样的精彩内容。感谢大家的支持:)***

## 问:你从 100 枚硬币中随机抽取一枚——1 枚不公平硬币(正面朝上)，99 枚公平硬币(正面朝下)，然后掷 10 次。如果结果是 10 头，硬币不公平的概率是多少？

这可以用贝叶斯定理来回答。贝叶斯定理的扩展方程如下:

![](img/5c383f5cfeba7e49157921fd41201963.png)

假设选到不公平硬币的概率表示为 P(A)，连续翻转 10 个头像的概率表示为 P(B)。那么 P(B|A)等于 1，P(B∣ A)等于 0。⁵ ⁰，P( A)等于 0.99。

如果填入等式，那么 P(A|B) = 0.9118 或者 91.18%。

## 问:有一栋楼有 100 层。你有两个相同的鸡蛋。如何用 2 个鸡蛋找到门槛楼层，在这里鸡蛋肯定会从 N 层以上的任何一层破开，包括 N 层本身。

更具体地说，问题是在给定两个鸡蛋的情况下，寻找阈值下限的**最优**方法。

为了更好地理解这个问题，我们假设你只有一个鸡蛋。要找到门槛楼层，你可以简单地从第一层开始，放下鸡蛋，然后一层一层往上爬，直到鸡蛋裂开。

现在想象我们有无限的鸡蛋。寻找最低门槛的最佳方法是通过二分搜索法。首先，你会从 50 楼开始。如果鸡蛋裂开了，你就在 25 楼扔一个鸡蛋，如果鸡蛋没有裂开，你就在 75 楼扔一个鸡蛋，重复这个过程，直到你找到门槛楼层。

对于两个鸡蛋，寻找阈值下限的最佳方法是上述两种解决方案的混合…

例如，你可以每隔 5 层扔第一个鸡蛋，直到它破了，然后用第二个鸡蛋找出在 5 个增量之间的哪一层是门槛层。在最坏的情况下，这将需要 24 滴。

如果你每隔 10 层楼扔第一个鸡蛋，直到它破掉，在最坏的情况下，它会掉 19 下，这比每隔 5 层楼扔第一个鸡蛋要好得多。但是如果你想做得更好呢？

这就是最大遗憾最小化这个概念发挥作用的地方。基本上，这意味着当你以给定的增量完成更多的下降(你跳过多少层)时，你希望每次都缓慢地减少增量，因为阈值楼层的可能楼层会更少。这意味着如果你的第一次下落是在 n 层，那么你的第二次下落应该是在 n + (n-1)层，假设它没有破裂。这可以写成下面的等式:

![](img/20493fe39fb7dc8d50d8854989223b23.png)

更进一步，这可以简化为:

![](img/a33bacd4ff74fefe4c1094b8d803554a.png)

求解 n，你得到大约 14。因此，你的策略将是从第 14 层开始，然后 14+13，然后 14+13+12，等等，直到它打破，然后使用第二个蛋一次一层地找到门槛层！

## 问:我们有两种在 Newsfeed 中投放广告的选择。方案一:每 25 个故事中，就有一个是 ad。方案二:每个故事都有 4%的几率成为广告。对于每个选项，100 个新闻故事中显示的广告的预期数量是多少？

两种选择的预期赔率都是 4/100。

对于选项 1，1/25 相当于 4/100。
对于选项 2，100 的 4%是 4/100。

*如果我遗漏了什么，请随时告诉我，因为这个问题似乎太直截了当了！*

## 问:只知道性别身高，你如何证明男性平均比女性高？

你可以用假设检验来证明男性平均比女性高。

零假设是男性和女性平均身高相同，而另一个假设是男性的平均身高高于女性的平均身高。

然后，您将收集男性和女性身高的随机样本，并使用 t 检验来确定您是否拒绝空值。

## 问:如果 iOS 上 70%的脸书用户使用 Instagram，但 Android 上只有 35%的脸书用户使用 Instagram，你会如何调查这种差异？

有许多可能的变量会导致这种差异，我将检查一下:

*   iOS 和 Android 用户的人口统计数据可能会有很大差异。例如，根据 Hootsuite 的调查，43%的女性使用 Instagram，而男性只有 31%。如果 iOS 的女性用户比例明显高于 Android，那么这可以解释这种差异(或者至少是部分差异)。这也适用于年龄、种族、民族、地点等
*   行为因素也会对差异产生影响。如果 iOS 用户比 Android 用户更频繁地使用手机，他们更有可能沉迷于 Instagram 和其他应用程序，而不是那些在手机上花费时间少得多的人。
*   另一个需要考虑的因素是 Google Play 和 App Store 有什么不同。例如，如果 Android 用户有明显更多的应用程序(和社交媒体应用程序)可供选择，这可能会导致用户的更大稀释。
*   最后，与 iOS 用户相比，用户体验的任何差异都会阻止 Android 用户使用 Instagram。如果这款应用对安卓用户来说比 iOS 用户更容易出错，他们就不太可能在这款应用上活跃。

## 问:每个用户的点赞数和在一个平台上花费的时间在增加，但用户总数在减少。它的根本原因是什么？

一般来说，你会想从面试官那里获得更多的信息，但是让我们假设这是他/她唯一愿意提供的信息。

关注每个用户的点赞数，有两个原因可以解释为什么这个数字会上升。第一个原因是，随着时间的推移，用户的平均参与度普遍提高了——这是有道理的，因为随着使用该平台成为一种习惯性做法，久而久之的活跃用户更有可能成为忠实用户。每个用户点赞数会增加的另一个原因是分母，即用户总数，在减少。假设停止使用该平台的用户是不活跃的用户，也就是参与度和点赞数低于平均水平的用户，这将增加每个用户的平均点赞数。

上面的解释也适用于在平台上花费的时间。随着时间的推移，活跃用户变得越来越活跃，而很少使用的用户变得不活跃。总体而言，参与度的增加超过了参与度很低的用户。

更进一步说，有可能“参与度低的用户”是脸书能够检测到的机器人。但随着时间的推移，脸书已经能够开发出识别和删除机器人的算法。如果以前有大量的机器人，这可能是这种现象的根本原因。

## 问:脸书发现赞数每年增长 10%，为什么会这样？

给定年份的总赞数是用户总数和每个用户的平均赞数的函数(我称之为参与度)。

用户总数增加的一些潜在原因如下:由于国际扩张而获得的用户以及随着年龄增长而注册脸书的年轻群体。

参与度增加的一些潜在原因是用户对应用程序的使用增加，用户变得越来越忠诚，新的特性和功能以及用户体验的改善。

## 问:如果我们测试产品 X，你会看什么标准来确定它是否成功？

决定产品成功的标准取决于商业模式和企业试图通过产品实现的目标。《精益分析》一书展示了一个很好的框架，人们可以用它来确定在给定场景中使用什么指标:

![](img/ba40437322ec42f2e86d394160cad7ae.png)

精益分析框架

## 问:如果一个项目经理说他们想把新闻订阅的广告数量增加一倍，你如何判断这是不是一个好主意？

您可以通过将用户分成两组来执行 A/B 测试:一组是广告数量正常的对照组，一组是广告数量翻倍的测试组。然后，您将选择指标来定义什么是“好主意”。例如，我们可以说零假设是广告数量翻倍会减少花在脸书上的时间，另一个假设是广告数量翻倍不会对花在脸书上的时间有任何影响。但是，您可以选择不同的指标，如活跃用户数或流失率。然后，您将进行测试，并确定拒绝或不拒绝 null 的测试的统计显著性。

## 问:有一个游戏，给你两个公平的六面骰子，让你掷骰子。如果骰子上的数值之和等于 7，那么您将赢得 21 美元。但是，每次掷出两个骰子，你都必须支付 5 美元。你玩这个游戏吗？

掷出 7 的几率是 1/6。
这意味着**期望**支付 30 美元(5*6)赢得 21 美元。
取这两个数字，预期支付额为-$ 9(21–30)。
由于预期付款为负，你不会想要支付此游戏。

# 感谢阅读！

如果你喜欢我的工作，想支持我…

1.  支持我的最好方式就是在**Medium**T7 这里关注我。
2.  在 **Twitter** 这里[成为第一批关注我的人之一](https://twitter.com/terence_shin)。我会在这里发布很多更新和有趣的东西！
3.  此外，成为第一批订阅我的新 **YouTube 频道** [这里](https://www.youtube.com/channel/UCmy1ox7bo7zsLlDo8pOEEhA?view_as=subscriber)！
4.  在 **LinkedIn** [这里](https://www.linkedin.com/in/terenceshin/)关注我。
5.  在我的**邮箱列表** [这里](https://forms.gle/UGdTom9G6aFGHzPD9)注册。
6.  查看我的网站，[**terenceshin.com**](https://terenceshin.com/)。

# 资源

[](https://medium.com/acing-ai/facebook-ai-interview-questions-acing-the-ai-interview-5982add0af55) [## 脸书数据科学访谈

### 脸书雇佣了 CNN 的发明者 Yann LeCun。

medium.com](https://medium.com/acing-ai/facebook-ai-interview-questions-acing-the-ai-interview-5982add0af55) [](https://www.glassdoor.ca/Interview/Facebook-Data-Scientist-Interview-Questions-EI_IE40772.0,8_KO9,23_IP3.htm) [## 脸书数据科学家面试问题

### 我在 12 月下旬在网上申请，然后在 1 月初与一名招聘人员谈了大约 15 分钟。我被安排…

www.glassdoor.ca](https://www.glassdoor.ca/Interview/Facebook-Data-Scientist-Interview-Questions-EI_IE40772.0,8_KO9,23_IP3.htm) [](/the-facebook-data-scientist-interview-38556739e872) [## 脸书数据科学家访谈

### 脸书数据科学家的职位是科技界最令人垂涎的职位之一。它需要多种技能…

towardsdatascience.com](/the-facebook-data-scientist-interview-38556739e872) [](http://mockinterview.co/index.php/2018/04/07/sample-data-science-interview-questions-from-facebook/) [## 来自脸书的数据科学面试问题示例:

### 我们分析了发布在 Glassdoor 上的脸书数据科学家的采访经历和发布的普通采访…

mockinterview.co](http://mockinterview.co/index.php/2018/04/07/sample-data-science-interview-questions-from-facebook/)