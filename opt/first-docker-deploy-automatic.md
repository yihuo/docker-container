#欢迎使用易活网络Docker培训指南
![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)      
此指南基于MIT协议并持续完善中，欢迎给予各种意见和建议，我们将积极采纳。我们希望能够变得更好，并且不作恶！     
更新于：2016/1/19 13:32:20 | E-mail:kai.zhu#yihuonet.com (替换#为@)    
本章节主要说明了如何利用Daocloud进行持续构建和持续集成，[基于上一节构建的Java CMS项目](first-docker-deploy-automatic.html "[first-docker-deploy.html]")([Github MD地址](first-docker-deploy-automatic.md "[first-docker-deploy.md]"))，当然这类的工具还是很多的，可以自由选择，这不是软文。

##1.自动构建
找到代码构建中，java-cms项目，并将“触发规则”进行设置。我们定义自动构建和自动部署都是基于Release分支的，进行自动化生产环境部署，而测试和开发的环境，采用手动构建方式。
![Daocloud-index-images-mcms-automatic](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy-automatic.png)
触发规则填写如下图，当基于Master分支创建“Release-”开头的分支时，将自动创建最新镜像。
![Daocloud-index-images-mcms-automatic2](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy-automatic2.png)
##2.自动部署（发布到最新版本）
找到应用列表中，应用的发布选项卡，将“自动发布”开启。此时当最新的镜像构建成功后，将自动进行发布。    
在这里我们需要注意的是，这里的自动发布并不会识别分支是否为Release分支，即使是Test和Dev、Master分支手动构建了最新镜像后，仍然会自动发布。    
解决办法：    
A.创建一个项目的时候，生产环境和开发测试环境进行分离，当作两个项目进行设置。这样就不会出现误将测试或者正在开发的项目发布到生产环境了。    
B.或者就干脆不要用“自动发布”，当然这需要运维人员升级时手动点一下。—— 应用数量多的话，确实是个不小的挑战。
![Daocloud-index-images-mcms-automatic3](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy-automatic3.png)
----------
    
自动化升级一个应用（持续构建和持续集成）已经介绍完了。    
[点击这里进入传送门](first-docker-deploy-automatic.html "[#]")，进入下一节。    
[点击这里进入传送门-in Github](first-docker-deploy-automatic.md "[#]")，进入下一节。