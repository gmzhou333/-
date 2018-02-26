# 机器学习
# 机器学习理论（参考西瓜书）handbook
1.什么是机器学习？
 ----
  它致力于研究如何通过计算的手段，利用经验来改善自身的性能。在计算机系统中，“经验”通常以“数据”
  形式存在，因此，机器学习所研究的主要内容，是关于在计算机上从数据中产生“模型”的算法，即“学习
  算法”。有了学习算法，把经验数据提供给它，就能基于这些数据产生模型；面对新的情况时，模型就会
  给我们提供相应的判断。本书用“模型”泛指从数据中学得的结果。
  
2.学习与训练
---
  从数据中学得的模型的过程成为“学习”(learning)或“训练”(training)，这个过程通过执行某个学习算法
  来完成。训练过程中使用的数据称为训练数据，训练样本组成的集合称为“训练集”。学得模型对应了关于
  数据的某种潜在的规律，称为“假设”；这种潜在规律自身，则成为“真相”(ground-truth),学习过程就是
  找出或逼近真相。本书中有时将模型称为“学习器”(learner)。学得模型后，使用其进行预测的过程称为
  “测试”(testing)，被预测的样本被称为“测试样本”(testing sample)。
  
 
3.有监督学习(supervised learning)和无监督学习(unsupervised learning)
---
  分类和回归是前者的代表，聚类是后者的代表。
  期望学得的模型有很强的泛化能力，也就是它能很好地适用于整个样本空间。尽管训练集只是样本空间的
  一个很小的采样，训练者仍希望它能够很好地反映样本空间的特性。
  
4.机器学习的发展
---
  机器学习是人工智能研究发展到一定阶段的必然产物。二十世纪五十年代到七十年代初，赋予机器逻辑推
  理能力，机器就具有智能，称为“推理期”。二十世纪七十年代中期开始，人工智能进入了“知识期”，大量
  专家系统问世。在二十世纪八十年代，“从样例中学习”，被研究最多、应用最广，也就是广义的归纳学习，
  即从训练样例中归纳出学习结果，它涵盖了监督学习、无监督学习等。
  
  二十世纪八十年代，“从样例中学习”的一大主流是符号主义学习，其代表包括决策树和基于逻辑的学习。
  直到九十年代中期之前，“从样例中学习”的另一主流技术是基于神经网络的连接主义学习。二十世纪九十
  年代中期，“统计学习”迅速占据主流舞台，代表性技术是支持向量机以及更一般的核方法。二十一世纪初，
  连接主义卷土重来，掀起了以“深度学习”为名的热潮。深度学习，狭义地说就是“很多层”的神经网络。
  
5.过拟合和欠拟合
---
  学习器在训练集上的误差称为“训练误差”或“经验误差”，在新样本上的误差称为“泛化误差”。显然，希望得
  到泛化误差小的学习器。然而，我们事前并不知道新样本是什么样，能做到的是努力使经验误差最小化。
  我们希望，学习器能在新样本上表现得很好。当学习器对训练样本学习的太好了的时候，很可能已经把训练
  样本自身一些特点当做了潜在样本具有的一般性质，导致泛化能力下降，称为“过拟合”。
  
