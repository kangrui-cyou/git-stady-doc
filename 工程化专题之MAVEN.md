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
  >


* **新建maven项目**

  * 项目结构

    ```java
    TestProjevt
    	src
    		main
    			java      //源码
    			resources //配置文件
    	test
    	pom.xml
    ```

  * pom.xml

    ```xml
    <groupId>com.cyou</groupId>
    <artfactid>功能命名</artfactid>
    <version>版本号</version>
    <packaging>打包方式 模式为jar</packaging>
    <dependencyManagement>
    	1:只能出现在父pom
        2:统一版本号
        3：声明（子pom里面用到再引用）
    </dependencyManagement>
    <Dependency>
    	1:Type 默认jar
        2:scope
        	a)complie 编译 例如 spring-core  默认
        	b)test 测试
        	c)provided 编译 例如 servlet
        	d)runtime 运行时 例如JDBC实例
        	e)system 本地一些jar 例如短信jar
        	f)依赖仲裁
        		i.最短路劲原则
        		ii.加载先后原则
        	g)exclusions
        		i.排除包
    </Dependency>
    ```


* **一般maven项目模块图**

  ```shell
  						     --------------
  						     | spring-mvc |
  						     --------------
  						     		^
  						     		|
  						     --------------
  						     | common-lib |
  						     --------------
  						     		^
  						     		|
               |--------------------->|<--------------------|
        --------------         --------------        --------------
  	  | spring-xxxx|	     | spring-jdbc|		   | spring-zzzz|
  	  --------------		 --------------	       --------------
              ^                        ^                    ^
  			|						 |                    |
  			-------------------------|---------------------
  						     --------------
  						     | spring-web |
  						     --------------
  						     		
  ```


* **生命周期**

  * --------------------------------------------------从左往右------------------------------------------------------------->

  |             clean             |                      default                       |               site               |
  | :---------------------------: | :------------------------------------------------: | :------------------------------: |
  | pre-clean\|clean\|post\|clean | prepare-package\|comlile\|compile\|install\|deploy | pre-sitr\|post-site\|site-deploy |

  * A Build Lifecycle is Made Up of Phases  (一个生命周期是包含多个Phases  )

  * A Build Phase is Made Up if Plugin Goals （一个Phase是由多个Goals组成的）

















​                