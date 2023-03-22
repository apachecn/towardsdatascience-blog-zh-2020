# 人力资源部门的机器学习和人工智能

> 原文：<https://towardsdatascience.com/machine-learning-and-ai-in-human-relations-departments-59ed8f9a14d5?source=collection_archive---------31----------------------->

## 生产力的新时代还是去除人力资源中的“人”？

![](img/488f88dd08174e5de66922fe00c6b3ad.png)

资料来源:Pexels.com

# 介绍

深度学习和人工智能已经彻底改变了医疗保健、金融服务和零售等行业，许多公司都欢迎新技术。然而，人力资源(HR)部门在将智能系统集成到他们的工作流程中时遇到了更多的挑战。

人力资源部门的任务是管理组织的员工——雇用、解雇、解决纠纷、工资、福利等等。这些任务中的许多似乎已经成熟，可以通过机器学习实现自动化，然而，它们也往往是主观的，移交控制权带来了有趣的伦理挑战。

# 员工招聘

招聘过程既费力又昂贵。从审查简历、面试和培训新员工，雇用新员工会给组织带来新员工工资之外的巨大成本。然而，这种成本通常是值得的，因为如果必须解雇员工并重新开始这一过程，做出错误的决定会花费更多的钱。不仅需要再次产生雇佣成本，而且还会出现产量损失和新员工达到满负荷生产所需的时间。

正因为如此，许多公司已经将目光投向深度学习，以提供降低雇佣员工成本和提高雇佣员工质量的解决方案。然而，这些尝试并不总是按计划进行。

从 2014 年到 2018 年，亚马逊的一个团队建立了审查申请人简历的系统，以简化招聘顶级人才的流程。为了训练他们的算法，该团队利用过去十年提交给该组织的简历汇编了一个训练数据集。

亚马逊曾希望该系统能够自动识别前 x 名申请人，从而大幅减少从申请人中识别顶尖人才的时间。然而，他们后来发现，该系统对男性申请者比对女性申请者更有利。这是因为向亚马逊提交简历的男性求职者多于女性，这就产生了一个有偏见和扭曲的数据集。

创建公正的招聘系统可能是一项艰巨的任务。由于大多数公司很少有 50%的男性员工和 50%的女性员工，该模型通常可以识别出它认为最能说明一个好员工的因素，但实际上招聘经理并没有考虑这些因素。

为了创建准确的招聘决策和候选人排名系统，必须注意收集用于培训的数据集，以消除不必要的行为。此外，对模型进行硬编码以忽略某些特征(如姓名、性别和种族)也是可行的。

# 每小时调度

管理小时工的人力资源团队在创建时间表时有一项艰巨的任务。当你的员工不是全日工作且有一致的时间表时，经常会出现时间冲突。由于工作日程不可预测，人力资源经理(通常是总经理)的一个关键职能是管理休假和换班请求。

如果你问许多餐馆或零售店的经理，日程安排和与之相关的任务经常占据他们工作日的很大一部分。然而，深度学习系统开始承担这一负担。

自动化系统可以分析这些请求，并根据个人层面的预定义业务规则自动批准或拒绝它们。例如，许多雇用兼职倒班工人的组织不允许他们的员工在一周内工作 40 个小时或更多。如果换班请求使一名员工一周工作超过 40 小时，系统将拒绝该请求，无需任何人工干预。

当与预测需求信息相结合时，这些系统变得更加强大。准确预测何时需要额外的员工并相应地调整时间表和休假请求，可以在需求较低时节省劳动力成本，并在需求较高时确保有足够的员工工作，从而提高员工管理的效率。

虽然这些系统可以极大地改善员工管理并减少经理的工作量，但它可能会打击员工的士气。通常情况下，休假和换班请求可能是个人性质的。如果一个自动化系统拒绝了一个重要事件的休假请求，员工可能会对组织产生怨恨。

要使自动排班系统正常工作，重要的是要彻底定义业务规则，并确保员工有办法通过他们的经理获得对模型决策的否决。

# 劳动力分析

分析团队让组织能够以前所未有的方式利用他们的数据，让公司做出前所未有的明智决策。

当我们想到业务数据时，我们通常会想到他们收集客户数据以更好地了解他们。然而，许多组织也在收集其员工的数据。

跟踪组织员工的关键指标可以让人力资源部门更好地了解他们的员工。跟踪员工的情绪、生产力和与组织的联系使人力资源部门能够更好地分配资源并提高员工的效率。此外，它允许预测分析模型识别有离开组织风险或有可能晋升的员工。

虽然劳动力分析似乎是人力资源部门的一个显而易见的选择，但员工可能不会有相同的观点。将一名员工浓缩成一系列数字指标会使管理过程失去人性，让员工觉得自己只不过是一个数字。

# 结论

机器学习和人工智能在人力资源方面有着广阔的应用前景。然而，从人到机器驱动的管理的转换会导致组织内员工士气的重大问题。这些技术是开创了生产力的新时代，还是将“人”从人力资源中移除？我将把那件事留给你。