6.模型评估方法
---
  通常，我们可通过实验测试来对学习器的泛化误差进行评估并进而做出选择。需要使用“测试集”来测试学习
  器对新样本的判别能力，然后以测试集上的“测试误差”作为泛化误差的近似。通常我们假设测试样本也是从
  样本真实分布中独立同分布采样而得。
  
  > 实验评估方法
  
  - 有时我们只有一个包含m个样例的数据集，既要训练又要测试，怎么样才能做到呢？
  
  - 留出法(hold-out) 2/3~4/5用作训练集，余下的用于测试集保持训练集和测试集数据分布的一致性，例如
    在分类任务中至少要保持样本类别比例相似。
    
  - 交叉验证法(cross validation) 每次用k-1个子集的并集作为训练集，余下的子集作为测试集，共k次。
  
  - 留一法(leave one out) m个样本唯一划分成m个子集，一个样本作为测试集，余下的用作训练集。缺点是
    计算开销难以忍受。
    
  - 自助法(bootstrapping) 我们希望评估用D训练出的模型。但在留出法和交叉验证法保留了一部分样例用于测
    试，因此实际评估模型所使用的训练集比D小，会引入因训练样本规模不同而导致的偏差，此时可以引入自助法。
    也成可放回重复采样。每次随机从D样本中挑出一个样本，可放回重复抽取m次，得到新样本D^，有的样本会重复
    出现，有的则不会出现。这样，实际评估的模型与期望评估的模型都是用m个训练样本，而仍约有1/3的样本没有
    出现在训练集中，可用于测试。
    
  - 自助法在数据集较小、难以划分训练测试集是很有用；此外，自助法能从初始数据集中产生很多个不同的训练集，
    对集成学习等方法有很大的好处。然而，自助法产生的数据集改变了初始数据集的分布，会引入估计偏差。因此，
    在初始数据量足够时，留出法和交叉验证法更常用一些。
    
  另外，我们通常把学得模型在实际使用中遇到的数据称为测试数据，为了加以区分，模型评估与选择中用于评估测试
  的数据集常称为“验证集”(validation set)。例如，在研究对比不同算法的泛化性能时，我们用测试集上的判别效果
  来估计模型在实际使用时的泛化能力，而把训练数据另外划分为训练集和验证集，基于验证集上的性能来进行模型选择
  和调参。
  
7.性能度量
---
  - 性能度量
  
  ** 错误率与精度 
  
     分类任务中最常用的两种性能度量，既适用于二分类任务，也适用于多分类任务。错误率是样本中分类
     错误的样本数占样本总数的比率。精度则是1-错误率。
    
  
 ** 查准率、查全率与F1
  
    错误率精度虽然常用，但并不能满足所有任务需求。在二分类中，分类结果可以用“混淆矩阵”表示。
    我们经常会关心“检索的信息中有多少比例是用户感兴趣的”  “用户感兴趣的信息中有多少被检测出来”。
    
    查准率
    P = TP/(TP+FP)   
    查准率
    R = TP/(TP+FN)
    
    查准率与查全率是一对矛盾的度量。既然是相互矛盾的值，在评估模型时，用到的是F1度量，综合了查准率和查全率。
   
    F = (1+beta^2)*P*R/(beta^2*P)+R
    
    beta>1 查全率有更大影响；beta<1时查准率有更大影响；beta=1时退化为标准的F1。
  
    
 ** ROC和AUC
  
    很多学习器是为测试样本产生一个实值或预测概率，然后将这个预测值与一个分类阈值进行比较，若大于阈值则分为正
    类，否则为反类。进行学习器比较时，若一个学习器的ROC曲线被另一个学习器的曲线完全包住，则可断言后者的性能
    优于前者；若两个学习器的ROC曲线发生交叉，很难判断孰优孰劣，此时则利用AUC进行判别。
    
  ** 代价敏感错误率与代价曲线
  
    在现实任务中，不同类型的错误所造成的后果不同，前面的一些性能度量，大都隐式地假设了均等代价，并没有考虑不
    同错误会造成不同后果。在非均等代价中，我们所希望的不再是简单地最小化错误次数，而是希望最小化“总体代价”。
    
8.偏差与方差
---
  > 偏差与方差
  
    以回归任务为例，期望输出与真实标记的差别称为偏差。
    f(x;D)为训练集D上学得模型f在x上的预测输出，y_D为x的数据集中的标记，y为x的真实标记；有可能出现噪声使得
    y_D != y
    
    学习算法的期望预测为：
   >> fbar(x) = E(f(x;D))
    
    使用样本数相同的不同训练集产生的方差为：
   >> var(x) = E_D(f(x;D)-fbar(x))^2
    
    噪声为:
   >> e^2 = E_D(y_D-y)^2
    
    期望输出与真是标记的差别称为偏差：
   >> bias^2(x) = (fbar(x)-y)^2
    
    偏差度量了学习算法的期望预测与真实结果的偏离程度，即刻画了学习算法本身的拟合能力；方差度量了同样大小的
    训练集的变动所导致的学习性能的变化，即刻画了数据扰动所造成的影响；噪声则表达了在当前任务上任何学习算法
    所能达到的期望泛化误差的下界，即刻画了学习问题本身的难度。偏差-方差分解说明，泛化性能是由学习算法的能力、
    数据充分性以及学习任务本身的难度所共同决定的。给定学习任务，为了取得好的泛化性能，则需使偏差较小，即能够
    充分拟合数据，并且使方差较小，即使得数据扰动产生的影响小。
   
