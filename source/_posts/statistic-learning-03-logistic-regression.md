title: 逻辑回归模型 Logistic Regression
date: 2017-11-18
tags:
- 统计学习
- 机器学习
- 算法
- 读书笔记
----

## 逻辑分布

介绍逻辑回归以前，首先介绍逻辑分布。假设一个随机变量$\bf X$ 满足逻辑分布，则 $\bf X$ 的分布函数 $F(\bf X)$为:

$$
F(\bf X) = \frac{1} {1+ e^{ \frac{-(X-u)}{r}}} \tag{1.1}
$$

## 逻辑回归模型

逻辑模型属于判断模型，即不去计算具体的$P(Y,X)$联合概率分布，而是通过$P(Y|X)$判断分类的结果。逻辑回归模型有如下假设：

$$
P(Y=1|X) = \frac{e^{W^TX}} {1+ e^{W^TX}}
\tag{2.1}
$$


$$
P(Y=0|X) = \frac{1} {1+ e^{W^TX}}
\tag{2.2}
$$

对于新的数据$X'$, 通过计算$2.1$, $2.2$取概率更大的作为分类的结果。

## 策略

设采样的数据为$X=\\{x\_{1}, ..., x\_{n}\\}$， 其中的每一条数据有$m$个维度 $x_i= \\{x^{1}\_{i},...,x^{m}\_{i}\\}$。现在根据采样数据 $X$，求逻辑回归参数 $W$。

极大似然估计法是假设$X$服从某个分布$f(X,\theta)$,通过采样数据，估计出分布$f(X,\theta)$。这里假设采样数据是独立同分布采样得出的。有一种最简单有效的参数估计方法，估计的参数在目前抽样的数据上表现最好，即使得$f(X|\theta)$的联合概率最大。设似然函数$L(\theta|x\_1,...,x\_n)$：

$$
\arg \max_\theta L(\theta|x_1,...,x_n) \tag{3.1}
$$

以上就是求逻辑回归模型参数的策略。

对于分类问题，先定义似然函数$L(W)$如下：
$$
\arg \max\_{W}L(W) = \arg P(Y|X;W) = \prod\_{i=1}^{n} P(y\_i|x\_i;W)  \tag{3.2}
$$

对于单个样本的后验概率$P(y_i|x_i;W)$，结合$2.1,2.2$,得：
$$
\begin{align}
h(x_i) &= \frac{e^{W^Tx_i}}{1+e^{W^Tx_i}} \tag{3.3} \\\\ 
P(y_i|x_i;W) &= h(x_i)^{y_i}(1-h(x_i))^{1-y_i}  \tag{3.4}
\end{align}
$$


## 算法

对$3.2$的求解，可以使用梯度下降法、随机梯度下降、共轭梯度法、牛顿法等等。这里可以参考下面引用的文章，具体暂不介绍了。To Be Continued...


----

## 参考资料

[Logistic Regression 模型简介-美团技术](https://tech.meituan.com/intro_to_logistic_regression.html)

[逻辑回归模型(Logistic Regression, LR)基础](http://www.cnblogs.com/sparkwen/p/3441197.html)

[【机器学习算法系列之二】浅析Logistic Regression](https://chenrudan.github.io/blog/2016/01/09/logisticregression.html#2.1)
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