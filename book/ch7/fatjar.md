# 利用Gradle打可执行jar包

过程比较简单,主要是将依赖一起打包到jar中 ,直接撸代码
```groovy
//基于Gradle 4.1
//pkaq.org

apply plugin: 'java'
    
def mainClassName = "Tiger"
//仓库
repositories {
    maven { url"https://repo.spring.io/libs-release" }
}
//依赖,为了确定依赖都打入jar包,这里随便添加了一个dom4j
dependencies {
    compile  "dom4j:dom4j:1.6.1"
}
//打包
task runnbaleJar(type: Jar) {
    from files(sourceSets.main.output.classesDirs)
    from configurations.runtime.asFileTree.files.collect { zipTree(it) }

    manifest {
        attributes 'Main-Class': mainClassName
    }
}
```