# 常用机器学习算法

1.线性模型
---
 - 线性模型形式简单，易于建模，系数更是可以直观解释每个属性值在预测中的重要性，有很好的解释性。均方误差是回归任务中最常用的性能度量，因此可以试图让均    方误差最小化。基于均方误差最小化来进行模型求解的方法称为“最小二乘”。
   在线性回归中，最小二乘法就是试图找到一条直线，使得所有样本到直线上的欧式距离之和最小。
    
 - 广义线性模型  y = g^{-1}(w^(T)x+b),g(.)称为联系函数。实质上已是再求取输入空间到输出空间的非线性函数映射。
  
 - 对数几率回归  
   做分类任务，找一个单调可微函数将分类任务的真是标记y与线性回归模型的预测值联系起来。考虑二分类任务，其输出标记y取值0,1区间，而线性回归模型产生的预测    值z是实值，需要把实值转化为0/1值。最理想的是“单位阶跃函数”，即若预测值z大于零就判别为正例，反之就判别为负例，预测值为零则可任意判别。然而，单位跃    阶函数并不连续，不能使用广义线性模型中，故找到一个替代函数y = 1/(1+e^{-z})，称为对数几率函数，对数几率函数是一种“Sigmoid函数”，它将z值转化为一个    接近0或1的y值。带入到联系函数，可以得到$ln(y/(1-y)) = w^{T}x+b$。两者的比值称为几率（odds）。
    
 - 对数几率回归，虽然名字是回归，但实际上却是一种分类学习方法。它无需事先假设数据分布，不仅能预测出“类别”，还可以得到近似概率预测，这对许多需利用概率    辅助决策的任务很有用。我们可以通过“极大似然法”来估计参数。
   
  - 线性判别分析(LDA)
    是一种经典的线性学习方法，LDA的思想非常朴素：给定训练样例集，设法将样例投影到一条直线上，使得同类样例的投影点
    尽可能接近、异类样例投影点尽可能远离；在对新样本进行分类时，将其投影到同样的这条直线上，再根据投影点的位置来确
    定新样本的类别。多分类LDA将样本投影到N-1维空间，N-1通常小于数据原有的属性数。于是，可以通过投影来减少样本点的
    维数，且投影过程中使用了类别信息，因此LDA也常被视为一种经典的监督降维技术。
    
    定义类内散度矩阵和类间散度矩阵S_w和S_b。
   
  - 多分类学习
    现实中常遇到多分类学习任务，有些二分类学习法可直接推广到多分类，但在更多情况下，我们基于一些基本策略，利用二分类学习器来解决多分类问题。不失一般       性，多分类学习任务的基本思路是“拆解法”，即将多分类任务拆分为若干个二分类任务求解。具体来说，先对问题进行拆分，然后为拆分出的每个二分类任务训练一个     分类器；在测试时，对这些分类器的预测结果进行集成以获得最终多分类结果。
    
2.决策树
---
 - 基于树的结构进行决策，每个测试的结果或是导出的最终结论，或是导出进一步判定的问题，其考虑范围都是在上次决策结果
   的限定范围之内。一般的，一棵决策树包含一个根节点、若干个内部节点和若干个叶节点；叶节点对应与决策结果，其他每个
   结点对应于一个测试属性；每个结点包含的样本集合根据属性测试的结果被划分到子结点中。从根节点到每个叶结点的路径对
   应了一个判定测试序列。决策树学习的目的是为了产生一颗泛化能力强，即处理未见示例能力强的决策树。
  
 - 信息熵是度量样本集合纯度最常用一种指标，信息熵值越小，则样本集合纯度越高。考虑不同结点所包含的样本数不同，给分支
   结点赋予权重，可计算出用属性a对样本集进行划分所获得的“信息增益”。一般而言，信息增益越大，则意味着使用属性a划分所
   获得的“纯度提升”越大。

 - 增益率 ：信息增益准则对可取值数目较多的属性有所偏好，为了较少这种偏好，C4.5决策树算法使用增益率来选择最优划分
   属性。C4.5是找出信息增益高于平均水平的的属性，在从中选择增益率最高的。
   
 - 基尼指数 ：CART决策树使用基尼指数来选择划分属性，选择划分后**基尼指数最小的属性**作为最优划分属性。
 
 - 剪枝处理 ：是决策树算法对付“过拟合”的主要手段，包括“预剪枝”和“后剪枝”。预剪枝是指在决策树生成过程中，对每个
   结点划分前先进行估计，若当前结点划分不能提升泛化性能，则停止划分将当前结点标记为叶节点；后剪枝是先从训练集生
   成一颗完整的决策树，然后自底向上对非叶结点进行考察，若将该结点对应的子树替换为叶结点能够提升泛化能力，则将该
   子节点替换为叶结点。
 
