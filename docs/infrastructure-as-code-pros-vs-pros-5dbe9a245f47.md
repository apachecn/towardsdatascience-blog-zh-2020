# 基础设施即代码—优点与缺点

> 原文：<https://towardsdatascience.com/infrastructure-as-code-pros-vs-pros-5dbe9a245f47?source=collection_archive---------66----------------------->

## 行业笔记

## 构建高质量软件的基本方法

![](img/533a5fd680620edcb3f916d3d3308865.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上[科学高清](https://unsplash.com/@scienceinhd?utm_source=medium&utm_medium=referral)拍摄的照片

如今，大多数软件公司必须频繁发布产品，以消除缺陷或引入新功能。此外，如果他们有基于云的产品，他们需要定期调配和管理云服务。这些任务可以手动执行，但效率非常低。

您可以通过编写代码来供应和管理云服务。这种方法被称为代码基础设施或 IaC。在本文中，我首先描述了使用 IaC 解决方案的好处。然后，我分享我使用这种方法的经验。

IaC 方法使我们能够:

*   **再造**云服务无数，
*   **监控**云配置轻松、
*   **在开发管道中自动执行**云供应，以及
*   **选择**更灵活的云服务提供商。

我再解释一下。

# 为什么基础设施是代码？

## **—重复**

由于多种原因，您必须在开发过程中多次配置云基础架构(例如网络、安全和存储)。例如，如果一个实例在集群中关闭，您的服务将停止工作。在这种情况下，您必须重新进行云配置，并且希望与之前的配置完全一致。

## **—监控**

在 IaC 解决方案中，一切都是用人类和机器可读的语言编写的，比如 YAML 或 JSON。因此，配置文件可以在**版本控制**系统中存档和标记，以备将来使用。因此，团队领导或 CTO 可以轻松地监控或检查这种配置。请注意，您只需要监视配置文件，而不需要 IaC 解决方案创建额外的文件。

**举例。**让我们假设工程团队选择了 AWS 基础设施，并分配了几个带有 16 个 CPU 的 EC2 实例来交付产品。使用 IaC 解决方案，领导可以轻松观察 EC2 实例的类型，并防止公司花费不必要的金额。这是一个在复杂产品中非常需要的**透明度**。

## **—自动化**

您可能希望在持续集成和部署或 CI/CD 管道中巧妙地嵌入云供应步骤。不建议每次想要部署解决方案时都执行云供应步骤，尤其是在开发环境中。但是，您可能希望在产品发布渠道中包含云供应步骤，尤其是在云配置发生变化的早期。

**举例。**你想搭建舞台，发布配置完全相同的环境。但是，配置会不断变化，因为您仍然不确定许多细节。您可以使用 IaC 解决方案来确保拥有相同的环境。另外，你对 YAML 文件做了一些修改，服务停止工作。您有一个截止日期，没有时间调试。您只需要将它回滚到过去的某个功能点。借助 IaC 解决方案，您可以访问以前的云配置。

## —灵活性

如果你通过使用所有的本地技术栈将自己锁定在一个云服务提供商身上，这将是非常昂贵的。云服务提供商的本地技术堆栈可能与其对手不兼容。因此，您可能无法轻松地迁移到其他服务，这可能会导致无法负担每月的账单。

# 二。我使用 IaC 的体验如何？

在我最近的经历中，我负责构建和管理 CI/CD 管道。我与产品经理密切合作发布产品。没有 IaC 解决方案，我无法交付任务。在这里，我想分享一下我的经历。

## 将开发局限于某个特定的供应商是很昂贵的。

在早期，我们获得了价值几千美元的信用额度来使用 AWS。我们可以开始使用所有 AWS 技术栈来开发我们的解决方案。然而，与许多同行相反，我认为应该是供应商不可知的，即使该供应商是亚马逊。

如果我们将自己锁定在一个供应商身上，我们将无法控制每月的账单，并且我们不能轻易将其最小化。例如，如果我们收到使用其他云服务的信用，我们将服务迁移到新主机就不容易了。所以，我选择了 [Terraform](https://www.terraform.io/) 而不是 [CloudFormation](https://aws.amazon.com/cloudformation/) 来配置更灵活的云基础设施。

请注意，我无意在本文中详细描述 CloudFormation vs Terraform 的优缺点。

## **甚至 AWS EC2 实例也可能永久关闭。**

在我们在 AWS 上设置云服务几周后，我们收到了一封来自 Amazon 的电子邮件，称集群中的一个 EC2 实例由于硬件问题将被永久关闭。我们在一张 JIRA 卡片上注意到了这个问题，并把它放在了我们的待办事项中，但它很容易被我们忽略。

在一个美丽的星期一，我们的云服务突然遇到了一个不寻常的错误。知道我们有一个交付的最后期限，它就不再那么漂亮了！经过调查，我们发现该错误是由于 EC2 实例关闭引起的。多亏了 Terraform，我们能够快速可靠地重建 EC2 集群。

## 阶段和发布环境必须完全相同。

当一些客户开始定期使用我们的解决方案时，我们将 stage 环境添加到我们的开发工作流中。阶段环境降低了在发布中失败或遇到意外行为的风险。

我们必须确信阶段和发布环境总是相同的。即使是很小的差异也可能导致失败。使用 IaC 方法是构建相同开发环境的最佳实践。所以，我们也用了它。

## 我们不得不多次配置云基础设施。

在早期，我们只有一个单一的开发环境。因此，我们没有想到 IaC 解决方案的必要性。然而，我们到达了一个点，我们有三个开发环境:开发、阶段和发布。因此，我们必须配置比以前多三倍的云基础架构。

另外，我们不知道每个环境需要什么样的云配置。因此，我们必须进行实验来找到最佳配置。显然，如果没有 IaC 解决方案，我们不可能进行这些实验。

## **我们每次都需要将一个文件复制到 EC2 实例中。**

在开发过程中的某个时候，我们决定将 DockerHub 帐户设为私有。为了确保 CI/CD 管道顺利工作，我们必须存储帐户凭证，并在需要时检索它们。

为了遵循最佳实践，我们应该在 AWS secret manager 之类的密码库中存储凭证。由于我们有一个确定的截止日期，并且我们想对公众关闭我们的 DockerHub 帐户，我们选择了一个更简单的方法。我们设法在 EC2 实例的云供应阶段存储凭证文件。这不是最好的方法，但至少相对提高了安全性。

## **不**公司对一切都有行业标准。

我们必须尽可能快地发展。我们有竞争对手，我们希望远远领先于他们。因此，我们总是使用能为我们提供更好用户体验的解决方案。例如，我们发现 Terraform 与它的替代品相比，为我们提供了:

*   一种对人类友好的开发语言，
*   写得非常好和更新的文件，和
*   易于理解的开发管道。

像亚马逊这样的公司对所有的云服务都有自己的解决方案；然而，他们不一定是最好的或最受欢迎的。例如，AWS 的 IaC 解决方案有 [CloudFormation](https://aws.amazon.com/cloudformation/) ，但 [Terraform](https://www.terraform.io/) 正在成为这种背景下的领先解决方案。

# 临终遗言

我所有的经历只是让我对基础设施如代码或 IaC 解决方案更感兴趣；尤其是 Terraform。您可能不需要以高级方式使用 IaC 解决方案。但是，开始使用这种方法来逐步解决您的挑战和需求是非常重要的。如果你开始使用这种方法，你一定会喜欢它。

# 感谢阅读！

如果你喜欢这个帖子，想支持我…

*   *跟我上* [*中*](https://medium.com/@pedram-ataee) *！*
*   *在* [*亚马逊*](https://www.amazon.com/Pedram-Ataee/e/B08D6J3WNW) *上查看我的书！*
*   *成为* [*中的一员*](https://pedram-ataee.medium.com/membership) *！*
*   *连接上*[*Linkedin*](https://www.linkedin.com/in/pedrama/)*！*
*   *关注我的* [*推特*](https://twitter.com/pedram_ataee) *！*

[](https://pedram-ataee.medium.com/membership) [## 通过我的推荐链接加入 Medium—Pedram Ataee 博士

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

pedram-ataee.medium.com](https://pedram-ataee.medium.com/membership)