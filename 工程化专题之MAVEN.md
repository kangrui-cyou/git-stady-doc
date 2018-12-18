#                        *工程化专题之MAVEN*



* **认识Maven**

* **优势**

  > 约定优于配置
  >
  > 简单
  >
  > 测试支持
  >
  > 构建简单
  >
  > CI
  >
  > 插件丰富

* **下载安装**

  > [maven下载地址](https://maven.apache.org/download.cgi)

  > 安装
  >
  > 超级pom的位置：maven-model-builder-3.3.9.jar/org/apache/maven/model
  >
  > 配置MVM_HOME
  >
  >  * Windows  path
  >
  >  * Linux  .bash_profile
  >
  >  * MAVEN_OPTS（maven是java写的，所以也是可以设置启动参数的）
  >
  >  * 配置setting.xml
  >
  >    * setting.xml文件的加载顺序
  >
  >      ```python
  >      用户   --->  ./m2/settings   --->   安装目录/config/setting.xml
  >      ```
  >
  >    * 常用国内镜像
  >
  >      ```xml
  >      <mirror>  
  >        <id>alimaven</id>  
  >        <name>aliyun maven</name>  
  >        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>  
  >        <mirrorOf>central</mirrorOf>          
  >      </mirror> 
  >      <mirror>
  >      	<id>ui</id>
  >      	<mirrorOf>central</mirrorOf>
  >      	<name>Human Readable Name for this Mirror.</name>
  >      	<url>http://uk.maven.org/maven2/</url>
  >      </mirror>
  >      <mirror>
  >      	<id>osc</id>
  >      	<mirrorOf>central</mirrorOf>
  >      	<url>http://maven.oschina.net/content/groups/public/</url>
  >      </mirror>
  >      <mirror>
  >      	<id>osc_thirdparty</id>
  >      	<mirrorOf>thirdparty</mirrorOf>
  >      	<url>http://maven.oschina.net/content/repositories/thirdparty/</url>
  >      </mirror>
  >      ```
  >
  >    * 
  >

  ​                
