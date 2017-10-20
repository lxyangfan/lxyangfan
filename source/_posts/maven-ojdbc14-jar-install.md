title: maven安装 Oracle Jdbc Driver失败
date: 2017-10-20
----


在工程中，按如下方式加入引用：

```
		<!-- https://mvnrepository.com/artifact/com.oracle/ojdbc14 -->
		<dependency>
			<groupId>com.oracle</groupId>
			<artifactId>ojdbc14</artifactId>
			<version>10.2.0.4.0</version>
		</dependency>

```
eclipse还是提示依赖无效。经查，发现因为licences的问题，maven中央仓库并没有这个jar包。

从oracle官网下载好 ojdbc14.jar, 然后加入本地maven仓库即可。

```
mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.4.0 -Dpackaging=jar -Dfile=ojdbc.jar -DgeneratePom=true
```



