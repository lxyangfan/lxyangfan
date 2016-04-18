
title: 工欲善其事，必先利其器—— Git + Hexo 搭建个人博客
date: 2016-4-12
tags:
- git
- hexo
- github
- blog

--------


搭建个人博客，好处很多，能分享个人经历，生活和感悟，没准还能成为网红，嘿嘿嘿……

废话不多说，首先列出来我参考的资料，在此感谢他们!

[1] [如何搭建一个独立博客——简明Github Pages与Hexo教程. http://www.jianshu.com/p/05289a4bc8b2 ](http://www.jianshu.com/p/05289a4bc8b2)
[2] [Jacman Hexo主题 wiki. https://github.com/wuchong/jacman/wiki
](https://github.com/wuchong/jacman/wiki)
[3] [Hexo博客框架官方文档. https://hexo.io/zh-cn/docs/index.html](https://hexo.io/zh-cn/docs/index.html)


---

## 安装前提

您的电脑必须安装 Git 和 Nodejs。
>* 因为需要使用git上传(push）静态网站到Github网站上；
>* Hexo博客框架需要使用nodejs才可以运行；

Github 和 git 什么关系呢？

（说给我女朋友的，可以理解为 *QQ*和 *QQ空间*之间的关系吧）

git 是一套代码管理系统，是由Linux之父Linus发明的，一种分布式源码管理系统。因为当时Linus写Linux内核的时候，就希望全世界的小伙伴一起帮他写，而他又不想架一个集中式的源码管理系统（如CVS/SVN），所以就写了一个分布式的 源码管理工具。

Github是 一个代码托管网站，程序员的facebook，社交化代码中心，很多很棒的项目（许多google codes项目都迁移到Github上，可见它多么火）。许多项目在上面开源。所以，你懂得……

Nodejs是什么鬼？

Google出品，必属精品。不解释了。简单理解就是 用javascript 写后台程序，which is based on Google chrome V8 engine。后来独立出来了，适用于 高并发，NoSql, Blabla。


[4] [官方下载 Git. https://git-scm.com/](https://git-scm.com/ )
[5] [官网下载 Nodejs. https://nodejs.org/en/](https://nodejs.org/en/)

---

## 具体安装/配置过程
[6] [使用GitHub和Hexo搭建免费静态Blog. http://wsgzao.github.io/post/hexo-guide/]( http://wsgzao.github.io/post/hexo-guide/)

参考[文章[1]](http://www.jianshu.com/p/05289a4bc8b2) ，不再赘述。这篇文章中有很好的小tips，配置Github那里就已经很详细了。

参考[文章[6]](http://wsgzao.github.io/post/hexo-guide/)，写了 部署静态网页到GitHub，很不错。

----

## 总结一下，我发布文章的过程

* 本地使用Hexo程序生成静态网站
  - `hexo g` 生成 `public`目录下面所有静态文件
  - 到 `public`目录下，拷贝all files 到本地代码仓库
* 使用git将 静态网站 push 到 github page上
  - `rescan` 查找代码变化
  - `stage changed`
  - `local commit` 将修改commit到本地仓库
  - `push` 将修改push到远程仓库

