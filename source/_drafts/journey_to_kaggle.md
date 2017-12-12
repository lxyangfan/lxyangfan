title: Kaggle之旅
date: 2017-12-06
tags:
- Kaggle
- 竞赛
----


Kaggle竞赛无需多言，上面会举办一些数据分析、预测、分类的比赛。

对于我来说，目前知道的Kaggle上面会提供：
- 竞赛题目说明，问题的定义：分类、回归还是其他问题；
- 训练数据和测试数据；

我要提供的：
- 一个训练结果文件，供kaggle评分
- 一些notebook

这篇文章会从我（小白）的角度记录如何入门kaggle，还有其中的一些数据分析的技巧（套路）。

## 从入门到”退出“

一直都听说 kaggle 上有一个titanic生存者预测的问题作为入门，今天我就来试试，地址在这[https://www.kaggle.com/c/titanic](https://www.kaggle.com/c/titanic)

kaggle 给出了问题描述和最后提交的结果文件格式，最终我们提交的是一个csv，里面包含2列，分别是id和他对应的结果(1-存活，0-死亡)。

分析：

- 2值分类问题，我知道的分类方法：Logistic回归、决策树、朴素贝叶斯分类
- 一般思路（我预想的，未经推敲验证）：
    - 第一步：获取、清洗数据，补充缺失值
    - 第二步：把玩、查看数据，使用可视化的方式查看数据潜在的规律：散点图、柱状图
    - 第三步：选择合适模型（分类方法）+ 策略
    - 第四步：验证模型结果，调参数、总结成果

这里，结合[这篇文章](https://www.kaggle.com/lxyangfan/titanic-data-science-solutions/)，工作流有如下目标：

> Workflow goals:
>- Classifying
>- Correlating 相关性，就是找出特征feature和结果之间的相关性，特征和特征之间的相关性。
>- Converting 转换数据，将文本数据转换成数值数据
>- Completing 完整性，利用相关性补充缺失值
>- Correcting 更正：分析训练数据，将其中可能的错误和异常值排除
>- Creating

> 2条最佳实践：
>- 在项目中更早的开展特征相关性分析
>- 为了可读性，使用多个图而不是覆盖图


## 开始动手

### 固定套路一：导入必要的库和训练数据

```python
## 导入必要的包
#encoding=utf-8
import pandas as pd
import numpy as np

# 画图
import matplotlib.pyplot as plt
import seaborn as sns

# 导入数据
test = pd.read_csv('data/test.csv')
train = pd.read_csv('data/train.csv')
gender = pd.read_csv('data/gender_submission.csv')

```

### 固定套路二：从描述数据开始分析

跟自己提几个问题：
- 有多少数据？多少条？
- 数据有哪些属性？多少列？这些列分别是什么类型？离散的还是连续？离散的可能哪些取值？有没有数字和非数字的组合？需不需要转换非数值型为数值型？
- 数据本身服从什么分布？怎么画图？散点图、柱状图等等

在从数据本身找特点中，主要使用如下函数：

