#                        *工程化专题之MAVEN*



# **认识Maven**

# **优势**

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



# **下载安装**

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



# **新建maven项目**

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

# **一般maven项目模块图**

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

# **生命周期**

* --------------------------------------------------从左往右------------------------------------------------------------->

|             clean             |                      default                       |               site               |
| :---------------------------: | :------------------------------------------------: | :------------------------------: |
| pre-clean\|clean\|post\|clean | prepare-package\|comlile\|compile\|install\|deploy | pre-sitr\|post-site\|site-deploy |

* A Build Lifecycle is Made Up of Phases  (一个生命周期是包含多个Phases  )
* A Build Phase is Made Up if Plugin Goals （一个Phase是由多个Goals组成的）

# **版本管理**

* 1.0-SNAPSHOT
* 主版本号.次版本号.增量版本号 - 里程碑版本  （1.0.0-RELAESE）

# **常用命令**

* compile  (编译) 
* clean      (清空 删除target)
* test         (运行 juit/testNG)
* package (打包 <packaging>jar/war</packaging>)
* install     (把项目install到本地仓库)
* deploy   (发本地jar到私服)

# **插件**

* 常用插件

  * 常用插件下载地址

    * ` 
      <https://maven.apache.org/plugins/> `
    * ` <http://www.mojohaus.org/plugins.html>`

  * findbugs 静态代码检查

    ```xml
    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>findbugs-maven-plugin</artifactId>
        <version>2.5.1</version>
        <configuration>
           <threshold>High</threshold>
           <effort>Default</effort>
           <findbugsXmlOutput>true</findbugsXmlOutput>
           <!-- findbugs xml输出路径-->                                                   <findbugsXmlOutputDirectory>target/site</findbugsXmlOutputDirectory>
       </configuration>
    </plugin>
    注：运行findbugs任务前请先运行“mvn package”编译工程
    mvn findbugs:help       查看findbugs插件的帮助  
    mvn findbugs:check      检查代码是否通过findbugs检查，如果没有通过检查，检查会失败，但							检查不会生成结果报表  
    mvn findbugs:findbugs   检查代码是否通过findbugs检查，如果没有通过检查，检查不会失败，							会生成结果报表保存在target/findbugsXml.xml文件中  
    mvn findbugs:gui        检查代码并启动gui界面来查看结果  
    ```

  * versions 统一升级版本号  一般配置在父项目

    ```xml
    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>versions-maven-plugin</artifactId>
        <version>2.3</version>
    </plugin>
    第一步： mvn versions:set -DnewVersion=1.0.8
    第二步：mvn versions:commit   搞定。
    
    如果想回退：mvn versions:revert
    ```

  * source 打包源代码  (切勿对外使用，防止源码泄露)

    ```xml
    <plugin>  
        <artifactId>maven-source-plugin</artifactId>  
        <version>2.3</version>  
        <executions>  
            <execution>  
                <id>attach-sources</id>
                <phase>install</phase>  
                <goals>  
                    <goal>jar-no-fork</goal>  
                </goals>  
            </execution>  
        </executions>  
    </plugin>  
    
    ```

  * assembly 打包zip、war

    ```xml
    <!-- jar打包相关插件 -->
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-assembly-plugin</artifactId>
        <version>2.2-beta-5</version>
        <configuration>
            <descriptorRefs>
                <descriptorRef>jar-with-dependencies</descriptorRef>					</descriptorRefs>
            <archive>
                <manifest>
                    <addClasspath>true</addClasspath>					                          <mainClass>com.hc360.score.CalculateScore</mainClass>
                </manifest>
            </archive>
        </configuration>
    </plugin>
    
    配置maven的Run Configurations，Goals配置成assembly:assembly即可。
    ```

  * tomcat7

    ```xml
    <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>				
            <path>/</path> <!-- 项目访问路径 本例：localhost:9090, 如果配置的aa，则访问路径为localhost:9090/aa -->
            <port>9090</port>
            <uriEncoding>UTF-8</uriEncoding><!-- 非必需项 -->
        </configuration>
    </plugin>
    
    使用命令：mvn tomcat7:run。
    ```

# **自定义插件**

<https://maven.apache.org/guides/plugin/guide-java-plugin-development.html>（参考地址）


  * 1: 新建项目

  * 2: 修改pom  

    ```xml
    <!--第一步新建项目-->
    <!--第二步修改packaging-->
    <packaging>maven-plugin</packaging>
    ```

  * 3: 添加依赖

    ```xml
    <!--第三步添加依赖-->
    <dependencies>
        <dependency>
            <groupId>org.apache.maven</groupId>
            <artifactId>maven-plugin-api</artifactId>
            <version>3.5.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.maven.plugin-tools</groupId>
            <artifactId>maven-plugin-annotations</artifactId>
            <version>3.5</version>
            <scope>provided</scope>
         </dependency>
    </dependencies>
    
    ```

  * 4: 书写插件定义类

    ```java
    import org.apache.maven.plugin.AbstractMojo;
    import org.apache.maven.plugin.MojoExecutionException;
    import org.apache.maven.plugin.MojoFailureException;
    import org.apache.maven.plugins.annotations.LifecyclePhase;
    import org.apache.maven.plugins.annotations.Mojo;
    import org.apache.maven.plugins.annotations.Parameter;
    
    import java.util.List;
    
    /**
     * Created by kangrui on 2018/12/20.
     * @Mojo:
     *  name：goal
     *  defaultPhase:
     */
    
    @Mojo(name = "cyouedu",defaultPhase = LifecyclePhase.PACKAGE)
    public class CyouMojo extends AbstractMojo{
    
        @Parameter
        private String msg;  //自定义参数
        @Parameter
        private List<String> options;  //自定义参数
    
        @Override
        public void execute() throws MojoExecutionException, MojoFailureException {
            System.out.println("自定义插件,需继承AbstractMojo类");
            System.out.println(msg);
            System.out.println(options);
        }
    }
    ```

  * 5: 构建

    mvn install

  * 6: 在其他项目中使用及参数传递演示

    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>com.cyou</groupId>
                <artifactId>cyou-plugin</artifactId>
                <version>1.0-SNAPSHOT</version>
                <!--参数传递延时-->
                <configuration>
                	<msg>This is msg</msg>
                    <options>
                    	<option>one</option>
                        <option>two</option>
                    </options>
                </configuration>
                <!--单纯的插件引入是没有任何意义的,只能双击执行，不会参与到maven其他动作
                        需要将它挂载到phase上
                        并指定要执行的goal,可以是多个
                -->
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                        	<goal>cyouedu</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```

# **Profile**

* 使用场景 dev/test/pro
* setting.xml 家和公司两套



# 私服搭建及使用



# archetype  模版化


* 生成一个archetype

  * mvn archetype:create-from-project
  * cd /target/generated-sources/archetype
  * mvn install
* 从archetype创建项目 mvn archetype:generate -DarchetypeCatalog=local





  	




​                