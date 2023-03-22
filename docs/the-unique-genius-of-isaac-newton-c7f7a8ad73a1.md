# 艾萨克·牛顿的独特天才

> 原文：<https://towardsdatascience.com/the-unique-genius-of-isaac-newton-c7f7a8ad73a1?source=collection_archive---------9----------------------->

## 一个著名数学结果的漂亮证明

![](img/a9cab5d21d44ac7e51ebf958b64468d7.png)

图片来自[维基百科](https://en.wikipedia.org/wiki/Woolsthorpe_Manor)。

艾萨克·牛顿(1642-1727)是有史以来最有影响力的思想家之一。他对科学最重要的贡献是他的书《T2 哲学自然数学原理》，出版于 1687 年，在那里他阐述了著名的三大运动定律和引力定律，统治了科学界 200 多年。用著名天体物理学家、诺贝尔奖获得者[Subrahmanyan**Chandrasekhar**](https://en.wikipedia.org/wiki/Subrahmanyan_Chandrasekhar)**的话说:**

> **只有当我们观察牛顿成就的规模时，有时与其他科学家进行的比较才显得对牛顿和其他人都不合适。**
> 
> **钱德拉塞卡尔**

**在数学方面，牛顿"明显地推进了后来研究的数学的每一个分支"，但是他最著名的两个发现是广义二项式展开和微积分。**

**![](img/07c8b2700ab2126a5c95942c64cf59b7.png)**

**图 1:左边是牛顿 46 岁时的肖像，由 17 世纪末 18 世纪初英国主要肖像画家 [Godfrey Kneller](https://en.wikipedia.org/wiki/Godfrey_Kneller) 所作[来源](https://en.wikipedia.org/wiki/Isaac_Newton)。右边是《原理》第一版的扉页([来源](https://en.wikipedia.org/wiki/Philosophi%C3%A6_Naturalis_Principia_Mathematica))。**

**在本文中，我的重点将是牛顿早期的数学成就。我将描述他对广义二项式展开的推导，以及他如何应用它来获得正弦函数的幂级数展开。根据德里克·怀特塞德，[认为](https://arquivo.pt/wayback/20090714064823/http://www.hps.cam.ac.uk/news/whiteside.html)是“他那一代最重要的数学史家”，这是正弦(和余弦)的幂级数第一次出现在欧洲。**

# **牛顿广义二项式展开**

**牛顿的数学创新是多方面的。但可以说，他的起点是所谓的[广义二项式展开](https://en.wikipedia.org/wiki/Binomial_theorem#Newton%27s_generalized_binomial_theorem)(更多细节见 [Dunham](https://books.google.com.br/books?id=Wj9hDwAAQBAJ&dq=calculus+gallery) )的发现，这首次出现(连同牛顿在微积分方面的一些工作)于 1676 年他发给 Gottfried Leibniz 的一封信中。这封信被称为他的 e *pistola prior。***

**![](img/0cfb20af7448a68ea11a9c9ecb9399d7.png)**

**图 2:之前的*书信，*牛顿写给莱布尼茨的信，信中描述了他的广义二项式展开的发现，这发生在很多年前([来源](https://www.maa.org/book/export/html/116901))。**

****牛顿原记法中的二项式展开** 在牛顿的记法中，展开式表示为:**

**![](img/6b85598d5a4c72ee1bf28f38ebc56abc.png)**

**等式 1:牛顿使用他的符号的二项式展开。**

**在这个表达式中， *A* 、 *B* 、 *C* 、 *D* 、……代表系列的前几项:**

**![](img/c20f46b3674739d57838a395fea8413c.png)**

**等式 2:在牛顿的原记法中， *A* ， *B* ，…代表级数的前几项。**

**牛顿在*书信*中给出的例子是:**

**![](img/97ecc25d4d873b34d2be00cee78d51ab.png)**

**等式 3:牛顿在他的书信中给出的例子。**

**扩展的前两项是:**

**![](img/62288dae148dda4925813f2e39d540ec.png)**

**依赖于前一项 *B* 的第三项类似地获得:**

**![](img/c7d4f0cbda93a4502a80c7b285203c14.png)**

**该过程然后可以无限地继续*。结果是:***

***![](img/c8e951fbeae72bf6146a85f539281325.png)***

*****获得现代符号** 我们可以很容易地用现代符号写出二项式展开式。我们首先从等式的左边分解出 *P* 项。1 并将 *A* 、 *B* 、 *C* 、 *D、…* 替换为相应的先前术语(见等式。2):***

***![](img/48a9a80a0116fb29008bc44201d8a47e.png)***

***取消 *P* 项，并将分子中的系数除以分母中的因子 *n* ，我们得到:***

***![](img/174311063b9a6747ebe893b7e7ce3b3e.png)***

***我们可以用[二项式系数](https://en.wikipedia.org/wiki/Binomial_coefficient)改写这个表达式。为了方便起见，我们将 *m* / *n* 重命名为 *m* ，并应用阶乘的性质将展开式的系数重写为:***

***![](img/fd568f530c960714ec5e3123626369ac.png)***

***使用二项式系数的标准符号:***

***![](img/d0ce452575fb34c9d052ba516a69c425.png)***

***我们得到现代形式的二项式展开式:***

***![](img/1a1a97727ee966c802596a1b97664572.png)***

***等式 4:用现代符号写出的二项式展开。***

# ***牛顿如何导出二项式展开式***

***从英国数学家约翰·沃利斯和其他人之前的工作中，牛顿知道如何对整数指数进行二项式展开:***

***![](img/67b7e58c698f1b38dca69f46e1bbd669.png)***

***等式 5:在牛顿之前已知的整数指数的二项式展开式。***

***这些系数有趣的可视化显示在下面的图 3 中。***

***![](img/3103f28a806e1736104c446c854796d5.png)***

***图 3:指数 1、2 和 3 的二项式展开的可视化([来源](https://en.wikipedia.org/wiki/Binomial_coefficient))。***

***牛顿的目标是扩展方程式。5 为了包括跟随在 [Bressoud](https://www.macalester.edu/aratra/edition2/chapt2.html) 之后的指数 *m.* 的非整数值，我们可以在一个表中安排系数，包括用于展开具有非整数值 *m* 的空行:***

***![](img/5fec7d5c392bd3553afa4f86380d7daf.png)***

***图 4:牛顿之前已知的二项式展开的系数表。***

***牛顿想让到填充这个表格中的空单元格*。他的推理如下。****

***第一列和第二列不难猜。第一个只包含 1，第二个随着 m 线性增加***

***![](img/306ac5c74ebbfa310f77f698b6e56e14.png)***

***图 5:第一列和第二列的空白单元格被填充的二项式展开系数的原始表格。***

***现在让我们考虑第三列。首先，我们注意到它只包含[个三角形数字](https://en.wikipedia.org/wiki/Triangular_number)(见下面的图 6)，这可以使用简单的公式获得:***

***![](img/a985cb868e0346530e1a2db0852ba3a9.png)***

***等式 6:第 I 个三角数的公式。***

***![](img/5cba954ea01553cb8be4b115463bb8a7.png)***

***图 6:三角数示例([来源](https://en.wikipedia.org/wiki/Triangular_number))。***

***我们还注意到第 *m* 行总是包含第( *m-* 1)个三角数。更具体地说， *m* =2 行包含第**第**个三角数， *m* =3 行包含第**第二**个三角数， *m* =5 行包含第**第四**个三角数。在等式中代入( *m-* 1)。6 我们得到:***

***![](img/54ef0ce2bda23a45e79808c8203da92a.png)***

***等式 7:第三列中的值对 m 的依赖性。***

***然后我们可以完成第三列:***

***![](img/b0a3beb8ecdf0a72eadb21a712eba743.png)***

***图 7:前三列完成的二项式展开的系数表。***

***现在，请注意，对于前三列，值是多项式增加的。***

*   ***第一列是常数(零阶多项式)***
*   ***第二列线性增加(一次多项式)***
*   ***第三列根据等式二次增加。7(二次多项式)***

***基于这种模式，牛顿推断第四列应该作为三次多项式增加。由于这个未知的多项式在 *m* = 0，1 和 2 时消失，所以它必须具有以下形式:***

***![](img/e3ad4fede61b650f0385b83fc5d46d9a.png)***

***其中常数 *a* 可以例如使用表的第七行来获得，根据该表 *p* (3)=1。因此:***

***![](img/3916fc1db1227f1f0af451d3dcd1d5d1.png)***

***然后，我们可以填充第四列的空白单元格:***

***![](img/b333d40ac8ef1f0a9161898e3240cee3.png)***

***图 8:填充了前四列的二项式展开的系数。***

***牛顿的过程现在清楚了。可以快速得到第五列和第六列对 *m* 的依赖关系:***

***![](img/70ade875bb88c0cd89cb191facd566da.png)***

***我们终于可以填满整张桌子了:***

***![](img/626c114877519a92c7641239ab0d087b.png)***

***图 9:包含 x 的五次方二项式展开系数的表格。***

***将军接着表述道:***

***![](img/a72289dda48c2523ad197fe1daba660c.png)***

***等式 7:牛顿二项式展开。***

***(其中使用了之前看到的二项式系数公式)。我们应该注意到，引用[怀特塞德](https://en.wikipedia.org/wiki/Tom_Whiteside)的话:***

> ***自相矛盾的是，这样的沃利斯插值程序，无论多么合理，都不能作为证明，牛顿数学方法的核心原则缺乏任何严格的证明。。。当然，二项式定理非常有效，这对 17 世纪的数学家来说已经足够了。”***
> 
> ***— D .怀特塞德***

# ***推导正弦幂级数的幂级数***

***在他 1669 年的手稿“[中，正弦函数“](http://www.newtonproject.ox.ac.uk/view/texts/normalized/NATP00204)[的幂级数的推导为【牛顿】的精湛表现](https://www.britannica.com/topic/Newton-and-Infinite-Series-1368282)”加冕。***

***![](img/1a0253b91138ca425284ed37d0e59add.png)***

***图 10:一页牛顿 1669 年的手稿“关于用含有无穷多项的方程进行分析”([来源](https://books.google.com.br/books?id=VTgPAAAAQAAJ&printsec=frontcover&source=gbs_ge_summary_r&redir_esc=y#v=onepage&q&f=false))。***

***理解牛顿推导所需的所有元素都包含在下面的图 10 中(基于[邓纳姆](https://books.google.com.br/books?id=Wj9hDwAAQBAJ&dq=calculus+gallery))，这是一个函数图***

***![](img/229d02af8f13b71bfd8f517c91398ce6.png)***

***方程式 8:单位半径圆的右上象限的方程式。***

***它描绘了半径为单位的圆的(一个[象限](https://en.wikipedia.org/wiki/Circular_sector#Quadrant))。***

***圆弧 *αD* 等于 *z* (圆的半径为 1)，从图 10 中我们得到:***

***![](img/f47f724300f6da088a0fa701edf21192.png)***

***等式 9:由于圆有单位半径，所以角度 z 的正弦等于横坐标 x。***

***因此，目标是确定 *x* (作为 *z* 上的幂级数)。***

***![](img/4b5ae25dcea2ab0db6d2507be15150f6.png)***

***图 10:Eq 的绘图。8 包括获得正弦函数的功率扩展所需的所有元素(图改编自 [Dunham](https://books.google.com.br/books?id=Wj9hDwAAQBAJ&dq=calculus+gallery) )。***

***三角形 DGH 和 DBT 是相似的。由于三角形 ABD 和 DBT 也相似，我们得到:***

***![](img/6dae0f37f57461591767a0ec75ab3f2e.png)***

***为了方便起见，这里使用了[莱布尼兹符号](https://en.wikipedia.org/wiki/Leibniz%27s_notation)。使用 Eq。8 这个表达式变成了:***

***![](img/b9f321c7433f208d0a2dcdb12ff913e2.png)***

***牛顿的下一步是将他的二项式展开应用到右边:***

***![](img/914949d231f9d5afacca2d680f0fa095.png)***

***现在反转 Eq。9 为了获得*z*=*z*(*x*)= arcsin*x*，并对上面的二项式展开进行积分，得到:***

***![](img/bb685d9adb4d93f76db45095c667a30b.png)***

***等式 10:反正弦级数。***

***注意，牛顿获得该表达式所需的唯一积分是对应于以下[反导数](https://en.wikipedia.org/wiki/Antiderivative)(或不定积分)的[定积分](https://en.wikipedia.org/wiki/Integral):***

***![](img/f1a1ee9ad00b75f73c53aa381dc75e3f.png)***

***其中 *C* 是常数。***

***在他的最后一步，牛顿必须转换(或者更准确地说，反转)Eq。10 转换成正弦函数的展开式(而不是反正弦函数的展开式)。为此，他使用了他以前开发的许多工具中的一种，即他的幂级数求逆技术。***

## ***应用幂级数求逆得到 Sin z***

***待求逆的级数为等式中的 *z* ( *x* )。10，即:***

***![](img/b547eb9c9d91a83f2bbb311241f5fc3a.png)***

***等式 11:要展开的系列。***

***换句话说，牛顿追求的是 *x* ( *z* )，就 *z* 而言的 *x* 的幂级数。遵循他的策略，我们从执行以下步骤开始:***

*   ***从第一项开始，在本例中为 *x* = *z****
*   ***将要导出的数列表示为*x*=*z*+*p****
*   ***将*x*=*z*+*p*代入等式。11***
*   ***仅保留 *p* 中的线性项，根据 *z* 对结果进行反演，得到 *p****

*****更具体地应用策略** ，让我们把这个系列写成:***

***![](img/952a637c0770cca6d31b330a003921d7.png)***

***等式 12:等式 11 中各项的重新排列。***

***(参见[邓纳姆](https://books.google.com.br/books?id=Wj9hDwAAQBAJ&dq=calculus+gallery))。下一步是只保留 *x:* 中的线性项***

***![](img/15020c3f794441629548e8bf9d57f8a7.png)***

***方程式 13:膨胀的线性近似。***

***为了说明所有被删除的项，牛顿接着用一个未知的级数 *p* 写出 *x* :***

***![](img/562de5b745618dc633b1b141842e709c.png)***

***等式 14:引入未知的级数 p，以说明线性近似中丢弃的项。***

***并将其代入等式。12:***

***![](img/0e1d0119118e36ca180d7d0037f11eec.png)***

***等式 15:原始系列设置 x = z+p。***

***扩展这个表达式并将 *p、*的幂分组，他得到:***

***![](img/53b2df54ff69381e8ddb6efb7631e482.png)***

***等式 16:对扩展等式进行分组。15 的 p 次方。***

***牛顿然后去掉幂大于 1 的项，并求解 p:***

***![](img/12ea78ca3d863ab5384db1f17e4e0f95.png)***

***等式 17:去掉等式中幂大于 1 的项后得到的表达式。16 和求解 p。***

***牛顿只保留分子的第一项，并考虑到被删除的项，引入了一个新的待定序列 *q* ，定义如下:***

***![](img/adc38e0a6b9ca031ab56041a8f53a979.png)***

***为了确定 *q* ，牛顿将这个新的 *p* 代入等式。16，只保留 *q* 和中的线性项，为 *q* 求解。这给出了一个类似于等式的表达式。17(用于 *p* )。然后，他再次只保留分子中度数最低的项，得到:***

***![](img/452b749c84fa33a26fc58d599664af31.png)***

***该程序可以无限期地执行*。*现在从 Eq。9， *x* = sin *z* ，他最终得出了正弦函数的如下表达式:***

***![](img/a54a106f1f6cb2828a6cb0cbb52b5166.png)***

***等式 18:正弦函数的幂级数展开，最高可达 5 阶。按照牛顿的策略，其他项可以很容易地得到。***

***![](img/7f6bc1dad228b598bcd846ac8d0f0d58.png)***

***图 11:牛顿 1669 年对正弦和余弦函数幂级数的演示。***

***这个结果可以通过[泰勒级数](https://en.wikipedia.org/wiki/Taylor_series)在今天得到。然而，牛顿做这件事的方式完全不同。正如[中提到的，邓纳姆](https://books.google.com.br/books?id=Wj9hDwAAQBAJ&dq=calculus+gallery)的推导“提醒我们，数学不一定以今天教科书的方式进化。相反，它是在断断续续和奇怪的惊喜中发展起来的。”***

***我的 [Github](https://github.com/marcotav) 和个人网站 [www.marcotavora.me](https://marcotavora.me/) 有一些其他有趣的材料，既有关于理论物理的，也有关于数据科学和金融等其他主题的。看看他们！***