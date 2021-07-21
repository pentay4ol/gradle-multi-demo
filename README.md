## gradle 多模块

**特别提示：项目在windows下编译的时候需要放在C盘，放到其他盘符会出现`build cache fail`的异常** 

### 1. 设置

- 创建项目名称 `mkdir demo && cd demo`
- 根目录下创建文件 `settings.gradle`
- 根目录下创建目录 `mkdir -p app/src/main/java && mkdir -p core/src/main/java`

#### 1.1 `settings.gradle`中指定子模块

```
include 'app'
include 'core'
```

#### 1.2 根目录下`build.gradle`

```
subprojects {
    apply plugin: 'java'
    apply plugin: 'application'
}
```
设定插件，`application`会提供`gradle build && gradle run`之类的命令

#### 1.3 子模块`app/build.gradle`

```
//指定依赖模块
dependencies {
    implementation  project(':core')
}
// jar {
//     manifest {
//         attributes 'Main-Class': 'cn.myo.app.MainClass'
//     }
// }

//指定main函数
application {
    mainClass = 'cn.myo.app.MainClass'
}
```
#### 1.4 执行测试
```
gradle clean && gradle :app:run
```
