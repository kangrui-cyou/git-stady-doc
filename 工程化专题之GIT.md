# ***工程化专题之GIT***

### **初识**

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

###  **逻辑区**

* Workspace 工作区
* Index/Stage 暂存区
* Repository 本地仓库
* Remote 远程仓库

### **常用命令**

* git status 有事没事敲一敲  查看文件状态
* git ac '提交注释'  （add  commit  同时进行）
* git add '文件名'  添加至暂存区
* git comit -m '注释' 提交至本地仓库
* git rm 删除
* git mv 改名
* git clone git@xxx.git  下载代码至本地
* git  remote  将代码推送到远端并在远端新建项目

  * 创建本地文件夹并 git init  初始化
  * 在远端 new project   (本地和远端的项目名必须相同  且必须为空项目)
  * git remote add origin git@xxx.git  （将本地和远端建立联系）   

  * git push origin master  (将本地代码推送至远端)
* git fetch 拉取远端信息
* git pull  拉取远端代码 并与本地合并
* git push 将本地代码推送至远端 
* git checkout
  * 切新分支  checkout -b dev 创建新分支  
  * 撤销更改  checkout . (撤销全部 可加具体文件名) 
* git log  日志
* git stash 工作未提交暂存栈
* git merge  合并分支
* git rebase 将head指定到某一个节点(变基)
* git tag 打版 一个特殊的分支
* git alias  命令组合







