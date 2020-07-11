# gradle
## 1、Gradle是什么？
   * 它不是用来开发项目的，而是用来对项目进行构建的。也就是说，Gradle是软件项目构建工具。可以非常简单地对项目进行编译、测试、打包、发布等。
   * Gradle是一个自动化的项目构建工具，它只是提供了一个构建项目的框架，真正起作用的是Plugin
*  Plugin向工程添加属性和任务(Task)，这些Task顺序执行为开发者构建项目
Gradle通常使用Groovy或Java语言编写构建脚本<br>

1、是个自动化构建工具<br>
2、有核心的概念 plugin task property project<br>
3、使用Groovy编写构建脚本<br>
4、方便打包js文件<br>
5、支持微服务<br>
6、把软件工程搬到构建中<br>
7、把制定个人的需求搬到构建中<br>
8、gradle包装器

## 2.建立自己的gradle项目
  标志性的文件就是build.gradle<br>
  提供了默认的文件目录结构<br>
    src/main/java java业务代码<br>
    src/test/java java测试代码<br>
    
    
   * 创建一个Java工程，包括一个src/main/java文件夹和一个build.gradle文件。Java源文件放在src/main/java中。build.gradle只有一条语句:apply plugin:’java’，说明要使用Java插件。<br>
打开命令窗口，命令提示符切换到该工程下，执行命令gradle build<br>
你就会看到Gradle为你做的构建了

 ### 在build.gradle配置文件中加入以下代码
    
  ```groovy
  plugins{
    id 'java'  //说明要使用Java插件
  }
  version="1.0" //定义版本
  sourceCompatibility=1.8  //设置Java版本编译兼容1.8
   jar{
       manifest{    //将Main-Class头添加到JAR文件清单中
         attributes 'Main-Class':  'com.lsf.PrintStr'
      }
   }

  ```
  
 *  通过java –jar build/libs/项目名-1.0.jar运行应用程序
 
  两只种构建Gradle项目的方法：一种是手动，另一种是使用gradle init 这个命令。
  
  
  #### 自定义任务
  ```groovy
    task hello{
      doLast{
        println 'hello world'
      }
    }
  
 ```
 
 ## 3、改变目录结构
### 3.1了解Java插件的sourceSets

#### 了解项目默认的项目结构
  src/main/java java业务代码<br>
  src/test/java java测试代码<br>
#### 定义新的sourceSet
在build.gradle文件完成以下配置配置
```groovy
sourceSets{
   main{
       java{   srcDirs=['mysrc']}  //指定自己创建的文件名
    }
    test{   
        java {   srcDirs=['mytest']   //指定自己创建的文件名
    }  
    
      }
}

jar{//jar的类的对象
      manifest{
	        attributes 'Main-Class' :'TestGradle'
	}

}
```

当我们执行build任务时，compileJava classes compileTestJava
### 3.2依赖和仓库
项目坐标（group、 name 、 version）<br>
例如： org.springfaremwork:spring-core:5.2.4 RELEASE<br>
依赖<br>
  任何项目都需要依赖的jar包
  
  ```grovy
    dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }
}
  ```
  
  仓库用阿里云镜像下载速度快
  ```groovy
    repositories {
    
    maven{  //阿里云镜像
        url  'http://maven.aliyun.com/nexus/content/groups/public'
    }
    mavenLocal()//本地仓库
    mavenCentral()//maven仓库
}
  ```
  ## 4.自定义任务
  * 任务类必须继承DefaultTask。指定哪个方法是任务的Action,就在哪个方法前加上@TaskAction
  * 任务类用Groovy或Java编写。使用buildSrc目录。存放在buildSrc/src/main/groovy或buildSrc/src/main/java里
  ```
  import org.gradle.api.DefaultTask
  import org.gradle.api.tasks.TaskAction
   class MyTask extends DefaultTask{
    @TaskAction
     public void start(){
        System.out.println(“hello gradle”);
     }
}

  ```
  * 加了@Input的变量是任务暴露在外面的属性。使用任务时为其注入值。
  ```
  import org.gradle.api.DefaultTask
  import org.gradle.api.tasks.TaskAction
  import org.gradle.api.tasks.Input
   class MyMailTask extends DefaultTask{
    @Input
    String username
   @TaskAction
   void send() {
      println  username
    }
}

  ```
 * 声明一个任务<br>
 `task  mymail1(type:MyMailTask){   username =‘Mary’ }`
 * 再声明一个任务<br>
 `task  mymail2(type:MyMailTask){   username =‘Tom’ }
`
### 自定义任务类的方式
* 将任务类和任务对象的定义都放在build.gradle中。
* 将任务类和任务对象的定义放在某个gradle文件中，如my.gradle中，在build.gradle中通过apply from:'my.gradle'将my.gradle包含中build.gradle中。
* 在buildSrc/src/main/java中定义任务类MyTask，在build.gradle定义任务对象
* 将任务类放在一个独立的工程中，在目标工程的build.gradle中的 buildscript{   }中配置仓库和依赖（任务类工程的依赖）。然后定义任务对象。
## 测试覆盖率
 我们测试时，需要定义测试用例，测试用例定义的如何直接决定着  你的测试效果。一般要求测试覆盖率是80%左右。
  哪些工具能帮我们计算出测试覆盖率。
  Gradle提供了jacoco插件可以帮我们计算出测试覆盖率。
  引入jacoco插件后，配置jacocoTestReport任务之后，才能使用
  jacocTestReport任务来生成测试覆盖率报告。当然，生成测试覆盖  率之前我们必须先对项目进行构建。



 




