title: Apache Maven 安装和使用
date: 2018-05-11
tags:
- Maven
- 安装使用
----

### Maven 介绍



### Maven 安装

- 下载地址：`http://maven.apache.org/download.cgi`
- 解压到本地磁盘，如：`C:\Users\fan.yang\work\env\apache-maven-3.5.3`
- 设置windows环境变量：`MAVEN_HOME=C:\Users\fan.yang\work\env\apache-maven-3.5.3`
- 加入`PATH=%MAVEN_HOME%\bin;%PATH%`
- 检查 maven 是否运行正确：`mvn -v`

```
C:\Users\fan.yang>mvn -v
Apache Maven 3.5.3 (3383c37e1f9e9b3bc3df5050c29c8aff9f295297; 2018-02-25T03:49:05+08:00)
Maven home: C:\Users\fan.yang\work\env\apache-maven-3.5.3\bin\..
Java version: 1.8.0_144, vendor: Oracle Corporation
Java home: C:\JDK\jdk1.8.0_144\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"
```

### Maven 使用

#### 创建新的工程

```
# 通过 archetype 插件，去`clone`一个现成的模板，不用自己手写pom.xml; 
mvn archetype:generate 
```
运行上面的命令，如果是首次，会下载很多模板到本地；之后需要根据提示，确定模板，以及本工程的信息：groupId\artifactId\version.

```
1182: remote ->- org.apache.maven.archetypes:maven-archetype-quickstart (An archetype which contains a sample Maven project.)
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 1182:
Choose org.apache.maven.archetypes:maven-archetype-quickstart version:
1: 1.0-alpha-1
2: 1.0-alpha-2
3: 1.0-alpha-3
4: 1.0-alpha-4
5: 1.0
6: 1.1
7: 1.3
Choose a number: 7:
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-quickstart/1.3/maven-archetype-quickstart-1.3.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-quickstart/1.3/maven-archetype-quickstart-1.3.pom (1.6 kB at 4.4 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-bundles/1.3/maven-archetype-bundles-1.3.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-bundles/1.3/maven-archetype-bundles-1.3.pom (4.5 kB at 12 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/31/maven-parent-31.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/31/maven-parent-31.pom (43 kB at 84 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/apache/19/apache-19.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/apache/19/apache-19.pom (15 kB at 37 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-quickstart/1.3/maven-archetype-quickstart-1.3.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/archetypes/maven-archetype-quickstart/1.3/maven-archetype-quickstart-1.3.jar (7.0 kB at 7.7 kB/s)
Define value for property 'groupId': cn.fr4nk
Define value for property 'artifactId': test
Define value for property 'version' 1.0-SNAPSHOT: :
Define value for property 'package' cn.fr4nk: :
Confirm properties configuration:
groupId: cn.fr4nk
artifactId: test
version: 1.0-SNAPSHOT
package: cn.fr4nk
 Y: :
  Y: :
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: maven-archetype-quickstart:1.3
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: cn.fr4nk
[INFO] Parameter: artifactId, Value: test
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: cn.fr4nk
[INFO] Parameter: packageInPathFormat, Value: cn/fr4nk
[INFO] Parameter: package, Value: cn.fr4nk
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: cn.fr4nk
[INFO] Parameter: artifactId, Value: test
[INFO] Project created from Archetype in dir: C:\Users\fan.yang\work\projects\mvn\test
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 05:07 min
[INFO] Finished at: 2018-05-11T10:21:29+08:00
[INFO] ------------------------------------------------------------------------
[0m[0m
```

一路回车，加上选填的信息，就建立了一个空Java工程。

#### 编译和打包

Maven 对项目管理包括如下阶段：

>- Validate: validates that all project information is available and is correct
>- Compile: compiles the source code
>- Test: runs unit tests within a suitable framework
>- Package: packages the compiled code in its distribution format
>- Integration-test: processes the package in the integration-test environment
>- Verify: runs checks to verify that the package is valid
>- Install: installs the package in the local repository
>- Deploy: installs the final package in a remote repository


- 下载依赖： `mvn dependency:resolve`
- 编译：`mvn compile`
- 打包: `mvn package`
- 清理：`mvn clean`
- 生成eclipse 工程: `mvn eclipse:eclipse`
- 清理eclipse 工程: `mvn eclipse:clean`




