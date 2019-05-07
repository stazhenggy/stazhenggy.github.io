---
title: BAT及各类机器学习面试整理
date: 2019-04-10 12:00:00
tags: 
categories: machine learning
top: true
mathjax: true
---

写在前面：
1 本文的内容部分来源于七月在线发布的BAT机器学习面试1000题系列。 部分是自己面试其他公司时被问到的一些其他问题。剩余是自己在平时思考整理的一些内容。 定期复习，定期检查自己对于一些算法的理解。 遇到好的内容，也会不断迭代更新。

<!--more-->

2 部分摘抄自其它的博客的内容，都在后面全部跟上了链接。 

## 简要介绍下SVM(进阶->手推SVM)

分类算法。 目标是确定一个分类超平面，从而将不同的数据分隔开。

支持向量机学习方法包括构建由简至繁的模型：线性可分支持向量机、线性支持向量机及非线性支持向量机。当训练数据线性可分时，通过硬间隔最大化，学习一个线性的分类器，即线性可分支持向量机，又称为硬间隔支持向量机；当训练数据近似线性可分时，通过软间隔最大化，也学习一个线性的分类器，即线性支持向量机，又称为软间隔支持向量机；当训练数据线性不可分时，通过使用核技巧及软间隔最大化，学习非线性支持向量机。

**SVM经典博客**

