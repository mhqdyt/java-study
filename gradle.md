1，Gradle是什么？
===
  * 它不是已开发项目的，还是用来对项目进行构建的。而是，Gradle是软件项目构建工具。可以非常简单地对项目进行编译，测试，打包，发布等。
  * Gradle是一个自动化的项目内置工具，它只是提供了一个整合项目的框架，真正推动的是Plugin
  * 插件向工程添加属性和任务（任务），这些任务顺序执行为开发者构建项目Gradle通常使用Groovy或Java语言编写的脚本
  1，是个自动化重建工具
  2，有核心的概念插件任务属性项目
  3，使用Groovy 
  编写脚本4，方便打包js文件
  5，支持微服务
  6，把软件工程搬到建造中
  7，把建立个人的需求搬到建造中
  8，gradle包装器
2.建立自己的gradle项目
===
  标志性的文件就是build.gradle 
  提供了替换的文件目录结构
  src / main / java java业务代码
  src / test / java java测试代码
  * 创建一个Java工程，包括一个src / main / java文件夹和一个build.gradle文件。Java源文件放在src / main / java中。build.gradle只有一条语句：apply plugin：'java'，说明要使用Java插件。
打开命令窗口，命令切换切换到该工程下，执行命令gradle build 
你就会看到Gradle为你做的构造了
在build.gradle配置文件中加入以下代码
---
  插件{
    ID ' Java的'   //说明要使用的Java插件
  }
  version = “ 1.0 ”  //定义版本 
  sourceCompatibility = 1.8   //设置Java版本编译兼容1.8
   罐{
       manifest {     //将Main-Class头添加到JAR文件清单中 
       属性' Main-Class '：   ' com.lsf.PrintStr '
       }
    }
  * 通过java –jar build / libs /项目名-1.0.jar运行应用程序
  两只种开发Gradle项目的方法：一种是手动，另一种是使用gradle init这个命令。
自定义任务
--
    任务你好{
    doLast {
      的println  “世界你好”
      }
   }
3，改变目录结构
===
