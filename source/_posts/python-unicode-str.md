title: Python 中的字符编码：str,unicode，utf-8...
date: 2016-11-27
tages:
- Python
- 字符编码
- unicode
- utf-8
-----

## 介绍

Python 2.7中让人头晕的编码问题几乎是每个初学者的恶梦，今天就来扒一扒。

相关概念：
- unicode： 是一种编码标准，不涉及具体实现，实现方式有多种如 utf-8,utf-16.
- utf-8: 是unicode的一种实现，表示8位一组，貌似也是可变长度的编码方式
- ascii：大学时候就接触过，能表示英文字符128个，最简单，无法表示中文

总结一下来说，unicode是一种编码标准，可以编码包括中英文在内的所有字符集合，但是unicode在实现方式上出于节省空间的角度，有utf-8/utf-16等等实现方式。

## Python 中的字符串编码

python 2.7 是支持unicode标准，这是肯定的。具体跟字符串相关的有2个类：`str`和`unicode`,它们分别是`basestring`的子类。

既然是不同的子类，那就当然不一样。

如下：
```
s1 = 'hello'
s2 = '你好'
type(s1)    # str
type(s2)    # 还是 str

s3 = u'你好'
type(s3)    # 变成 unicode了

```

## Python 中正确使用字符串编码的姿势

- S1： 保持编码方式的统一，IDE\文件\源代码 都是utf-8的编码方式
- S2：
    - decode early, 对于是str类型的变量，使用decode('utf-8')转化成unicode
    - unicode everywhere, 过程中愉快的统一使用 unicode
    - encode last，最终结果保存到文件还是输出哪里，对unicode字符串使用encode('utf-8')保存


## 参考

[PYTHON-进阶-编码处理小结](http://wklken.me/posts/2013/08/31/python-extra-coding-intro.html)