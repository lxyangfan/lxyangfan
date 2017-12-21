title: 感知机模型
date: 2017-12-16
tags:
- 机器学习
- 算法
- 感知机
- 监督学习
- 分类
- 读书笔记
----

感知机模型是一种线性分类模型，可以用于解决2分类问题，同时它也是支持向量机SVM模型的基础。

一般不直接使用这个简单的模型，可以使用一些技巧，将原来线性不可分的问题转换成线性可分的问题，再使用它或者SVM算法。

## 问题定义

设$\chi$是定义在$R^{n}$的输入空间，分类结果$Y = \\{-1, +1\\}$。

对于$\bf x\_{i} \in \chi, i=1,...,m$ 线性可分，意味存在一个超平面$w^{T} \bf x+b=0$ （$w$,$b$均是一个$n$维列向量），使得对所有的$y\_{i}=1$有 $sign(w^{T}\bf x+b) > 0$；对所有的$y\_{i}=-1$有 $sign(w^{T}\bf x+b) > 0$。

现在已知$\chi$线性可分，我们需要根据训练数据，找到对应的超平面$w^{T}\bf x+b=0$ （求出向量$w$,$b$）。对于新的数据 $\bf x\_j$，根据$sign(w^{T}\bf x+b)$ 判断$y\_j$属于1还是-1.

$$
y\_{j} =
\begin{cases}
1&  sign(w^{T}\bf x+b) > 0 \\\\
-1&   sign(w^{T}\bf x+b) < 0
\end{cases}
$$

## 点到超平面的距离

在介绍损失函数之前，需要知道$R^{n}$维空间中，一个点$x$距离超平面$w^{T}\bf x+b=0$的距离怎么求？

超平面$w^{T}\bf x+b=0$的法向量是$w$，在超平面上任意选一点$\bf x'$,点$\bf x$距离超平面$w^{T}\bf x+b=0$的距离$h$等于向量$\vec{\bf x'x}=(\bf x-\bf x')$在$w$上投影的长度。

<img src="/assets/20171216/1.png" />

$$
h = ||(\bf x-\bf x')||\_{2} \cos \theta   \tag{2.1}
$$
其中，$\theta$是$\vec{\bf x'x}$和$w$的夹角。

$$
\cos \theta = \frac{w^{T}(\bf x-\bf x')} {||w||\_{2}||\bf x-\bf x'||\_{2}} \tag{2.1}
$$

结合$2.1$,可知，

$$
h = \frac{w^{T}(\bf x-\bf x')} {||w||\_{2}}  = \frac{|w^{T}\bf x+b|} {||w||\_{2}}  \tag{2.3}
$$

其中$||w||\_{2}$表示2范数。

> 向量的范数
> 对于向量$x=[x\_1,x\_2,...,x\_n]^T$，范数表示一种函数，意义用于表达“长度”。常见的范数有L0-范数，L1-范数，L2-范数，无穷范数，Lp-范数。
> - L0-范数: 表示向量$x$中非0元素的个数，用于表示向量的稀疏性。
> - L1-范数: 表示向量$x$元素的绝对值之和，$\sum\_i^n(|x\_i|)$
> - L2-范数: 表示向量$x$元素的平方之和的平方根，$\sqrt{\sum\_i^n(x\_i^{2})}$
> - 无穷范数: 表示向量$x$元素最大的一个，$\max (x\_i)$
> - Lp-范数: 是L2范数的扩展，${[\sum\_i^n(x\_i^{p})]}^{\frac{1}{p}}$


## 损失函数

现在的策略是最小化使用超平面$w^{T}\bf x+b=0$误分类导致的误差。这个损失函数可以表示为所有误分类的点$x\_i$，到超平面的距离之和最小。

因为误分类了$x\_i$，对于$y\_i=1$,有$sign(w^{T}\bf x\_i+b)<0$，$-y\_i(w^{T}\bf x\_i+b)>0$。
对于$y\_i=-1$,有$sign(w^{T}\bf x\_i+b)>0$，$-y(w^{T}\bf x\_i+b)>0$。

假设误分类点集合是$\it M$，那么目标要求是最小化所有错误分类点到超平面距离最小，即：
$$
\min \sum\_{\bf x\_i \in \it M} {\frac{-y\_i(w^{T}\bf x\_{i}+b)} {||w||\_2}} \tag {3.1}
$$

因为$||w||\_2$不变，所以可以定义如下损失函数:

$$
L(w, b) = \sum\_{\bf x\_i \in  \it M}  { -y\_i(w^{T}\bf x\_{i}+b)} \tag {3.2}
$$

学习的策略就是最小化损失函数，得到参数$w^{\*}, b^{\*}$:

$$
(w^{\*}, b^{\*}) = \arg \min L(w, b)  \tag {3.3}
$$

## 最优化问题：使用随机梯度下降法

假设误分类点集合是$\it M$不变，那么对于$3.3$，在$\it M$中某一点$\bf x\_i$梯度有：
$$
\nabla\_{\it w} L(w, b) = - y\_i\bf x\_i \tag {4.1}
$$

$$
\nabla\_{\it b} L(w, b) = - y\_i\tag {4.2}
$$

算法首先选取一个初始值$(w\_0,b\_0)$，然后从误分类点集合是$\it M$中选取一个点$\bf x\_i$,更新$w,b$，
$$
\begin{align}
w\_i &= w\_{i-1} + \alpha  y\_i\bf x\_i \\\\
b\_i &= b\_{i-1} + \alpha  y\_i  \tag {4.3}
\end{align}
$$

因为是最小化，所以选取负梯度方向作为迭代更新，$0 \< \alpha \le 1$称为学习率。根据新的参数$(w\_i,b\_i)$，确定错误分类的点集合$\it M$。重复迭代，直到没有误分类的点（$M$为空）。


## 参考

李航 《统计学习》

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
