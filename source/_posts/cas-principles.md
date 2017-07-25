title: CAS 原理介绍 和 实现客户端
date: 2016-6-6
tages:
- CAS
- 单点登录
- 原理
----

### 原理

[构建和实现单点登录解决方案](https://www.ibm.com/developerworks/cn/web/wa-singlesign/)
[使用 CAS 在 Tomcat 中实现单点登录](https://www.ibm.com/developerworks/cn/opensource/os-cn-cas/)

![enter image description here](https://www.ibm.com/developerworks/cn/opensource/os-cn-cas/images/image001.jpg)

>-  CAS Client 与受保护的客户端应用部署在一起，以 Filter 方式保护受保护的资源。对于访问受保护资源的每个 Web 请求，CAS Client 会分析该请求的 Http 请求中是否包含 Service Ticket，如果没有，则说明当前用户尚未登录，于是将请求重定向到指定好的 CAS Server 登录地址，并传递 Service （也就是要访问的目的资源地址），以便登录成功过后转回该地址。用户在第 3 步中输入认证信息，如果登录成功，CAS Server 随机产生一个相当长度、唯一、不可伪造的 Service Ticket，并缓存以待将来验证，之后系统自动重定向到 Service 所在地址，并为客户端浏览器设置一个 Ticket Granted Cookie（TGC），CAS Client 在拿到 Service 和新产生的 Ticket 过后，在第 5，6 步中与 CAS Server 进行身份合适，以确保 Service Ticket 的合法性。
>- 在该协议中，所有与 CAS 的交互均采用 SSL 协议，确保，ST 和 TGC 的安全性。协议工作过程中会有 2 次重定向的过程，但是 CAS Client 与 CAS Server 之间进行 Ticket 验证的过程对于用户是透明的。

另外，CAS 协议中还提供了 Proxy （代理）模式，以适应更加高级、复杂的应用场景，具体介绍可以参考 CAS 官方网站上的相关文档。

下面是一个，我觉得更清楚的版本：

![enter image description here](https://www.ibm.com/developerworks/cn/web/wa-singlesign/figure1.gif)

下面是这个身份验证协议中的主要步骤。
> 1. 用户尝试使用应用程序的 URL 访问应用程序。用户被重定向到 CAS 登录 URL，采用的是 HTTPS 连接，他请求的服务的名称作为参数传递。这时向用户显示一个用户名/密码对话框。
> 2. 用户输入 ID 和密码，CAS 对他进行身份验证。如果身份验证失败，目标应用程序根本不会知道这个用户曾经试图访问它 —— 用户在 CAS 服务器上就被拦住了。
> 3. 如果身份验证成功，CAS 就将用户重定向回目标应用程序，并在 URL 中附加一个称为 ticket 的参数。然后，CAS 尝试创建一个称为 ticket-granting cookie 的内存 cookie。这是为了以后进行自动的重新验证；如果存在这个 cookie，就表示这个用户已经成功地登录了，用户就不需要再次输入他的用户名和密码。
> 4. 然后，应用程序要检查这个 ticket 是否正确，以及是否代表一个有效用户；检查的方法是，打开一个 HTTPS 连接来调用 CAS serviceValidate URL，并作为参数传递 ticket 和服务名称。CAS 检查这个 ticket 是否有效，以及是否与请求的服务相关联。如果检查成功，CAS 就将用户名返回给应用程序。


---

我再说一个我自己的理解：

![CAS 单点登录原理](http://7xsyqy.com2.z0.glb.clouddn.com/-SSO-process.png)


---

## References

[1] [构建和实现单点登录解决方案](https://www.ibm.com/developerworks/cn/web/wa-singlesign/)
[2] [使用 CAS 在 Tomcat 中实现单点登录](https://www.ibm.com/developerworks/cn/opensource/os-cn-cas/)

