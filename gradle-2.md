## 3、改变目录结构
### 一、了解Java插件的sourceSets

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
### 二、依赖和仓库
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
  
  

### 三、web项目用gradle创建
