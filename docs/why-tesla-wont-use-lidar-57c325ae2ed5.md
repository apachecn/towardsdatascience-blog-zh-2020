# 为什么特斯拉不使用激光雷达

> 原文：<https://towardsdatascience.com/why-tesla-wont-use-lidar-57c325ae2ed5?source=collection_archive---------1----------------------->

## 哪种技术最适合自动驾驶汽车

![](img/916c53a6b214d61d80ab9ab3d7ea43ec.png)

戴维·冯迪马尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

几乎每一家从事无人驾驶汽车的公司现在都在使用激光雷达。优步、Waymo 和丰田都用它，但特斯拉不用。我想回顾一下这两种相互竞争的技术能够提供什么，以及我们应该对未来的自动驾驶汽车有什么期待。

# 激光雷达与视觉

**激光雷达**是一种通过发射激光并检测它们返回需要多少时间来测量距离的方法。这个想法类似于雷达，但我们使用的不是无线电波，而是激光。这项技术在探测甚至高达毫米的物体时非常精确。

**计算机视觉**是人工智能的一个领域，训练计算机理解视觉世界。这基本上是对人类视觉的逆向工程。

# 特斯拉的愿景

(埃隆·马斯克在特斯拉自主日)

特斯拉一直严重依赖视觉，并与激光雷达传感器背道而驰。与此同时，所有其他公司使用激光雷达，似乎并不关心。埃隆·马斯克甚至说:

> 激光雷达是一个傻瓜的差事…任何依赖激光雷达的人都注定要失败。——埃隆·马斯克

如果你想了解埃隆对技术选择的所有想法，请务必查看他在特斯拉自主日的讲话。

# 费用

![](img/ea5f069823b56bc1b82681ef310d3dc0.png)

照片由 [Pepi Stojanovski](https://unsplash.com/@timbatec?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

特斯拉另辟蹊径最明显的原因是成本。在汽车上放置一个激光雷达设备的成本大约为**10，000 美元**。谷歌及其 Waymo 项目已经能够通过引入大规模生产来略微减少数量。然而，成本仍然相当可观。

特斯拉高度关注成本，确保人们买得起汽车。在已经很贵的汽车上增加激光雷达的价格意义重大。

# 实际道路应用

![](img/0e52380ad7cb4867404379f1237d0b10.png)

照片由 [Charlie Deets](https://unsplash.com/@charliedeets?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

最重要的一点，也是会议中高度强调的一点，就是与人类视觉的相关性。作为人类，我们不会为了开车而朝各个方向发射激光。正如埃隆·马斯克所说，汽车也不应该。

我们在路上看到的一切都充满了*视觉信息*。所有的标志，转弯，十字路口都是为了帮助我们导航。所有这些都是静止的物体，激光雷达能够如此精确地探测到它们真是太好了。

当*移动物体*出现在路上时，问题就开始出现了。人、狗、飞来飞去的塑料袋，都是我们在路上经常遇到的物体。激光雷达无法探测它们是如何移动的，甚至无法探测这些物体是什么。

**激光雷达无法区分道路颠簸和塑料袋**。这是会议中提到的一个例子，考虑到这一点非常重要。如果我们在高速公路上高速行驶，并且有一个塑料袋，我们不需要快速停车。如果我们撞上了，问题不大。

现在，如果汽车停下来，真正的危险就来了。后面的车可能无法对我们在路中间停车做出如此迅速的反应。这种情况进一步证明了制造自动驾驶汽车时对细节的关注。

特斯拉明确表示，他们的相机和雷达系统能够检测到一个物体是什么。向前看的雷达能够迅速判断前方是否有问题。一旦一个物体进入视线，摄像机将决定这个物体是什么，然后汽车可以对这种情况做出反应。

# 适应

![](img/8e6e332dfee4e2c75988b2810a547007.png)

照片由 [Jp Valery](https://unsplash.com/@jpvalery?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

从 Autonomy Day 和埃隆·马斯克的其他采访中，另一个重要的收获是，系统是为了适应而生的。他们谈论了很多关于所使用的神经网络以及该系统如何能够使用所提供的数据来做出合理的决定。

特斯拉竞争对手的一个大问题是缺乏这种适应能力。这些系统中的大多数要么严重依赖带有道路线的高精度地图，要么从未在真实道路上测试过。是的，我们已经看到 Waymo 在城市中行驶。然而，只有大型道路具有高效率的地图。在这些演示中，照明、天气条件和交通都很理想。大多数人不会每天都在这样的路上开车。

更小的道路，有意想不到的转弯和大小变化的车道，更为常见。另外，特斯拉是一辆你可以买到的真车。人们已经驾驶特斯拉汽车行驶了超过 10 亿英里，而 Waymo 只测试了大约 1000 万英里。

特斯拉能够积累的大量困难且不可预测的道路数据是无价的。这就是系统学习和不断改进的方式。这种概念实际上很有前景，因为客户实际上看到了不断的改进。

# 准确(性)

![](img/a95c3437d4804aaa8b366bed5ae67ba5.png)

Jannes Glas 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

从康奈尔大学发表的一篇研究论文中可以推导出另一个有趣的观点。本文讨论了如何使用立体相机生成几乎与激光雷达地图一样精确的 3D 地图。

我们可以从这篇论文中得出结论，除了花费 7500 美元购买激光雷达设备，您还可以购买几台仅花费 5 美元的相机，并获得几乎相同的精度。因此，当特斯拉的人说这种硬件很快就会过时时，他们可能有道理。

# 最后的想法

随着自动驾驶汽车领域投入了多少资金，以及竞争的不断加剧，我们可以相当乐观地认为，这种汽车正在到来。特斯拉是否会成为这样做的公司，我们无法知道，甚至可能不需要知道。事实上，可能有几种方法来开发无人驾驶汽车。我们甚至可能最终看到两者的结合，这并不令人惊讶。

说到特斯拉，我们实际上可以购买这样一辆车。他们被带到世界各地，实际上可以实时观察到进展情况。你不能买 Waymo 或优步汽车。

特斯拉的决定的原因包括在这里，但这并不意味着我们都应该赌特斯拉。也许其他一些公司会先制造出自动驾驶汽车。我们所知道的是，一些公司会这样做，我们应该密切关注该领域发生的一切。

# 参考资料:

[1]王，杨，曹伟林，加尔格，d，哈里哈兰，b，坎贝尔，m .，&温伯格，K. Q. (2019)。来自视觉深度估计的伪激光雷达:弥补自动驾驶 3d 物体探测的差距。在*IEEE 计算机视觉和模式识别会议论文集*(第 8445–8453 页)。

[2]自动驾驶评测。(2019 年 4 月 27 日)。 *Elon Musk 在相机上对比自动驾驶和自动驾驶汽车的激光雷达*[视频]。YouTube。[https://youtu.be/HM23sjhtk4Q](https://youtu.be/HM23sjhtk4Q)

[3]霍金斯，A. J. (2019)。Waymo 将向不会与其机器人出租车业务竞争的客户出售激光雷达。2020 年 09 月 07 日检索，来自[https://www . the verge . com/2019/3/6/18252561/waymo-sell-lidar-laser-sensor-av-customer-robot-taxi-competition](https://www.theverge.com/2019/3/6/18252561/waymo-sell-lidar-laser-sensor-av-customer-robot-taxi-competition)