+ [支持向量机通俗导论(理解SVM的三层境界)](https://www.cnblogs.com/v-July-v/archive/2012/06/01/2539022.html)
+ [机器学习之深入理解SVM](https://blog.csdn.net/sinat_35512245/article/details/54984251)

## 在k-means或kNN，我们常用欧氏距离来计算最近的邻居之间的距离，有时也用曼哈顿距离，请对比下这两种距离的差别【中】

欧氏距离，最常见的两点之间或多点之间的距离表示法，又称之为欧几里得度量，它定义于欧几里得空间中，如点$x = (x_1,\cdots,x_n)$ 和 $y = (y_1,\cdots,y_n)$ 之间的距离为：

$$De_{xy} = \sqrt{(x_1 - y_1)^{2} + (x_1 - y_1)^{2} + \cdots + (x_n -y_n)^{2}} = \sqrt{\sum_{i = 1}^{n}{(x_i - y_i)^{2}}}$$

曼哈顿距离，我们可以定义曼哈顿距离的正式意义为L1-距离或城市区块距离，也就是在欧几里得空间的固定直角坐标系上两点所形成的线段对轴产生的投影的距离总和。例如在平面上，坐标$(x_1, y_1)$的点$P_1$与坐标$(x_2, y_2)$的点$P_2$的曼哈顿距离为:

$$Dm_{xy} = |x_1 - x_2| + |y_1 - y_2|$$

要注意的是，曼哈顿距离依赖座标系统的转度，而非系统在座标轴上的平移或映射。

通俗来讲，想象你在曼哈顿要从一个十字路口开车到另外一个十字路口，驾驶距离是两点间的直线距离吗？显然不是，除非你能穿越大楼。而实际驾驶距离就是这个“曼哈顿距离”，这也是曼哈顿距离名称的来源， 同时，曼哈顿距离也称为城市街区距离(City Block distance)。

此外，欧几里得以及曼哈顿距离都是$L_p$距离的特例。 点$x = (x_1,\cdots,x_n)$ 和 $y = (y_1,\cdots,y_n)$ 的$L_p$距离为

$$Dl_{xy} = ((x_1 - y_1)^{p} + (x_1 - y_1)^{p} + \cdots + (x_n -y_n)^{p})^{\frac{1}{p}}$$

**相关内容**

+ [KNN,距离度量](https://blog.csdn.net/v_july_v/article/details/8203674)

## LR 【难】

@rickjin：把LR从头到脚都给讲一遍。建模，现场数学推导，每种解法的原理，正则化，LR和maxent模型啥关系，lr为啥比线性回归好。有不少会背答案的人，问逻辑细节就糊涂了。原理都会? 那就问工程，并行化怎么做，有几种并行化方式，读过哪些开源的实现。还会，那就准备收了吧，顺便逼问LR模型发展历史。

+ [LR前世今生](https://blog.csdn.net/cyh_24/article/details/50359055)
+ [机器学习之logistic回归](https://blog.csdn.net/sinat_35512245/article/details/54881672)

## LR和SVM的联系与区别

@朝阳在望，联系：

1 LR和SVM都可以处理分类问题，且一般都用于处理线性二分类问题（在改进的情况下可以处理多分类问题）
2 两个方法都可以增加不同的正则化项，如l1、l2等等。所以在很多实验中，两种算法的结果是很接近的。

区别： 
1 LR是参数模型，SVM是非参数模型。 
2 从目标函数来看，区别在于逻辑回归采用的是logistical loss，SVM采用的是hinge loss.这两个损失函数的目的都是增加对分类影响较大的数据点的权重，减少与分类关系较小的数据点的权重。 
3 SVM的处理方法是只考虑support vectors，也就是和分类最相关的少数点，去学习分类器。而逻辑回归通过非线性映射，大大减小了离分类平面较远的点的权重，相对提升了与分类最相关的数据点的权重。 
4 逻辑回归相对来说模型更简单，好理解，特别是大规模线性分类时比较方便。而SVM的理解和优化相对来说复杂一些，SVM转化为对偶问题后,分类只需要计算与少数几个支持向量的距离,这个在进行复杂核函数计算时优势很明显,能够大大简化模型和计算。 
5 logic能做的svm能做，但可能在准确率上有问题，svm能做的logic有的做不了。
6 logic给出的是概率

## GBDT和XGBoost的区别是什么

@Xijun LI：XGBoost类似于GBDT的优化版，不论是精度还是效率上都有了提升。与GBDT相比，具体的优点有
+ [机器学习算法与Python实践之LR](https://blog.csdn.net/zouxy09/article/details/20319673)

1.损失函数是用泰勒展式二项逼近，而不是像GBDT里的就是一阶导数
2.对树的结构进行了正则化约束，防止模型过度复杂，降低了过拟合的可能性
3.节点分裂的方式不同，GBDT是用的基尼系数，XGBoost是经过优化推导后的

**相关内容**

+ [集成学习内容](https://xijunlee.github.io/2017/06/03/%E9%9B%86%E6%88%90%E5%AD%A6%E4%B9%A0%E6%80%BB%E7%BB%93/)

## LR与线性回归的区别与联系【中】

@AntZ: LR工业上一般指`Logistic Regression`(逻辑回归)而不是`Linear Regression`(线性回归). `LR`在线性回归的实数范围输出值上施加`sigmoid`函数将值收敛到0~1范围, 其目标函数也因此从差平方和函数变为对数损失函数, 以提供最优化所需导数（sigmoid函数是softmax函数的二元特例, 其导数均为函数值的f*(1-f)形式）。请注意, LR往往是解决二元0/1分类问题的, 只是它和线性回归耦合太紧, 不自觉也冠了个回归的名字(马甲无处不在). 若要求多元分类,就要把sigmoid换成大名鼎鼎的softmax了。


## 决策树, Random Forest, Boosting, Adaboost, GBDT和XGBoost的区别是什么

随机森林Random Forest是一个包含多个决策树的分类器。GBDT（Gradient Boosting Decision Tree），即梯度上升决策树算法，相当于融合决策树和梯度上升boosting算法。

@Xijun LI：xgboost类似于gbdt的优化版，不论是精度还是效率上都有了提升。与gbdt相比，具体的优点有：
1.损失函数是用泰勒展式二项逼近，而不是像gbdt里的就是一阶导数
2.对树的结构进行了正则化约束，防止模型过度复杂，降低了过拟合的可能性
3.节点分裂的方式不同，gbdt是用的gini系数，xgboost是经过优化推导后的

https://xijunlee.github.io/2017/06/03/%E9%9B%86%E6%88%90%E5%AD%A6%E4%B9%A0%E6%80%BB%E7%BB%93/


## KNN中的K如何选取

KNN中的K值选取对K近邻算法的结果会产生重大影响。如李航博士的一书「统计学习方法」上所说：

+ 如果选择较小的K值，就相当于用较小的领域中的训练实例进行预测，“学习”近似误差会减小，只有与输入实例较近或相似的训练实例才会对预测结果起作用，与此同时带来的问题是“学习”的估计误差会增大，换句话说，K值的减小就意味着整体模型变得复杂，容易发生过拟合；

+ 如果选择较大的K值，就相当于用较大领域中的训练实例进行预测，其优点是可以减少学习的估计误差，但缺点是学习的近似误差会增大。这时候，与输入实例较远（不相似的）训练实例也会对预测器作用，使预测发生错误，且K值的增大就意味着整体的模型变得简单。

+ K=N，则完全不足取，因为此时无论输入实例是什么，都只是简单的预测它属于在训练实例中最多的累，模型过于简单，忽略了训练实例中大量有用信息。

在实际应用中，K值一般取一个比较小的数值，例如采用交叉验证法（简单来说，就是一部分样本做训练集，一部分做测试集）来选择最优的K值。

**相关内容**

[KNN](http://blog.csdn.net/v_july_v/article/details/8203674)

## 防止过拟合的方法 

过拟合的原因是算法的学习能力过强；一些假设条件（如样本独立同分布）可能是不成立的；训练样本过少不能对整个空间进行分布估计。 

处理方法有：

+ 早停止：如在训练中多次迭代后发现模型性能没有显著提高就停止训练。 决策树pre-pruning(cp, maxdepth, minsplit)

+ 数据集扩增：原有数据增加、原有数据加随机噪声、重采样

+ 正则化

+ 交叉验证

+ 特征选择/特征降维

## 哪些机器学习算法不需要做归一化处理

概率模型(比如树模型)不需要归一化，因为它们不关心变量的值，而是关心变量的分布和变量之间的条件概率，如决策树、rf。而像adaboost、svm、lr、KNN、KMeans之类的最优化问题就需要归一化。

@管博士：我理解归一化和标准化主要是为了使计算更方便, 比如两个变量的量纲不同, 可能一个的数值远大于另一个。 那么他们同时作为变量的时候, 可能会造成数值计算的问题，比如说求矩阵的逆可能很不精确 或者梯度下降法的收敛比较困难。 还有如果需要计算欧式距离的话可能量纲也需要调整。 


## 对于树形结构为什么不需要归一化

**数值缩放**，不影响分裂点位置。 因为第一步都是按照特征进行排序的，排序的顺序不变，那么所属的分支以及分裂点就不会有不同。对于线性模型，比如说LR，我有两个特征，一个是(0,1)的，一个是(0,10000)的，这样运用梯度下降时候，损失等高线是一个椭圆的形状，这样我想迭代到最优点，就需要很多次迭代，但是如果进行了归一化，那么等高线就是圆形的，那么SGD就会往原点迭代，需要的迭代次数较少。
另外，注意树模型是不能进行梯度下降的，因为树模型是阶跃的，阶跃点是不可导的，并且求导没意义，所以树模型（回归树）寻找最优点事通过寻找最优分裂点完成的。


## 数据归一化（或者标准化，注意归一化和标准化不同）的原因

@我愛大泡泡 能不归一化最好不归一化，之所以进行数据归一化是因为各维度的量纲不相同。而且需要看情况进行归一化。

**相关内容**

+ [数据归一化](http://blog.csdn.net/woaidapaopao/article/details/77806273)

有些模型在各维度进行了不均匀的伸缩后，最优解与原来不等价（如SVM）需要归一化。

有些模型伸缩有与原来等价，如：LR则不用归一化，但是实际中往往通过迭代求解模型参数，如果目标函数太扁（想象一下很扁的高斯模型）迭代算法会发生不收敛的情况，所以最坏进行数据归一化。

补充：其实本质是由于loss函数不同造成的，SVM用了欧拉距离，如果一个特征很大就会把其他的维度dominated。而LR可以通过权重调整使得损失函数不变。

## 请简要说说一个完整机器学习项目的流程

@寒小阳、龙心尘

**1 抽象成数学问题**

明确问题是进行机器学习的第一步。机器学习的训练过程通常都是一件非常耗时的事情，胡乱尝试时间成本是非常高的。
这里的抽象成数学问题，指的我们明确我们可以获得什么样的数据，目标是一个分类还是回归或者是聚类的问题，如果都不是的话，如果划归为其中的某类问题。

**2 获取数据**

数据决定了机器学习结果的上限，而算法只是尽可能逼近这个上限。
数据要有代表性，否则必然会过拟合。
对于分类问题，数据偏斜不能过于严重，不同类别的数据数量不要有数个数量级的差距。
对数据的量级有一个评估，多少个样本，多少个特征，可以估算出其对内存的消耗程度，判断训练过程中内存是否能够放得下。如果放不下就得考虑改进算法或者使用一些降维的技巧了。如果数据量实在太大，那就要考虑分布式了。

**3 特征预处理与特征选择**

良好的数据要能够提取出良好的特征才能真正发挥效力。
特征预处理、数据清洗是很关键的步骤，往往能够使得算法的效果和性能得到显著提高。归一化、离散化、因子化、缺失值处理、去除共线性等，数据挖掘过程中很多时间就花在它们上面。这些工作简单可复制，收益稳定可预期，是机器学习的基础必备步骤。

筛选出显著特征、摒弃非显著特征，需要机器学习工程师反复理解业务。这对很多结果有决定性的影响。特征选择好了，非常简单的算法也能得出良好、稳定的结果。这需要运用特征有效性分析的相关技术，如相关系数、卡方检验、平均互信息、条件熵、后验概率、逻辑回归权重等方法。

**4 训练模型与调优**

直到这一步才用到我们上面说的算法进行训练。现在很多算法都能够封装成黑盒供人使用。但是真正考验水平的是调整这些算法的（超）参数，使得结果变得更加优良。这需要我们对算法的原理有深入的理解。理解越深入，就越能发现问题的症结，提出良好的调优方案。

**5 模型诊断**

如何确定模型调优的方向与思路呢？这就需要对模型进行诊断的技术。

过拟合、欠拟合判断是模型诊断中至关重要的一步。常见的方法如交叉验证，绘制学习曲线等。 过拟合的基本调优思路是增加数据量，降低模型复杂度。 欠拟合的基本调优思路是提高特征数量和质量，增加模型复杂度。
误差分析也是机器学习至关重要的步骤。通过观察误差样本，全面分析误差产生误差的原因:是参数的问题还是算法选择的问题，是特征的问题还是数据本身的问题……
诊断后的模型需要进行调优，调优后的新模型需要重新进行诊断，这是一个反复迭代不断逼近的过程，需要不断地尝试， 进而达到最优状态。

**6 模型融合**

一般来说，模型融合后都能使得效果有一定提升。而且效果很好。

工程上，主要提升算法准确度的方法是分别在模型的前端（特征清洗和预处理，不同的采样模式）与后端（模型融合）上下功夫。因为他们比较标准可复制，效果比较稳定。而直接调参的工作不会很多，毕竟大量数据训练起来太慢了，而且效果难以保证。

**7 上线运行**

这一部分内容主要跟工程实现的相关性比较大。工程上是结果导向，模型在线上运行的效果直接决定模型的成败。 不单纯包括其准确程度、误差等情况，还包括其运行的速度(时间复杂度)、资源消耗程度（空间复杂度）、稳定性是否可接受。
这些工作流程主要是工程实践上总结出的一些经验。并不是每个项目都包含完整的一个流程。这里的部分只是一个指导性的说明，只有大家自己多实践，多积累项目经验，才会有自己更深刻的认识。

**机器学习算法大体步骤**

1 对于一个问题，用数学语言来描述它； 然后对应一个模型来描述这个问题

2 通过极大似然、最大后验概率或最小化分类误差等等建立模型的代价函数， 问题转化为最优化问题。 

3 求这个代价函数的最优化问题的解。 求解大体分以下几种情况：

- 代价函数存在解析解。 一般方法是对代价函数求导，找到导数为0的点即为最优解。 如果代价函数能简单求导，并且求导后为0的式子存在解析解，就可以直接得到最优参数

- 如果代价函数很难求导数，例如函数里存在隐含变量或变量间存在相互依赖的情况；或求导后为0的式子得不到解析解，就需要借助迭代算法来一步步找到最优解。 

## 逻辑斯特回归为什么要对特征进行离散化 

@严林

在工业界，很少直接将连续值作为逻辑回归模型的特征输入，而是将连续特征离散化为一系列0、1特征交给逻辑回归模型，这样做的优势有以下几点：

0. 离散特征的增加和减少都很容易，易于模型的快速迭代；

1. 稀疏向量内积乘法运算速度快，计算结果方便存储，容易扩展；

2. 离散化后的特征对异常数据有很强的鲁棒性：比如一个特征是年龄>30是1，否则0。如果特征没有离散化，一个异常数据“年龄300岁”会给模型造成很大的干扰；

3. 逻辑回归属于广义线性模型，表达能力受限；单变量离散化为N个后，每个变量有单独的权重，相当于为模型引入了非线性，能够提升模型表达能力，加大拟合；

4. 离散化后可以进行特征交叉，由M+N个变量变为M*N个变量，进一步引入非线性，提升表达能力；

5. 特征离散化后，模型会更稳定，比如如果对用户年龄离散化，20-30作为一个区间，不会因为一个用户年龄长了一岁就变成一个完全不同的人。当然处于区间相邻处的样本会刚好相反，所以怎么划分区间是门学问；

6. 特征离散化以后，起到了简化了逻辑回归模型的作用，降低了模型过拟合的风险。

李沐曾经说过：模型是使用离散特征还是连续特征，其实是一个“海量离散特征+简单模型” 同 “少量连续特征+复杂模型”的权衡。既可以离散化用线性模型，也可以用连续特征加深度学习。就看是喜欢折腾特征还是折腾模型了。通常来说，前者容易，而且可以n个人一起并行做，有成功经验；后者目前看很赞，能走多远还须拭目以待。

**相关内容**

[LR特征离散化](https://www.zhihu.com/question/31989952)


## 什么是熵 

## 熵、联合熵、条件熵、相对熵、互信息的定义

## 简单说下有监督学习和无监督学习的区别 

有监督学习：对具有标记的训练样本进行学习，以尽可能对训练样本集外的数据进行分类预测。（LR,SVM,BP,RF,GBDT）

无监督学习：对未标记的样本进行训练学习，比发现这些样本中的结构知识。(KMeans,DL)

## 协方差和相关性有什么区别

相关性是协方差的标准化格式。协方差本身很难做比较。例如：如果我们计算工资（$）和年龄（岁）的协方差，因为这两个变量有不同的度量，所以我们会得到不能做比较的不同的协方差。为了解决这个问题，我们计算相关性来得到一个介于-1和1之间的值，就可以忽略它们各自不同的度量。

## 线性分类器与非线性分类器的区别以及优劣 

如果模型是参数的线性函数，并且存在线性分类面，那么就是线性分类器，否则不是。

常见的线性分类器有：LR,贝叶斯分类，单层感知机、线性回归
常见的非线性分类器：决策树、RF、GBDT、多层感知机
SVM两种都有(看线性核还是高斯核)
线性分类器速度快、编程方便，但是可能拟合效果不会很好
非线性分类器编程复杂，但是效果拟合能力强

## 简单说说贝叶斯定理

全概率公式：$$P(A) = \sum_{i = 1}^{n}{P(A|B_i)*P(B_i)}$$

贝叶斯公式：$$P(A = a_i|B) = \frac{P(B|A = a_i)*P(A = a_i)}{\sum_{i=1}^{n}{P(B|A = a_i)*P(A = a_i)}}$$

**相关内容**

[从贝叶斯方法到贝叶斯网络](https://blog.csdn.net/v_july_v/article/details/40984699)

## 简要介绍分类决策树

决策树呈树型结构。 分类决策树是基于特征对实例进行分类的过程。 它可以认为是if-then规则的集合，也可以认为是定义在特征空间与类空间上的条件概率分布。 其主要优点是具有可读性，分类速度快。 决策树学习包含3个步骤： 特征选择，决策树的生成和决策树的剪枝。 

### 特征选择

决策树特征选择在于选取对训练数据具有分类能力的特征。 通常特征选择的准则是信息增益(ID3), 信息增益比(C4.5), 基尼系数(CART)。

### 决策树生成

ID3算法的核心是在决策树各个结点上应用信息增益准侧选择特征， 递归地构建决策树。 具体方法是：从根结点开始，对结点计算所有特征的信息增益，选择信息增益最大的特征作为结点的特征，由该特征的不同取值建立子结点； 再对子结点递归地调用以上方法，构建决策树； 直到所有特征信息增益都很小或没有特征选择为止。 最后的得到一个决策树。 C4.5与ID3的算法类似，只是使用信息增益比来选择特征。


### 决策树剪枝

决策树生成算法递归地产生决策树，直到不能再继续下去为止。 这样产生的分类树可能会存在过拟合。 过拟合的原因是由于学习时过多考虑如何提高对训练数据的准确分类，从而构建出过于复杂的分类树。 解决这个问题的方法是考虑决策树的复杂度， 对已生成的树进行简化。 这一简化过程称为剪枝。 决策树的剪枝往往通过**极小化损失函数**来实现。 剪枝算法为从叶结点开始，向上回缩至父结点。 如果回缩之后，损失函数变小或增大值小于阈值， 则剪枝，该父结点变为新的叶结点。。


## KNN中的K如何选取

+ [determining k in knn](https://discuss.analyticsvidhya.com/t/how-to-choose-the-value-of-k-in-knn-algorithm/2606)

The trick is that -- in general -- the lower the k value, the better the performance in the training set. That is to say, the better your model will capture the variability for the set of data it was trained on. You can think of it this way: k = 1 is the most overfit case for all instances. The prediction is based solely on the training sample nearest the sample provided.

The trouble is that -- even in a low dimensional, intuitive space -- this cannot (or rather, does not frequently) generalize well. On larger data sets, it is better to increase the number of neighbors to better represent the shared characteristics of the class being discriminated: some variability is acceptable but it (hopefully) generallly cancels out to best reflect the average properties of the class(es) being identified.

In general, there is no magic bullet for this problem. Sometimes, it might be obvious: plot the generalization error as a function of k. If there is an obvious elbow (rapid decrease followed by plateau) that is a good indication of an appropriately selected value for k. It means that there is a value of k "suggested" by the training data: a value that generalizes optimally without undue calculations of the class of nearest neighbors.

There is no clear analytical solution, though. Fundamentally, this is a question of how well your training data reflects your testing data and how well your training and testing data reflect the data outside of the collected samples. Let me know if you have additional questions! I'm passionate about data science and happy to refine my answer!

For a loose intuition, a low value of k corresponds to "sharp" decision boundaries in the classification space. Higher values of k correspond to "curvier" or, in the limit flat, decision boundaries. My recommendation would to make some synthetic data to get an intuition for the effect of varying k!


If you carry on going, you will eventually end up with the CV error beginning to go up again. This is because the larger you make k, the more smoothing takes place, and eventually you will smooth so much that you will get a model that under-fits the data rather than over-fitting it (make k big enough and the output will be constant regardless of the attribute values). I'd extend the plot until the CV error starts to go noticably up again, just to be sure, and then pick the k that minimizes the CV error. The bigger you make k the smoother the decision boundary and the more simple the model, so if computational expense is not an issue, I would go for a larger value of k than a smaller one, if the difference in their CV errors is negligible.

If the CV error doesn't start to rise again, that probably means the attributes are not informative (at least for that distance metric) and giving constant outputs is the best that it can do.


























### 如何确定聚类算法k-means中的k, 有几种方法并简要介绍下

+ [kmeans in r](https://uc-r.github.io/kmeans_clustering)

+ [determine k](https://www.datanovia.com/en/lessons/determining-the-optimal-number-of-clusters-3-must-know-methods/)


## 选择题

1 下面哪种不属于数据预处理的方法？ (D)
A变量代换 B离散化 C 聚集 D 估计遗漏值




## Reference 

+ [BAT机器学习面试1000题系列jianshu](https://www.jianshu.com/p/980efc8105b2)
+ [BAT机器学习面试1000题系列CSDN](https://blog.csdn.net/v_july_v/article/details/78121924)
+ [如何准备机器学习工程师的面试](https://www.zhihu.com/question/23259302)