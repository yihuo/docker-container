#欢迎使用易活网络Docker培训指南
#《Git和Dockerfile集成的威力：一行命令完成发布》
![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)      
此指南基于MIT协议并持续完善中，欢迎给予各种意见和建议，我们将积极采纳。我们希望能够变得更好，并且不作恶！     
更新于：2016/1/20 15:27:03  | E-mail:kai.zhu#yihuonet.com (替换#为@)    
本章节主要说明了如何利用Git实现自动更新应用，[基于之前构建的Java CMS项目](first-docker-deploy-automatic.html "[first-docker-deploy.html]")([Github MD地址](first-docker-deploy-automatic.md "[first-docker-deploy.md]"))，当然这类的工具还是很多的，可以自由选择，这不是软文。

##1.Git的简单介绍
定义：Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。Git的读音为/gɪt/。Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

##2.Git的常规命令（只说本文用到和相关的）
`git add <file> #`  将工作文件修改提交到本地暂存区    
`git add . #`  将所有修改过的工作文件提交暂存区    
`git commit`  -m "提交的描述信息"    
`git br <new_branch>`  # 创建新的分支    
`git br -d <branch>`  # 删除某个分支    
`git br -D <branch>`  # 强制删除某个分支 (未被合并的分支被删除的时候需要强制)    
`git pull`  # 抓取远程仓库所有分支更新并合并到本地    
`git pull`  --no-ff # 抓取远程仓库所有分支更新并合并到本地，不要快进合并    
`git push`  # push所有分支    
`git push origin master`  # 将本地主分支推到远程主分支    
`git push -u origin master`  # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)    
`git push origin <local_branch>`  # 创建远程分支， origin是远程仓库名    
`git push origin <local_branch>:<remote_branch>`  # 创建远程分支    
`git push origin :<remote_branch>`  #先删除本地分支(git br -d <branch>)，然后再push删除远程分支    

##3.Follow me，执行一次自动构建和部署给你看。
首先将在Dev-\*****上开发的分支，merge到Master分支。—— 这里不介绍`git merge`命令，不然会牵扯的太远。    
我们这里演示发布前文提及的Java CMS网站，如何直接更新生产环境。    
第一步，应用程序打包为zip包并上传至指定位置，修改Dockerfile文件相关信息。    
指定位置：由Dockerfile定义，我们这里是在自动构建的时候，采用wget方式从指定的`MCMS_DOWNLOAD_FILE`环境变量处下载，这个环境变量即为需要上传的位置，并按照`YIHUONET_MCMS_FILENAME`中约定名称的形式进行命名zip包。    
我们采用zip包的命名格式为：程序名-系列名称-版本号。
![Deploy-docker-with-git2](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git2.png)    
第二步，基于Master分支构建Release分支。    
打开Git Shell（登陆配置、安装Git的过程不复述），进入master分支。如果当前不在master分支，执行`git checkout master`切换到master分支。    
下面的操作生效与否，取决于是否参照这篇文章的说明进行了设置，[[传送门]](first-docker-deploy-automatic.html "[first-docker-deploy-automatic.html]") [[传送门-in Github]](first-docker-deploy-automatic.md "[first-docker-deploy-automatic.md]")。如未按照上文或者上文的思想进行设置，肯定不会生效。
![Deploy-docker-with-git](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git.png)    
输入`git branch Release-general-1-1.0.0`创建一个Release分支。其中Release为发布分支的意思，general-1为系列的名字，我们在多个项目公用一个版本库，因而需要进行区分设置。1.0.0是发布的产品版本号。    
![Deploy-docker-with-git3](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git3.png)    
输入`git checkout Release-general-1-1.0.0`切换到刚才创建的分支。    
这时，系统给出了提示？好吧，正常情况是不该有提示的，然而我们正在写这篇MD文章，所以……这个问题可以愉快的忽略。继续执行。
![Deploy-docker-with-git4](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git4.png)    
输入`git commit`确认一下问题，的确是只有这两个md文件，那么果断忽略。执行最后一步操作。    
![Deploy-docker-with-git5](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git5.png)    
输入`git push origin Release-general-1-1.0.0:Release-general-1-1.0.0`，但暂时先不执行。我们先打开Daocloud的控制台，看一下上次的执行情况，看看是否真的自动构建了。    
![Deploy-docker-with-git6](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git6.png)    
按下回车之后，立即自动创建了一个镜像构建任务，并且“开始执行”。
![Deploy-docker-with-git7](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git7.png)    
当镜像自动构建完成后，进入应用列表，找到基于这个镜像构建的应用。看见“事件”选项卡中，这个应用已经根据最新的镜像开始了自动发布。    
那么我们还要做什么么？    
Anything？No,nothing else……
![Deploy-docker-with-git8](http://a.oss.yihuonet.com/storage/guide-book/Deploy-docker-with-git8.png)    

----------
    
Git和Dockerfile集成的威力：一行命令完成发布，已经介绍完了。    
[点击这里进入传送门](first-docker-deploy-automatic-git.html "[#]")，进入下一节。    
[点击这里进入传送门-in Github](first-docker-deploy-automatic-git.md "[#]")，进入下一节。