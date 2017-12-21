title: 梯度基础概念
date: 2017-12-17
tags:
- 矩阵
- 梯度
- 读书笔记
----

在多元函数$f(\bf x), \bf x = (x\_1,...,x\_n)$中，梯度表示随$\bf x$增大，函数$f(\bf x)$增长最快的方向。负梯度则表示减少最快的方向。因此对于无约束优化问题而言，可以使用迭代的方式，每次迭代选择梯度方向（或者负梯度）来寻找极大（小）的值点。

## 梯度定义

对于$n×1$的向量$\bf x=(x\_1,...,x\_n)^{T}$,定义梯度算子$\nabla\_{\bf x}$:
$$
\nabla\_{\bf x}(\bf x) = (\frac {\partial}{\partial x\_1}, ..., \frac {\partial}{\partial x\_n})^{T} \tag {1.1}
$$

对于包含$n×1$的向量$\bf x=(x\_1,...,x\_n)^{T}$的函数$f(\bf x)$,定义梯度算子$\nabla\_{ \bf x }$:
$$
\nabla\_{\bf x}(f(\bf x)) = (\frac {\partial f(\bf x)}{\partial x\_1}, ..., \frac {\partial f(\bf x)}{\partial x\_n})^{T} \tag {1.2}
$$

如果此时$f(\bf x) = [f\_1(\bf x), f\_2(\bf x),...,f\_m(\bf x)]$, 那么此时的梯度是一个$n×m$的矩阵：
$$
\nabla\_{\bf x} f(\bf x) = 
\left[
 \begin{matrix}
   \frac {\partial f\_1(\bf x)}{\partial x\_1} & ... &  \frac {\partial f\_m(\bf x)}{\partial x\_1} \\\\
   ... & ... & ... \\\\
    \frac {\partial f\_n(\bf 1)}{\partial x\_n} & ... &   \frac {\partial f\_m(\bf x)}{\partial x\_n}
  \end{matrix}
  \right]\_{n×m} \tag {1.3}
$$

$1.3$又有1种特殊情况：

如果 $f(\bf x) = [x\_1, x\_2, ... ,  x\_n]$, 带入$1.3$，得下：
$$
\nabla\_{\bf x} f(\bf x) = 
\left[
 \begin{matrix}
  1 & 0&  ... &  0 \\\\
  0 & 1 & ... & 0 \\\\
  0 & ... & ... & 0 \\\\
   0 & ... &   ... & 1
  \end{matrix}
  \right] = I\_{n×n} \tag {1.3}
$$

得到：
$$
\nabla f(\bf x^T) = \frac{\partial \bf x^{T}}{\partial \bf x} = I\_{n×n} \tag {1.4}
$$

## 梯度计算方法

首先给出几个特殊例子：
- 假设$A$与向量$\bf x$无关，$A\bf x$ 是一个标量函数,$A \bf x = (A \bf x)^T = x^TA^T$，那么：
$$
\nabla A \bf x  =  \frac{\partial A \bf x }{\partial \bf x} =  \frac{\partial \bf x^{T}A^T}{\partial \bf x}  = A ^T
$$
- 假设$A\bf y$与向量$\bf x$无关，则
$$
\nabla f(\bf x^T A \bf y) =  \frac{\partial \bf x^{T}}{\partial \bf x} A \bf y = A \bf y
$$
- 假设$A$是与向量$\bf x = [x\_1,x\_2,...,x\_n]^T$无关的方阵$A=[a\_1,a\_2,...,a\_n]$，$\bf xA\bf x$ 是一个标量函数$\bf xA\bf x = \sum\_i^n \sum\_j^n (x\_i a\_{ij} x\_j)$，那么 $\nabla (\frac{\bf x^T A \bf x} {\bf x})$列向量的第k个分量：
$$
\begin{align}
\left [\nabla  \left (\frac{\bf x^T A \bf x} {x\_k} \right) \right]\_k = & \sum\_j^n ( a\_{kj} x\_j) + \sum\_i^n ( a\_{ik} x\_i) \\\\
= & \sum\_j^n ( a\_{kj}) \bf x + \sum\_i^n (a\_{ik} ) \bf x 
\end{align} 
$$ 所以，完整得到： $$
\nabla  \left (\frac{\bf x^T A \bf x} {\bf x} \right) = A \bf x+ A^T \bf x = (A+A^T)\bf x
$$

由上，可以归纳出如下的求梯度的法则：

- 假设向量$a$与向量$\bf x$无关的常数向量，那么：
$$
\nabla a^T \bf  x  =  \it a, \nabla a \bf x  =  \it a^T,  \nabla a f(\bf x)  =  \frac{\partial  \it f(\bf x)^T}{\partial \bf x} \it a^T, 
$$
- $$
\nabla \left ( \it f(\bf x)^T A \it f(\bf x) \right) = \frac{\partial \it f(\bf x)^T}{\partial  \bf x} (A+A^T) f(\bf x)
$$
- 其他还有乘法法则、链式法则等等请见参考资料

## 参考

[http://www.voidcn.com/article/p-ponrkmdt-xd.html](http://www.voidcn.com/article/p-ponrkmdt-xd.html)

[矩阵分析与应用].张贤达.2004

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
