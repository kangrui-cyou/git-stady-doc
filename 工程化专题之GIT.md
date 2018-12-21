# ***工程化专题之GIT***

###**初识**

* git：目前世界上最先进的分布式版本控制系统
* git和svn的区别
  * git分布式，svn集中式
  * git内容按元数据方式存储，svn按文件存储
  * git没有全局版本号，svn有
  * git内容完整新优于svn,因为svn版本升级后存储的其实是文件变化
  * git可以不依赖网络，去中心化
  * 等等......

###  **安装**

* 相关下载地址
  * https://git-scm.com/book/en/v2/Getting-Started-Installing-Git 
  * http://windows.github.com
  * http://mac.github.com
  *  http://git-scm.com/download/linux  
* 配置git
  * git  config  --global  user.name  'kangrui'
  * git  config  --global  user.email   'kangrui@cyou.com'
  * ssh-keygen  -t  rsa  -C  'kangrui@cyou.com'
    * 生成公私钥后拷贝公钥内容至githup

### **常用命令**

* git status 有事没事敲一敲  查看文件状态







