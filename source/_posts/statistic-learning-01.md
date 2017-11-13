title: 李航《统计学习方法》第一章读书笔记
date: 2017-11-10
tags:
- 统计学习
- 机器学习
- 算法
- 读书笔记
----

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    extensions: ["tex2jax.js"],
    jax: ["input/TeX", "output/HTML-CSS"],
    tex2jax: {
      <!--$表示行内元素，$$表示块状元素 -->
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
      processEscapes: true
    },
    "HTML-CSS": { availableFonts: ["TeX"] }
  });
</script>
<!--加载MathJax的最新文件， async表示异步加载进来 -->
<script type="text/javascript" async src="https://cdn.staticfile.org/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### 介绍

 李航《统计学习方法》是一本理论性很强的书，里面没有代码，全部介绍统计学习方法的理论知识。这本书和《Machine learning in action（机器学习实战）》结合在一起看，我觉得才有互补的效果。
 
 《实战》这本书，里面倒是全部是可执行的程序，但是往往描述了问题之后，对方法的理论分析不到位，往往看着程序不知道什么意思，为什么这样写逻辑。毕竟程序只是对算法的表达，真正思想还是背后的数学逻辑。我认为，如果对《实战》这本书加一些理论分析，反而会更完整。

### 统计学习的三要素

 模型、策略、算法 为统计学习的三要素。

#### 模型
 使用统计学习或者机器学习，首先我们需要数据，并且可以认为训练数据是具有统计规律的采样数据。如果完全随机生成的数据，完全杂乱无章的数据，我们也不能从中找出什么规律，用于预测新的特征数据了。模型正是用于描述采样数据具备的“统计规律”的。常用的模型有：感知机、朴素贝叶斯分类器、Logistic回归、神经网络、贝叶斯网络、支持向量机等等。
 
 #### 策略
 我们可以根据同一份训练数据训练不同的模型，选择最优的模型的准则又称为策略。一般的，我们希望经验风险最小化和达到结构风险最小化。经验风险是指由训练数据生成的模型，得出的结果肯定与训练数据结果越接近越好，因此可以定义如下几类损失函数：
- 0-1损失函数：
$$\mathbf L( \mathbf Y,f( \mathbf X))=
\begin{cases}
0&   \text{f(X) =  Y} \\\\
1&   \text{f(X) !=  Y}
\end{cases}$$
- 平方损失函数
$$\mathbf L( \mathbf Y,f( \mathbf X))= (\mathbf Y - f(\mathbf X ) )^2$$
- 绝对值损失函数
$$\mathbf L( \mathbf Y,f( \mathbf X))= |\mathbf Y - f(\mathbf X ) |$$
- 对数损失函数
$$\mathbf L( \mathbf Y , P(\mathbf Y|f( \mathbf X))= -\log(P(\mathbf Y|f( \mathbf X))$$

定义经验损失函数：
$$R\_{emp}=\frac{1}{N}\sum\_{i=1}^{N} L(Y_i, f(X_i))  $$

我们的策略就是最小化经验损失，这样便构造了一个最优化问题：

$$\arg\min_{w}{R\_{emp}}$$

其中 $w$ 是模型需要的参数。

通过最小化经验误差得出$w$又会产生一个问题：过拟合问题（over-fitting)，也就是说，经验误差可能为0，但是模型不能很好的预测新的特征数据。解决过拟合问题的方法，包括正则化等方法，具体以后再谈。

#### 算法

将机器学习问题转化为优化问题后，使用算法解决最优化问题。通常使用的方法包括：（随机）梯度下降（上升）法、最大似然估计法等等。

###

本文简要的介绍了统计学习的三要素，下面会结合具体的模型和例子去学习。