title: 朴素贝叶斯分类
date: 2017-11-10
tags:
- 机器学习
- 分类
- 算法
----

### 条件概率和贝叶斯定理

条件概率：定义在事件A发生的条件下发生事件B的概率，记为$P(A|B)$。

贝叶斯定理：

$$P(A|B) = \frac{P(AB)}{P(B)} \tag{1.1} $$

其中，$P(AB)$表示事件A和事件B同时发生的概率，$P(B)$表示事件B发生的概率，也被称为先验概率。

贝叶斯定理稍作变换，可以得到一个很有用的推论：

$$P(Y_i|X) = \frac{P(XY_i)}{P(X)} = \frac{P(Y_i)P(X|Y_i)}{P(X)} \tag{1.2}$$

这个推论是使用朴素贝叶斯分类的理论依据：

这里，设$X$为特征数据，$Y\_i$为预测结果（如分类的结果）。$P(Y\_i|X)$表示在特征数据为$X$的条件下，分类结果为$Y_i$的概率。为此，我们只需得到这样的$Y\_i$作为分类的结果，使得：
$$\arg \max_{Y_i} P(Y_i|X) \tag{1.3}$$

### 朴素贝叶斯分类

设特征$X = (x_1, x_2, ..., x_n)$，则$P(X|Y_i) = P(x_1,x_2,...,x_n|Y_i)$。这里假设$x_1,x_2$都是互相独立的，这是一个很强的假设，因此称为朴素贝叶斯 (native bayes) :
$$
\begin{align}
P(X|Y_i) = & P(x_1,x_2,...,x_n|Y_i) \\\\
 = & P(x_1|Y_i)P(x_2|Y_i)...P(x_n|Y_i) \\\\
 = & \prod_{k=1}^{n} P(x_k|Y_i)  \tag{2.1}
\end{align}$$

$$P(Y_i|X) = \frac{P(Y_i)P(X|Y_i)}{P(X)} \tag{2.2}$$

将${2.1}$代入${2.2}$，得：

$$
P(Y = c_i|X) =  \frac{P(Y_i)\prod_{k=1}^{n} P(x_k|Y_i) }{P(X)} \tag{2.3}
$$

注意到${2.3}$中的$P(X)$对所有的分类$c_i$都是一样的，结合$1.3$得朴素贝叶斯分类器：

$$
y = f(x) = \arg \max_{Y_i}  P(Y_i)\prod_{k=1}^{n} P(x_k|Y_i) \tag{2.4}
$$

对于${2.4}$, 哪些式子是从训练数据得到的，又该怎么使用这个模型？
- 训练数据得到的: $P(x_k|Y=c_i)$ 当分类结果为$c_i$时出现特征$x_k$的概率；$P(Y_i)=P(Y=c_i)$为所有训练数据中分类为$c_i$的先验概率；
- 如何使用模型？对于一个新数据$\mathbf X^{j}$, 首先统计出其中包括哪些特征$\rm K = \\{x_1,x_3...,x_m\\}$,计算${2.4}$时，哪些特征$x_k$出现，则参与$\prod_{k\in \rm K} P(x_k|Y_i)$

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
<script type="text/javascript" async src="https://cdn.staticfile.org/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
