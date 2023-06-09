# Azure 机器学习服务—训练模型

> 原文：<https://towardsdatascience.com/azure-machine-learning-service-train-a-model-df72c6b5dc?source=collection_archive---------42----------------------->

## 第 3 部分:学习如何使用估计器训练模型的高级概念

# 摘要

到目前为止，在这一系列文章中，我已经能够简单介绍 Azure 机器学习服务(AML)的[](https://www.kaggle.com/pankaj1234/azure-machine-learning-introduction)****，并且能够运行一个简单的实验[](/azure-machine-learning-service-run-python-script-experiment-1a9b2fc1b550)**。在这篇文章中，我将介绍实验脚本的参数化，配置脚本环境、框架和依赖关系的不同方法。此外，如何在培训结束后向 AML 服务注册模型。******

> ******这篇特别的帖子摘自 Kaggle 笔记本托管— [此处](https://www.kaggle.com/pankaj1234/azure-machine-learning-model-training)。使用设置的链接来执行实验。******

******![](img/76546ec9221033cecc12240125b8852a.png)******

******[Luis J.](https://www.pexels.com/@onewayupdesigns?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 摄于 [Pexels](https://www.pexels.com/photo/star-wars-r2-d2-2085831/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)******

# ******即兴创作——简单的实验******

******在开始讨论 AML 中的数据存储和数据集管道之前，我将简要介绍一些高级配置选项，以运行前面描述的简单实验。******

## ******脚本参数******

******在[文章# 2，](/azure-machine-learning-service-run-python-script-experiment-1a9b2fc1b550)中，我讨论了使用定制 Python 脚本实现一个简单的 ML 实验，但是那个脚本文件有一个问题，它是简单的和静态的，所以我们如何改进实验的脚本，以便它可以接受一系列值并有效地训练模型？是的，答案是参数化脚本——因此在 AML 服务环境中，任何实验脚本的参数值都可以按如下方式实现:******

```
*****### .... ###*run = Run.get_context()**##Adding the parameter: regularization rate 
parser = argparse.ArgumentParser()
parser.add_argument('--reg_rate', type=float, dest='reg', default=0.01)
args=parser.parse_args()
r = args.reg**run.log("model regularization", np.float(r))*# load the data from a local file*
data = pd.read_csv('IRIS.csv')
X = data[['sepal_length', 'sepal_width','petal_length','petal_width']].values
X=StandardScaler().fit_transform(X)
Y= (data['species']).map(lambda x: 0 if x=='Iris-setosa' else (1 if x=='Iris-versicolor' else 2))*#Split data into train and test set*
X_train, X_test, Y_train, Y_test = train_test_split(X,Y, test_size=0.25, random_state=1234)*# fit the model:* ***with extra parameter***
model = LogisticRegression(***C=1/r,*** solver='lbfgs', multi_class='multinomial').fit(X_train,Y_train)Y_pred = model.predict(X_test)
accuracy = np.average(Y_test == Y_pred)
print("accuracy: " + str(accuracy))
run.log("Accuracy", np.float(accuracy))*###....###*****
```

## ******评估者 API******

******虽然**运行配置**和**脚本运行配置**允许开发人员运行基于脚本的实验来训练机器学习模型，但 AML 服务也提供了更好的抽象，将它们的功能封装到单个对象中，称为**估计器**。典型的用例是当运行配置变得太复杂而无法为某些依赖项和框架进行配置时。它可用于最常用的机器学习框架，即 Scikit-Learn、PyTorch 和 Tensorflow。******

****下面的代码实现了通用估计器类的对象来运行训练实验。`Estimator()`构造器通过使用`compute_target`参数来参数化实验执行的计算资源的引用，例如容器、VM 或本地计算。通用估计器不包括 scikit-learn 包，因此，我们需要传递参数`conda_packages`的值。另外，我们可以通过使用构造函数方法`Estimator()`的`script_params`参数来传递脚本的参数集合。****

```
**from azureml.train.estimator import Estimator
from azureml.core import Experiment
from azureml.widgets import RunDetails*# Create an estimator*
estimator = Estimator(source_directory=experiment_folder,
                      entry_script='iris_simple_experiment.py',
                      compute_target='local',
                      use_docker=False,
                      **script_params = {'--reg_rate': 0.07},**
                      conda_packages=['scikit-learn']
                      )***# COMMENTED - SKLearn as an estimator***
*#estimator = SKLearn(source_directory=experiment_folder, entry_script='iris_simple_experiment.py', compute_target='local', use_docker=False)**# Create an experiment*
experiment_name = 'iris-estimator-experiment'
experiment = Experiment(workspace = ws, name = experiment_name)*# Run the experiment based on the estimator*
run = experiment.submit(config=estimator)*# Get Run Details*
RunDetails(run).show()*# Wait to complete the experiment. In the Azure Portal we will find the experiment state as preparing --> finished.*
run.wait_for_completion(show_output=True)**
```

> ****AML SDK 包括特定于框架的 estmators 类，它允许开发人员轻松配置框架依赖关系，例如，用于 SKLearn 或 Tensorflow 或 PyTorch。代码中还有一个 SKLearn 估计器的例子(注释)。****

## ****注册模型****

****完成 ML 模型的训练后，我们必须使用它进行推理，因此，通过 AML 服务，我们可以注册模型，并在需要时使用它进行推理。****

******下载模式:**运行对象的`download_file()`或`download_files()` 方法用于将输出文件下载到本地文件系统。****

```
**# List the files generated by the experimentfor file in run.get_file_names():
     print(file)# Download a named filerun.download_file(name='outputs/model.pkl', output_file_path='model.pkl')**
```

****为了**注册**模型和相关的元数据——名称、版本、标签，我们可以编写以下内容:****

```
**from azureml.core import Modelrun.**register_model**(model_path='outputs/iris_simple_model.pkl', model_name='iris_estimator_model', tags={"Training Context":"Estimator", "Script Context":"Parameters"},
                  properties={"Accuracy":run.get_metrics()["Accuracy"]})**
```

****最后，要查看在反洗钱服务中注册的模型，可以使用以下信息****

```
**for model **in** Model.list(ws):
    print(model.name, ":", model.version)
    print("**\n**Tag List")
    for tag_name **in** model.tags:
        tag = model.tags[tag_name]
        print(tag_name, tag)
    print("**\n**Properties List")
    for prop_name **in** model.properties:
        prop = model.properties[prop_name]
        print(prop_name,prop)**Output** iris_estimator_model : 4Tag List
Training Context Estimator
Script Context ParametersProperties List
Accuracy 0.9736842105263158
IRIS_model : 1Tag List
Training context Pipeline**
```

# ****结论****

****随着这篇文章的结束，到目前为止，我们能够涵盖反洗钱服务的最基本的方面。我们能够运行一个简单的实验并训练一个 ML 模型。此外，使用 API(如运行配置、脚本运行配置和估算器)允许我们创建一个具有相关依赖关系的环境来动态运行实验，而不考虑计算环境。****

# ****接下来呢？****

****这是一系列博客帖子，包含各种 Azure 机器学习功能的详细概述，其他帖子的 URL 如下:****

*   ****帖子 1: [Azure 机器学习服务:第一部分——简介](/azure-machine-learning-service-part-1-an-introduction-739620d1127b)****
*   ****帖子 2: [Azure 机器学习服务——运行一个简单的实验](/azure-machine-learning-service-run-python-script-experiment-1a9b2fc1b550)****
*   ****岗位 3 *(这个)* : [蔚蓝机器学习服务——训练一个模型](/azure-machine-learning-service-train-a-model-df72c6b5dc)****
*   ****帖子 4: [Azure 机器学习服务——我的数据在哪里？](/azure-machine-learning-service-where-is-my-data-pjainani-86a77b93ab52)****
*   ****帖子 5: [Azure 机器学习服务——目标环境是什么？](/azure-machine-learning-service-what-is-the-target-environment-cb45d43530f2)****

> *****与我连线*[***LinkedIn***](https://www.linkedin.com/in/p-jainani/)*进一步讨论*****

# ****参考****

****[1]笔记本&代码— [Azure 机器学习—模型训练](https://www.kaggle.com/pankaj1234/azure-machine-learning-model-training)，Kaggle。[2]Azure Machine Learning—Estimator API，[*URL*](https://aka.ms/AA70rqw)
【3】[Azure 机器学习服务](https://docs.microsoft.com/en-in/azure/machine-learning/)官方文档，微软 Azure。****