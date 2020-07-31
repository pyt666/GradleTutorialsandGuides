# Gradle教程与指南

在这里你可以找到基于项目的教程以及通过使用gradle来学习它的专题指南。不管你是使用gradle的新手还是经验丰富的老手，这篇指南都可以帮助到你。
不管是一般任务，还是特定任务，下面都会一步步教你如何使用gradle来完成。

## 1. 创建构建扫描 （create build scan）

学习如何在一个gradle构建项目中使用构建扫描。添加插件和许可协议，执行一次扫描，并查看它的结果。通过一个初始化脚本，为所有构建添加构建扫描功能。

一份构建扫描是可分享的，是一次构建的核心记录。通过这份记录，我们可以洞悉发生了什么、为什么发生。在项目中应用构建扫描插件，你可以免费发布构建扫描结果到 [https://scans.gradle.com](https://scans.gradle.com/) 上。

### 1.1 创建什么

这篇指南向你展示了如何在不修改任何构建脚本的情况下即时发布自己的构建扫描。

你也可以学习如何修改一个构建脚本，使给定项目的所有构建都能进行构建扫描。

当然，你也可以修改一个初始化脚本，使你的所有项目都能构建扫描。

### 1.2 需要什么

#### 1.2.1 你自己的样例项目，或者Gradle上的示例项目

#### 1.2.2 联网

#### 1.2.3 邮箱

#### 1.2.4 6min

### 1.3 选择一个样例项目

Gradle给了一个简单的Java项目，你可以用它验证构建扫描。如果你想使用，可以克隆或者下载。

```
$ git clone https://github.com/gradle/gradle-build-scan-quickstart
Cloning into 'gradle-build-scan-quickstart'...
$ cd gradle-build-scan-quickstart
```

如果你更喜欢自己的项目，请略过这步。

### 1.4自动应用构件扫描插件

如果你是使用Gradle4.3开始的，那么在构建脚本中不需要任何额外的配置，你就可以使用构建扫描功能了。当使用命令行选项--scan来发布一次构建扫描时，所需的构建扫描插件会自动被应用。在构建结束之前，在命令行中你会被提问是否接受许可认证。下面的控制台输出具体描述了这一过程。

```
$ ./gradlew build --scan
> Task :compileJava
> Task :processResources NO-SOURCE
> Task :classes
> Task :jar
> Task :assemble
> Task :compileTestJava
> Task :processTestResources NO-SOURCE
> Task :testClasses
> Task :test
> Task :check
> Task :build

BUILD SUCCESSFUL
4 actionable tasks: 4 executed

Publishing a build scan to scans.gradle.com requires accepting the Gradle Terms of Service defined at https://gradle.com/terms-of-service. Do you accept these terms? [yes, no] yes

Gradle Terms of Service accepted.

Publishing build scan...
https://gradle.com/s/czajmbyg73t62
```

即使没有在自己的构建中配置构建扫描插件，这种机制下我们也可以轻易地进行即时的、一次性的构建扫描。如果需要细粒度配置，你可以在构建中配置构建扫描插件或者像下个章节中一样配置初始化脚本。

### 1.4 在你项目的所有构建中使用构建扫描

使用版本Gradle 2.x-5.x的用户，你需要在根构建脚本中添加 com.gradle.build-scan 插件。使用版本Gradle 6.0的用户，你需要在你的 settings 脚本中使用 com.gradle.enterprise 插件。

通过

[Gradle构建扫描插件文档]: https://docs.gradle.com/enterprise/gradle-plugin/?_ga=2.41519714.1567320297.1596098791-192503258.1592536201#applying_the_plugin	"Gradle构建扫描插件文档"

你可以在自己的项目中使用构建扫描插件。

### 1.5 接受许可协议

为了发布构架扫描到

[https://scans.gradle.com]: https://scans.gradle.com/?_ga=2.210497493.1567320297.1596098791-192503258.1592536201	"https://scans.gradle.com"

上，你需要接受许可协议。在发布时这一步骤可以通过命令行即时实现，但也可以通过添加一下部分在你的Gradle构建文件中实现定制化。

```groovy
gradleEnterprise {
    buildScan {
        termsOfServiceUrl = 'https://gradle.com/terms-of-service'
        termsOfServiceAgree = 'yes'
    }
}
```

在buildScan代码块中你可以配置插件，在这里你需要设置两个必要参数来接受许可协议。还有其他参数可以设置，详情请查看

[构建扫描用户手册]: https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201	"构建扫描用户手册"

### 1.6 发布一份构建扫描

通过使用命令行标识--scan实现一次构建扫描的发布。

运行一次 build 构建任务，并且配置 --scan选项。当构建完成，上传构建数据到scans.gradle.com上之后，会出现一个链接，你可以通过它查看自己的构件扫描。

```
$ ./gradlew build --scan

BUILD SUCCESSFUL in 0s

Publishing build scan...
https://gradle.com/s/uniqueid
```

### 1.7 在线进入构建扫描

第一次进入链接，你会被要求激活创建的构建扫描。

你收到的激活邮件类似于。。。

你现在可以构建扫描中的全部信息了，包括任务执行的时间、每次构建所需的时间、所有测试的结果、使用的插件以及其他依赖，所有命令行开关和其他更多。

### 1.8 对所有构建使能构建扫描（可选）

你可以通过使用

[Gradle初始化脚本]: https://docs.gradle.com/enterprise/gradle-plugin/?_ga=2.214533463.1567320297.1596098791-192503258.1592536201#many-projects	"Gradle初始化脚本"

来避免对所有构建添加插件和许可协议。

你还可以向脚本添加其他功能，比如基于什么条件发布扫描信息。详情可见

[构建扫描用户手册]: https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201	"构建扫描用户手册"

。

### 1.9 总结

在这篇指南中，你会学习到：

1. 生成一次构建扫描
2. 在线查看构建扫描信息
3. 创建一份可以使所有构建进行构建扫描的初始化脚本

### 1.10 下一步

其他信息可以在

[构建扫描用户手册]: https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201	"构建扫描用户手册"

上面看到。