3.神经网络
---
 - M-P神经元模型。在这个模型中，神经元接收到n个其他神经元传递过来的信号，这些输入信号通过带权重的连接进行传递，神
   经元接收到的总输入值将与神经元的阈值比较，然后通过激活函数处理以产生神经元的输出。典型的Sigmoid函数，它可以把
   在较大范围内变化输入值挤压到（0,1）输出值范围内。
   
 - 感知机 ：有两层神经元组成，输入层接收外界输入信号后传递给输出层，输出层是M-P神经元，亦称“阈值逻辑单元”。
 
 - 学习率 ：若感知机对训练样例预测错误，则根据错误程度使用学习率进行权重调整。
 
 - 感知机不能解决非线性超平面可分的问题，需考虑使用多层功能神经元。输入层和输出层之间的称为隐含层。每层神经元与下一
   层神经元互连，神经元之间不存在同层连接，也不存在跨层连接。这样的神经网络结构通常称为“多层前馈神经网络” 。输入层
   仅接受输入信号，不进行函数处理，隐藏层和输出层对信号加工，最终结果由输出层神经元输出。 
  
 - 神经网络的学习过程 ：根据训练数据来调整神经元之间的“连接权”以及每个功能神经元的阈值；神经网络学到的东西，蕴含在
   连接权与阈值中。
 
 - 误差逆传播算法：亦称“反向传播算法”，多层网络的学习能力比单层感知机要强得多，但是训练简单感知机的学习规则却不再
   适合多层网络了，需要更强大的学习算法，也就是反向传播算法。BP算法不仅可以用于多层前馈神经网络，还可以用于其他类型
   的神经网络，例如递归神经网络。但通常说“BP网络”时，一般指用BP算法训练多层前馈神经网络。BP是一个迭代学习算法，在迭代
   的每一轮采用广义感知机学习规则对参数进行更新估计；BP算法基于梯度下降策略，以目标的负梯度方向对参数进行调整。权重
   的数学推导可以参考周老师的机器学习一书，p103页。
   
   一般来说，标准BP算法每次更新只针对一个样例，参数更新十分频繁，而且对不同样例进行更新的效果可能出现“抵消”现象。因此，
   为了达到同样的累计误差极小点，标准BP算法需要迭代更多次。累计BP算法直接针对累计误差最小化，它在读取整个训练集一遍
   之后才对参数进行更新，其参数更新的频率低得多。
   
   正是由于BP算法强大的表示能力，BP神经网络经常遭遇过拟合，其训练误差持续降低，但测试误差却有可能上升。有两种方法常
   用来缓解BP网络过拟合：早停策略和正则化策略。早停：将数据集分成训练集和验证集，训练集用来计算梯度、更新连接权和阈值
   ，验证集用来估计误差，若训练集误差降低但验证集误差升高，则停止训练，同时返回具有最小验证集误差的连接权和阈值。
   正则化：基本思想是在误差目标函数中增加一个用于描述网络复杂度的部分，例如连接权与阈值的平方和；对经验误差与网络复杂
   度这两项进行折中，常通过交叉验证法来估计。
   
 - 全局最小与局部极小：直观来看，局部极小解是参数空间中的某个点，其邻域点的误差函数不小于该点的误差函数；全局最优则是
   指参数空间中所有点的误差函数值均不小于该点的误差函数值。神经网络训练过程可看作是一个参数寻优过程，显然，我们在参数
   寻优过程中是希望找到全局最小。
    
   全局最小一定局部极小，参数空间内梯度为零的局部极小点对应的局部极小值可能存在很多个，但却只会有一个全局最小。
   
4.SVM
---




















