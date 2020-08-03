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

根据[Gradle构建扫描插件文档]( https://docs.gradle.com/enterprise/gradle-plugin/?_ga=2.41519714.1567320297.1596098791-192503258.1592536201#applying_the_plugin)，你可以在自己的项目中使用构建扫描插件。

### 1.5 接受许可协议

为了发布构架扫描到[https://scans.gradle.com](https://scans.gradle.com/?_ga=2.210497493.1567320297.1596098791-192503258.1592536201) 上，你需要接受许可协议。在发布时这一步骤可以通过命令行即时实现，但也可以通过添加一下部分在你的Gradle构建文件中实现定制化。

```groovy
gradleEnterprise {
    buildScan {
        termsOfServiceUrl = 'https://gradle.com/terms-of-service'
        termsOfServiceAgree = 'yes'
    }
}
```

在buildScan代码块中你可以配置插件，在这里你需要设置两个必要参数来接受许可协议。还有其他参数可以设置，详情请查看[构建扫描用户手册]( https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201)

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

你可以通过使用[Gradle初始化脚本](https://docs.gradle.com/enterprise/gradle-plugin/?_ga=2.214533463.1567320297.1596098791-192503258.1592536201#many-project)来避免对所有构建添加插件和许可协议。

你还可以向脚本添加其他功能，比如基于什么条件发布扫描信息。详情可见[构建扫描用户手册](https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201 )。

### 1.9 总结

在这篇指南中，你会学习到：

1. 生成一次构建扫描
2. 在线查看构建扫描信息
3. 创建一份可以使所有构建进行构建扫描的初始化脚本

### 1.10 下一步

其他信息可以在[构建扫描用户手册](https://docs.gradle.com/build-scan-plugin/?_ga=2.117539145.1567320297.1596098791-192503258.1592536201 )上面看到。

## 2.创建一个新的Gradle构建（create a new Gradle build）

不论项目类型，学习Gradle任务如何在任意项目上工作。查看可使用的任务，生成一个封装包（wrapper），从一个位置复制数据到另一个位置，添加插件，等等。

跟随以下指南，你将会创建一个小的Gradle项目，使用到一些基础的Gradle命令，并找到如何使用Gradle管理项目的感觉。

### 2.1. 需要什么

#### 2.1.1 大约11分钟

#### 2.1.2 一个终端应用

#### 2.1.3 Java环境，版本为8以上

#### 2.1.4 Gradle包，版本4.10.3以上

### 2.2 初始化一个项目

首先，创建一个新的目录用来放我们的项目。

现在我们可以使用Gradle的初始化命令来生成一个简单的项目。通过研究生成的所有文件，你会清楚到底发生了什么。

```
❯ gradle init 
Starting a Gradle Daemon (subsequent builds will be faster)

BUILD SUCCESSFUL in 3s
2 actionable tasks: 2 executed
```

命令行应该显示“BUILD SUCCESSFUL”并且生成下面的“空”项目。如果没有，请确保Gradle已经正确安装，并且你已经正确配置了JAVA_HOME环境。

以下是Gradle生成的文件以及文件夹：

```groovy
├── build.gradle  
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar  
│       └── gradle-wrapper.properties  
├── gradlew  
├── gradlew.bat  
└── settings.gradle  
```

build.gradle--该脚本是用来配置当前文件的。

gradle wrapper gradle-wrapper.jar--gradle打包可执行文件jar包

gradle wrapper gradle-wrapper.properties --gradle打包配置参数

gradlew--基于Unix系统的Gradle打包脚本

gradlew.bat--基于Windows的打包脚本

settings.gradle--配置Gradle构建的设置脚本

注意点：
gradle初始化可以生成不同类型的项目，甚至知道如何将简单的pom.xml(maven配置文件)转换成Gradle。

我们看到这里，其实已经可以结束本指南了。但如果你想知道如何在项目中使用Gradle，那就继续吧。

### 2.3 创建一个任务

Gradle通过Groovy或者基于Kotlin的DSL提供的API接口用来创建和配置任务。一个项目包含了一组任务，每个任务都有一些基础的操作。

Gradle提供了一个任务库，你可以在自己的项目中配置这些任务。比如，有一个叫做Copy的核心任务，这个任务的作用是将文件从一个位置复制到另一个位置。这个Copy任务非常有用（具体请[查看文档](https://docs.gradle.org/4.10.3/dsl/org.gradle.api.tasks.Copy.html)），但是这里，再一次，让我们保持简洁性。按以下步骤执行操作：

#### 2.3.1 创建一个src目录

#### 2.3.2 在src目录中添加名为myfile.txt的文件，文件内容随意（甚至可以为空），但是为了方便还是添加简单的“Hello World”进去吧。

#### 2.3.3 在你的build.gradle文件中，定义一个类型是Copy（注意大写字母）的任务并命名为copy，用来复制src目录到新的叫做dest的目录。（你不需要创建dest目录--任务会帮你创建的。）

build.gradle

```groovy
task copy(type: Copy, group: "Custom", description: "Copies sources to the dest directory") {
    from "src"
    into "dest"
}
```

在这里，group和description可以是任意你想写的东西。你甚至可以省略它，但是也会在之后要用到的任务报告中忽略它们。

现在执行你的新copy任务:

```
❯ ./gradlew copy
> Task :copy

BUILD SUCCESSFUL in 0s
1 actionable task: 1 executed
```

通过检查dest目录下是现在是否有一个新的叫做myfile.txt的文件，并且内容与src目录下的内容一致，来验证是否达到预期。

### 2.4 应用插件

Gradle包含一系列插件，并且在Gradle插件站点还可以找到更多的插件，发行版本中包含的插件之一是base插件。与叫做Zip的核心插件类型结合使用，你可以使用配置的名称和位置创建项目的压缩存档（zip archive）。

使用插件语句，添加base插件到你的构建脚本文件中，确保在文件顶部添加plugins{}代码块。

build.gradle

```groovy
plugins {
    id "base"
}

... rest of the build file ...
```

现在添加任务将src目录压缩存档。

build.gradle

```groovy
task zip(type: Zip, group: "Archive", description: "Archives sources in a zip file") {
    from "src"
    archiveFileName = "basic-demo-1.0.zip"
}
```

base插件使用设置在build/distributions文件夹下创建了名为basic-demo-1.0.zip的归档文件。

在这个例子中，简单运行了新的zip任务，并且按预期看到了生成的压缩文件。

```
❯ ./gradlew zip
> Task :zip

BUILD SUCCESSFUL in 0s
1 actionable task: 1 executed
```

### 2.5 查看并调试构建

让我们来看看在新项目中Gradle还能做什么。也可以查看[命令行接口全参考](https://docs.gradle.org/4.10.3/userguide/command_line_interface.html)。

#### 2.5.1 发现可使用的任务

任务命令窗口列出了可以调用的Gradle任务，包括由基础插件添加的任务，和你刚刚添加的自定义任务。

```
❯ ./gradlew tasks

> Task :tasks

------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Archive tasks
-------------
zip - Archives sources in a zip file

Build tasks
-----------
assemble - Assembles the outputs of this project.
build - Assembles and tests this project.
clean - Deletes the build directory.

Build Setup tasks
-----------------
init - Initializes a new Gradle build.
wrapper - Generates Gradle wrapper files.

Custom tasks
------------
copy - Simply copies sources to a the build directory

Help tasks
----------
buildEnvironment - Displays all buildscript dependencies declared in root project 'basic-demo'.
components - Displays the components produced by root project 'basic-demo'. [incubating]
dependencies - Displays all dependencies declared in root project 'basic-demo'.
dependencyInsight - Displays the insight into a specific dependency in root project 'basic-demo'.
dependentComponents - Displays the dependent components of components in root project 'basic-demo'. [incubating]
help - Displays a help message.
model - Displays the configuration model of root project 'basic-demo'. [incubating]
projects - Displays the sub-projects of root project 'basic-demo'.
properties - Displays the properties of root project 'basic-demo'.
tasks - Displays the tasks runnable from root project 'basic-demo'.

Verification tasks
------------------
check - Runs all checks.

Rules
-----
Pattern: clean<TaskName>: Cleans the output files of a task.
Pattern: build<ConfigurationName>: Assembles the artifacts of a configuration.
Pattern: upload<ConfigurationName>: Assembles and uploads the artifacts belonging to a configuration.

To see all tasks and more detail, run gradlew tasks --all

To see more detail about a task, run gradlew help --task <task>

BUILD SUCCESSFUL in 0s
1 actionable task: 1 executed
```

#### 2.5.2 分析和调试你的构建

Gradle也提供了丰富的，基于页面的构建查看，叫做构建扫描。（build scan）

具体可参考1.6

通过使用--scan选项或者在项目中使用构建扫描插件，你就可以免费在[scans.gradle.com](https://scans.gradle.com/?_ga=2.246928964.1574540686.1596420546-192503258.1592536201)中创建构架扫描了。发布构建扫描结果到scans.gradle.com，并将结果数据传输到Gradle的服务器上。

