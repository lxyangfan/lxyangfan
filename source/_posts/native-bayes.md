title: 朴素贝叶斯分类
date: 2017-11-10
tags:
- 机器学习
- 分类
- 算法
----

### 条件概率和贝叶斯定理

条件概率：定义在事件A发生的条件下发生事件B的概率，记为$P(A|B)$，$P(A|B)$称为事件A的后验概率。

贝叶斯定理：

$$P(A|B) = \frac{P(AB)}{P(B)} \tag{1.1} $$

其中，$P(AB)$表示事件A和事件B同时发生的概率，$P(B)$表示事件B发生的概率，也被称为先验概率。

贝叶斯定理稍作变换，可以得到一个很有用的推论：

$$P(Y\_i|X) = \frac{P(XY\_i)}{P(X)} = \frac{P(Y\_i)P(X|Y\_i)}{P(X)} \tag{1.2}$$

#### 后验概率$P(Y=c\_i|\bf X) $最大意味着预期损失 $R\_{exp}$ 最小

推论${1.2}$是使用朴素贝叶斯分类的理论依据：

这里，设 $\bf X=\\{\rm X\_{1},..., \rm X\_{n}\\}$ 为 $n$ 个训练数据，每条训练数据 $\rm X\_{i}$ 包括 $m$ 个特征， $\rm X\_{i} = \\{x\_{i}^{1},...,x\_{i}^{m}\\}$。$Y=c\_i$为预测结果（如分类的结果）。$P(Y=c\_i|\bf X)$表示在训练数据为 $\bf X$ 的条件下，分类结果为 $c\_i$ 的概率。

为此，我们只需得到这样的 $c\_i$ 作为分类的结果，使得：
$$\arg \max\_{c\_i} P(Y=c\_i|X) \tag{1.3}$$

我们的策略是最小化预期损失$R\_{exp}(f(\bf X))$，定义$0-1$损失函数：
$$L(y, f(\bf X)) = 
\left \\\{
\begin{align}
1 & , y = f(\bf X)\\\\
0 & , y \ne f(\bf X)
\end{align}
\right.
\tag{1.4}
$$

数学期望$R\_{exp}(f(\bf X))$是对联合概率分布 $P(\bf X, Y)$取的，
$$
\begin{align}
& \arg \min\_{c\_i} R\_{exp}(f(\bf X)) \\\\
 & = \arg \min\_{c\_i} \sum\_{i=1}^{n} \sum\_{j=1}^{k} P(c\_j, \rm X\_i)L(c\_j, f(\rm X\_i)) \\\\
& = \arg \min\_{c\_i} \sum\_{i=1}^{n} \sum\_{j=1}^{k} P(y \ne c\_j, \rm X\_i), \it y = f(\rm X\_i) \ne c\_j \\\\
& = \arg \min\_{c\_i} \sum\_{i=1}^{n} \sum\_{j=1}^{k} (1 - P(y = c\_j, \rm X\_i) ) \\\\
& = \arg \max\_{c\_i} \sum\_{i=1}^{n} \sum\_{j=1}^{k} P(y = c\_j, \rm X\_i)  \\\\
& = \arg \max\_{c\_i} \sum\_{i=1}^{n} \sum\_{j=1}^{k} P(c\_j | \rm X\_i) P(\rm X\_i) \\\\
& = \arg \max\_{c\_i} P(c\_j | \bf X) \\\\
\end{align}$$

因此最大化后验概率就是最小化预期损失。

### 朴素贝叶斯分类

设特征$X = (x\_1, x\_2, ..., x\_n)$，则$P(X|Y\_i) = P(x\_1,x\_2,...,x\_n|Y\_i)$。这里假设$x\_1,x\_2$都是互相独立的，这是一个很强的假设，因此称为朴素贝叶斯 (native bayes) :
$$
\begin{align}
P(X|Y\_i) = & P(x\_1,x\_2,...,x\_n|Y\_i) \\\\
 = & P(x\_1|Y\_i)P(x\_2|Y\_i)...P(x\_n|Y\_i) \\\\
 = & \prod\_{k=1}^{n} P(x\_k|Y\_i)  \tag{2.1}
\end{align}$$

$$P(Y\_i|X) = \frac{P(Y\_i)P(X|Y\_i)}{P(X)} \tag{2.2}$$

将${2.1}$代入${2.2}$，得：

$$
P(Y = c\_i|X) =  \frac{P(Y\_i)\prod\_{k=1}^{n} P(x\_k|Y\_i) }{P(X)} \tag{2.3}
$$

注意到${2.3}$中的$P(X)$对所有的分类$c\_i$都是一样的，结合$1.3$得朴素贝叶斯分类器：

$$
y = f(x) = \arg \max\_{Y\_i}  P(Y\_i)\prod\_{k=1}^{n} P(x\_k|Y\_i) \tag{2.4}
$$

对于${2.4}$, 哪些式子是从训练数据得到的，又该怎么使用这个模型？
- 训练数据得到的: $P(x\_k|Y=c\_i)$ 当分类结果为$c\_i$时出现特征$x\_k$的概率；$P(Y\_i)=P(Y=c\_i)$为所有训练数据中分类为$c\_i$的先验概率；
- 如何使用模型？对于一个新数据$\mathbf X^{j}$, 首先统计出其中包括哪些特征$\rm K = \\{x\_1,x\_3...,x\_m\\}$,计算${2.4}$时，哪些特征$x\_k$出现，则参与$\prod\_{k\in \rm K} P(x\_k|Y\_i)$

### 算法

有了${2.4}$定义的最优化问题，下面需要给出求解的算法。


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
<script type="text/javascript" async src="https://cdn.staticfile.org/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML\_HTMLorMML">
</script>
