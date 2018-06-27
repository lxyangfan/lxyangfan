title: Spring Boot 学习
date: 2018-06-12
tags:
- java
- Spring Boot
----

### 初识 Spring Boot

Spring Boot 使用几句话概况就是：
- 约定大于配置；
- 关注应用代码，重用现有通用的模板工程；
- TDD，测试驱动开发；

为了开发一个简单的 Hello World页面，使用Spring全家桶，我们可能需要配置 web.xml \ DispatcherServlet \ Context配置等等。但是使用Spring Boot，只需要依赖一个 "web" 的Starter工程，编写核心的 `@Controller`类，完成 url 到 方法的映射就结束了。

Spring Boot 强调约定大于配置，能减少的配置就减少；并且使用 auto-configuration自动配置；这些好处，对于熟悉 Spring 生态熟手，很友好；但是对于刚入门新手，我觉得不是很友好，入门难度高，很多地方不知道怎么配置。

> When you add Spring Boot to your application, there’s a  JAR file named spring-boot-autoconfigure that contains several configuration classes. Every one of these configuration classes is available on the application’s classpath and has the opportunity to contribute to the configuration of your application. There’s configuration for Thymeleaf, configuration for Spring Data  JPA , configuration for Spring  MVC , and configuration for dozens of other things you might or might not want to take advantage of in your Spring application.

SpringBoot 使用了 Spring 4中提供的“条件配置”功能，可以动态根据条件，去加载或者生成相关配置。





