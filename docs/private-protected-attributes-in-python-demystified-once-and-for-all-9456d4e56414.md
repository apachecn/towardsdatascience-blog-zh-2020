# Python 中的私有“受保护”属性——一劳永逸地去神秘化

> 原文：<https://towardsdatascience.com/private-protected-attributes-in-python-demystified-once-and-for-all-9456d4e56414?source=collection_archive---------16----------------------->

![](img/29e38ebb9ed3867db261ccc102fba581.png)

照片由[**clément H**](https://unsplash.com/@clemhlrdt)****[**un splash**](https://unsplash.com/)****

## ****所有关于私有和“受保护”属性的知识都在 748 个单词中****

> ****永远不要使用两个前导下划线。这是令人讨厌的隐私。—伊恩·比金，pip、virtualenv 和许多其他软件的创作者****

****H 这些词你在 Python 的世界里遇到过多少次:*公有*、*私有*、*受保护*？有多少次，那些一个前导下划线`_`，两个前导下划线`__`让你困惑，试图理解它们？****

****好吧，让我们一劳永逸地揭开它们的神秘面纱。私有和“受保护”的属性有什么用。以及它们在 Python 世界中的样子。****

# ****私有属性到底有什么意义？****

****考虑这个场景:你有一个名为`Vehicle`的类，它在内部使用一个名为 *horn* 的实例属性，并且不想公开它*。现在，你想要子类化`Vehicle`并将你自己的类命名为`MyCar.`*****

****如果您在类`MyCar`中创建自己的`horn`实例属性，您将覆盖`Vehicle`的`horn` 实例属性。结果是，你将粉碎`Vehicle`**类中所有使用`horn` 属性的方法。更糟糕的是，调试随之而来的问题将是一件令人头疼的事情。******

******为了防止这种情况发生，`Vehicle`类的开发人员会将`horn`属性*设为私有属性*，以防止这种意外事故。******

# ******Python 中的私有属性******

******在 Python 的世界里，不像 Java，没有办法创建一个私有的修饰符。python 给你的是一个简单的机制，防止**意外**覆盖你的类中的属性，如果有人想从你的类继承。******

******在前面的例子中，如果您想将`horn`属性设为 private，您需要在它前面加上两个下划线:`__horn` *。*这样，Python 将把这个属性名存储在实例`__dict__`中，以下划线和类名为前缀。这样，在`Vehicle`类中，你的`__horn` *属性*就变成了`_vehicle__horn` 而*在* `*MyCar*` 类中就变成了`_MyCar__horn`。python 的这个特性被冠以一个微妙的名字 ***名为 mangling* 。下面是我们目前讨论的代码:********

******示例 01 —私有属性，其中名称**被篡改********

******这里需要注意的是，**名称篡改完全是关于** **安全而不是安全。它不会保护你免受故意的错误行为；只是，偶然的超越。在上面的例子中，您可以简单地通过这样做来改变私有属性的值:`v1._vehicle__horn = 'new value'`。********

# ******Python 中的“受保护”属性******

******无论是名字的乱涂乱画，还是把名字写成`self.__horn` 的歪歪扭扭的样子，都不为皮达尼斯所喜爱。在公共存储库中，您会注意到开发人员通常更喜欢遵循这样的惯例:只给**添加一个前导下划线(`self._horn`)，以防止它们被无意中修改。********

********批评者建议，为了防止属性混乱，只需简单地遵循在属性前加一个下划线的惯例就足够了。这是我在文章开头引用的伊恩·比金的话全文；********

> ********永远不要使用两个前导下划线。这是令人讨厌的隐私。如果担心名称冲突，请使用显式名称混淆(例如 _MyThing_balabla)。这和双下划线本质上是一样的，只是在双下划线模糊的地方是透明的。********

********我必须注意，带有单个前导下划线`_`的属性对于 python 解释器来说没有任何特殊意义。但是，这是皮托尼斯塔世界里的一个很强的惯例。如果您看到一个，这意味着您不应该从类外部访问这样的属性。您甚至可以观察到，甚至在官方 Python 文档的某些角落中，带有单个前导下划线`_`的属性也被称为“受保护的”********

********尽管使用单个前导下划线来“保护”属性的做法很常见，但很少听到它们被称为“受保护的”属性。有些人甚至称之为“私人”********

# ********总而言之********

********将属性设为私有的主要目的是防止子类意外覆盖该属性。在 python 中，使变量私有的官方方法是添加两个下划线，例如`self.__privateattr.`，但是，在 python 社区中，当使变量私有时，强烈倾向于只添加一个前导下划线。您可能经常听到或看到这样的属性被称为“受保护的”********

********因此，只需知道在 python 中将变量设为私有是为了安全，只需添加一个前导下划线就足以保护它们不被无意中覆盖:例如`self._protected`。********

********如果你喜欢我的文章并想阅读更多，考虑注册成为一名媒体会员。每月 5 美元，你可以无限制地阅读媒体上的故事。通过使用下面的链接，你也将支持我作为一个作家。********

********[](https://7sapien.medium.com/membership) [## 通过我的推荐链接加入 Medium-Amir AFI anian

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

7sapien.medium.com](https://7sapien.medium.com/membership)********