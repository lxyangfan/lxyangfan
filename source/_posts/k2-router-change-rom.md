title: 斐讯 K2 路由器刷 breed 与第三方固件教程
date: 2018-01-23
tags:
- 路由器
- 科学上网
-----

## 介绍

斐讯 K2 路由器用399入手了，号称399其实做工也就一般，凑合用用。因为其可以刷机，而且可以免费兑换（K码结合APP注册返现），故而入手。

[斐讯 K2 最简单刷 breed 与第三方固件教程](https://www.jianshu.com/p/de34081c1de0)

上面的文章，我没有成功，因为我的固件版本是：22.5.11.14。按照如下论坛的方法成功刷入 breed ：

[【刷机必读】斐讯K2刷breed的安全方法及开源一键刷机脚本和终极大法【2017-04-24】](http://www.right.com.cn/forum/forum.php?mod=viewthread&tid=208820&highlight=%D6%D5%BC%AB%B4%F3%B7%A8)

其中,我把最有技术含量的东西修改好放到我的博客，就是如下代码了：

```
05 |wget -T 10 http://www.frank.cn/uploads/breed-mt7620-phicomm-psg1208.bin -O /tmp/breed.bin && [ -f /tmp/breed.bin ] && [ $(md5sum /tmp/breed.bin|cut -d ' ' -f1) = cfbc68e305b6c0da38c0bb89c47814a3  ] && mtd unlock Bootloader&&mtd -r write /tmp/breed.bin Bootloader
```
 等同于：

 ```bash
#K2能正常联网，下载breed，设置10秒超时
wget -T 10 http://www.frank.cn/uploads/breed-mt7620-phicomm-psg1208.bin -O /tmp/breed.bin

#判断是否有下载文件
if [ -f "/tmp/breed.bin" ] ;then
vmd5=`md5sum /tmp/breed.bin|cut -d ' ' -f1 `
#判断下载文件的MD5值是否正确
if [ "$vmd5" = "cfbc68e305b6c0da38c0bb89c47814a3" ] ;then
  #如果正确则开始刷写breed
  mtd unlock Bootloader
  mtd -r write /tmp/breed.bin Bootloader
fi
fi

 ```

原始文件从官网[https://breed.hackpascal.net/](https://breed.hackpascal.net/)下载的。