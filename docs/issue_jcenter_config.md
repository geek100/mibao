Android资源库发布JCenter配置及使用
-----
###### 1.去jcenter官网注册个账号：https://bintray.com
###### 2.在项目根目录的build.gradle(Project)添加如下配置
```gradle
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.7.1'
classpath 'com.github.dcendents:android-maven-gradle-plugin:1.5'
```
###### 3.在local.properties中添加jcenter的user和apikey
```text
bintray.user=jcenter用户名
bintray.apikey=jcenter API key
```
###### 4.在gradle.properties中添加如下配置
```text
#上传的构件的Group
PROJ_GROUP=组名(com.xxxx)
#此次上传构件的版本
PROJ_VERSION=1.0.0
#上传到你bintray的maven仓库的仓库名，即他会在你的maven仓库中新建一个子仓库，并使用这个值作为仓库名
PROJ_NAME=工程项目名称
#工程网站的url，一般为你的Github项目地址
PROJ_WEBSITEURL=工程项目在github中的地址
#项目版本控制系统的url
PROJ_VCSURL=工程项目在github中的git地址
#项目描述
PROJ_DESCRIPTION=Android项目开发框架——RxBasicFun项目基础配置、组件及各种基类
#构件ID，如如compile 'com.android.support:appcompat-v7:22.2.0'中的appcompat-v7
PROJ_ARTIFACTID=basicfun
#项目包名
PROJ_PACKAGE_NAME=要上传modle的包名
#LICENSE_NAME和LICENSE_URL保持不变即可
LICENSE_NAME='The Apache Software License, Version 2.0'
LICENSE_URL='http://www.apache.org/licenses/LICENSE-2.0.txt'
DEVELOPER_ID=开发者唯一标识
DEVELOPER_NAME=开发者姓名
DEVELOPER_EMAIL=开发者邮箱
```
###### 5.在要上传的module目录下新建文件bintray.gradle,内容如下
```text
apply plugin: 'com.github.dcendents.android-maven'
apply plugin: 'com.jfrog.bintray'
group = PROJ_GROUP
version = PROJ_VERSION
project.archivesBaseName = PROJ_ARTIFACTID
install {
    repositories.mavenInstaller {
        pom.artifactId = PROJ_ARTIFACTID
        pom {
            project {
                description PROJ_DESCRIPTION
                packaging 'aar'
                name PROJ_NAME
                url PROJ_WEBSITEURL
                licenses {
                    license {
                        name LICENSE_NAME
                        url LICENSE_URL
                    }
                }
                developers {
                    developer {
                        id DEVELOPER_ID
                        name DEVELOPER_NAME
                        email DEVELOPER_EMAIL
                    }
                }
                scm {
                    connection PROJ_VCSURL
                    developerConnection PROJ_VCSURL
                    url PROJ_WEBSITEURL
                }
            }
        }
    }
}
tasks.withType(Javadoc) {
    options.addStringOption('Xdoclint:none', '-quiet')
    options.addStringOption('encoding', 'UTF-8')
}
task sourcesJar(type: Jar) {
    from android.sourceSets.main.java.srcDirs
    classifier = 'sources'
}
task javadoc(type: Javadoc) {
    source = android.sourceSets.main.java.srcDirs
    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
}
task javadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
}
artifacts {
    archives javadocJar
    archives sourcesJar
}
Properties properties = new Properties()
properties.load(project.rootProject.file('local.properties').newDataInputStream())
bintray {
    user = properties.getProperty("bintray.user")
    key = properties.getProperty("bintray.apikey")
    configurations = ['archives']
    pkg {
        repo = PROJ_NAME
        name = PROJ_PACKAGE_NAME
        websiteUrl = PROJ_WEBSITEURL
        vcsUrl = PROJ_VCSURL
        licenses = ["Apache-2.0"]
        publish = true
    }
}
javadoc {
    options {
        encoding "UTF-8"
        charSet 'UTF-8'
    }
}
```
###### 6.在要上传的module的build.gradle中的最后添加apply from: 'bintray.gradle'
###### 7.如果以上都配置正确的话，最后在Android Studio的Terminal执行下面命令即可将项目发布到JCenter上
```text
./gradlew bintrayUpload
```
*发布成功后还不能直接引用，需要登录上面注册的账号进入到仓库中发布项目点击"Add to jcenter",等审核通过后才能引用;*
