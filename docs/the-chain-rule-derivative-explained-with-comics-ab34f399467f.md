# 用漫画解释链式法则导数

> 原文：<https://towardsdatascience.com/the-chain-rule-derivative-explained-with-comics-ab34f399467f?source=collection_archive---------28----------------------->

## 这一切都是从 Seth 偶然发现神话中的"**平方机器**"开始的:

![](img/68069ace1c3719ddb04e4962fe10c2e7.png)

图片来自 [Pixnio](https://pixnio.com/media/combine-vehicle-agriculture-equipment-machine)

传说中，无论你将什么东西放入平方机器，机器都会给你那个数量的物体**平方**。

![](img/f86fac4ea1e631bc76d21cade3eadd15.png)

图片来自[维基媒体](https://commons.wikimedia.org/wiki/File:Man_Talking_Angry_on_the_Phone_Cartoon_Vector.svg)

于是，比利把这颗巨大的钻石带到了磨方机前，他们把它放了进去。

![](img/dab3938302a3597f533d3a68978452c7.png)

等一下…

![](img/be0ade10814959c3630ba9580b5bb2f4.png)

但是比利已经有了更大的想法…

![](img/074d5bf07c090b23779dd999577f7595.png)

图片来自[维基媒体](https://commons.wikimedia.org/wiki/File:Black_Man_Waving_Hand_Cartoon_Vector.svg)

于是他们放了 3 个瓶子，出来了 9 个！

![](img/9dacbbbe129a38bc274a556ed9f2770c.png)

然后，比利想知道“如果我们把 3 包洗发水放入平方机会发生什么？”

他们照做了，又一次，9 个瓶子出来了！

![](img/b4db387f1d4a937fdddb7d6d0f2e755a.png)

比利发现，如果你把“x”瓶子放进去，你会把“x”瓶子拿出来，但他也注意到了其他一些非常有趣的事情:

他意识到你可以用价值包来描述这台机器。如果您放入“x”价值包，您会得到“3”价值包。

> ^Let 这才明白过来。这是“链式法则”中最难理解的部分。

Billy 发现，您还可以用“瓶子”或“价值包”来描述这台机器的*衍生产品*:

1.  **机器如何响应添加/取出洗发水？**

X 的导数当然是 2x。

2.**机器如何响应添加/移除价值包？**

3 合 1 超值套装是 3 倍。如果你用“3x”代替上面例子中的“x ”,你会得到 2 的导数(3x ),或者 6x。

Billy 现在知道了平方机器如何将*相对于*移动到价值包，这在以后会非常有用…

# 事情变得复杂了

他们找到了第二个神奇的机器。这台叫做“三倍机”。如果你把一个项目放在“三倍机”，它会给你一个 3 包！

![](img/df9d156055861334371050031430f134.png)

照片来自[geograph.org](https://www.geograph.org.uk/photo/5524155)

Seth 和 Billy 高兴地跳起来，急切地将一个洗发水瓶子放入三倍机中(*没有意识到他们可以将钻石放在那里*)。

正如所承诺的，一个 3 包弹出。

赛斯开始变得渴望权力。他想从地球表面根除油腻的头发。

![](img/e4fb2f9ceeedd8d8921e6ad9d267668c.png)

他决定将两台机器“链接”在一起。他计划将物品放入“三倍机”，然后连接两台机器，以便三倍机生产的价值包直接进入“平方机”。

![](img/f5d0fe9dcec76d4d69ae04422e44cc04.png)

Seth 想知道:“我如何计算新组合函数的总导数？”

比利心想。

![](img/16222060681685bffe98e3c8a90fd21d.png)

就在那时，Billy 意识到:我们知道三倍机如何相对于洗发水瓶子移动(3x)，我们也知道平方机如何相对于三包移动(6x)。我们可以将这些相乘，并计算出“x”的变化如何影响平方机器的最终输出。

3x * 6x = 18x

这个概念适用于所有“链”类型的函数。如果我们计算外部函数如何将*相对于*移动到内部函数，并且我们计算出内部函数如何将*相对于*移动到 x，我们可以将这些相乘来发现总输出如何相对于 x 移动

# 我们如何计算外层函数相对于内层函数的运动？

为了计算平方机器如何将*相对于*移动到(3x ),我们对 x 求导，但是用(3x)代替 x。

(3 倍)

变成了:

2(3x)
6x

如果我们想计算平方机器如何相对于“sin(x)”机器移动*到“sin(x)”机器，传入 sin(x)，对外部部分求导，然后简化。*

(sin(x))

2 * sin(x)

# 这个故事的寓意:一切都是相对的

假设你已经设置了一个"*汽车- >马力*计算器。

如果一辆车有 10“马力”，我们的函数就是 f(x) = 10x。

如果我们通过 5 辆车，我们正确地获得 50 马力。

如果你传入 1(飞机)，你将得到 10 马力，这是不正确的，因为这个函数是马力*相对于汽车*的度量。

但是，如果我们有一个“*飞机- > carpower* ”计算器，我们可以将两个函数相乘，计算出一架飞机有多少“*马力*”。

# 关于作者

*我是 FlyteHub.org 的创始人约翰尼·伯恩斯，这是一个免费开源工作流程库，用于执行无需编码的机器学习。我相信在人工智能上的合作会带来更好的产品。*