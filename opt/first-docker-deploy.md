#欢迎使用易活网络Docker培训指南
![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)      
此指南基于MIT协议并持续完善中，欢迎给予各种意见和建议，我们将积极采纳。我们希望能够变得更好，并且不作恶！     
更新于：2016/1/19 13:32:20 | E-mail:kai.zhu#yihuonet.com (替换#为@)    
本章节主要说明了如何手动的利用Daocloud创建一个Java CMS项目并实现发布，当然这类的工具还是很多的，可以自由选择，这不是软文。

##1.Daocloud界面初识
下面是Daocloud登陆成功后的界面，对于小公司/小项目的开发、测试人员，暂时只需要接触红线框出的功能：代码构建、镜像仓库、应用管理。对于运维人员还需要操作：我的集群和应用编排。    
如果自己没有服务器，可以采用：服务集成、Volume两个功能。自己有服务器且资源不紧张的的，就可以略过了。即使自己有服务器，也可以利用免费的额度创建临时的应用做测试、调试使用。
![Daocloud-index](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-index-usage.png)
代码构建：基于Git进行镜像的构建。    
镜像仓库：已经构建成功的镜像存放的位置。    
应用管理：依据镜像仓库中镜像创建的应用（生产环境）。

##2.代码构建过程
点击代码构建，进入代码构建模块。下图为代码构建页面：    
![Daocloud-index-code-build](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-code-build.png)    
页面右侧区域很清晰的列出了已有的项目情况，及创建新项目的入口。也可以点击帮助文档进行查看。    
点击创建新项目，进行项目的创建。    
![Daocloud-index-code-build-new-project](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-code-build-new-project.png)
填写项目名称，填写Dockerfile文件的地址。——本文不讨论Dockerfile文件如何写，后续文章说明。
![Daocloud-index-code-build-new-project-keyin](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-code-build-new-project-keyin.png)
填写完毕系统开始第一次自动构建。当然这个窗口没必要一直开着，除非是调试确认有无问题，一般情况下获得的Dockerfile都是测试没有问题的，不需要盯着看。去喝个咖啡……本例中的Dockerfile基于OpenJDK1.7的官方镜像，安装Tomcat7.0.67，然后将JAVA程序以wget方式从指定的存储中下载，并调整server.xml的配置信息。最后开启容器080端口，启动Catalina服务。
![Daocloud-index-code-auto-build](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-code-auto-build.png)
![Daocloud-index-code-auto-build](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-code-auto-build2.png)


##3.镜像
执行成功，可以点击这个界面上的查看镜像，也可以在首页点击“镜像仓库”，查看刚刚构建成功的镜像。
![Daocloud-index-images](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images.png)
我们可以看一下，这里的版本系统自动命名规范：
master代表是基于master分支构建的镜像，init表示第一次构建的镜像（创建项目时的基线）。我们再看另一张图，镜像较多的。如release-1.1.1是分支的名称，基于这个分支构建的镜像。而ecee9ac是git版本号的前7位。这个release分支恰好是根据master分支同样的版本号构建的，因为这里恰好使用master分支构建过这个镜像，不然是只有一个release分支的。
![Daocloud-index-images-mcms](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms.png)
我们看一下这张构建的具体历史图。这个Release分支是在24小时前，由zhukainet创建Release分支时系统自动产生的镜像，区别于手动构建会显示为Daocloud。
![Daocloud-index-images-mcms-log](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-log.png)

##4.部署第一个Docker应用
现在才是激动人心的时候，镜像构建完。那么就是部署了，本文说的是手动构建，那么我们就手动构建应用吧。——当然如果自动构建，第一次的应用也是得手动建立一下的（更新版本无需人工参与）。
![Daocloud-index-images-mcms-deploy](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy.png)
点击部署最新版本，进行设置。常规的填写应用名称（便于区分），建议这里写网站域名，然而“.”打不了可以用下划线解决。点击基础设置。    
PS：按这么说，我们这个应用域名是cms.com.yh？ 是的，然而yh这个根域名并不存在，作者在办公网创建了这个不存在的域名仅仅为了方便调试用，可以用任何一个DNS服务器去实现，管理一个根域名对于“运维狗”来说，是不是感觉良好。
![Daocloud-index-images-mcms-deploy2](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy2.png)
下一步是填写一些高级的配置，这里我们没有修改端口。只是加了卷（Volume）和环境变量。对于“程序猿”来说，环境变量比较好理解，我们这里设置的三个环境变量分别是JDBC地址、MySQL账户和密码（这里的数据库信息，自己刷库，不做演示）。    
那么什么是卷？因为Docker一旦部署成功，任何对Docker这个虚拟的操作系统做的修改都是暂时有效的，一旦容器重启/崩溃会自动恢复，所做的修改都会丢失。那么我们将一些可能发生更改的目录映射到宿主机上即可实现长期保存。忘记部署完还需要人工一一配置的历史吧，否则你永远用不好Docker！——这里暂时不具体说原理，这里配置的作用是将ROOT这个应用的upload目录映射到宿主机的/data/cms-com-yh/upload目录。
![Daocloud-index-images-mcms-deploy3](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy3.png)
下面是Docker进行部署应用的界面，日志可以随时查看并自动刷新，我们可以看看Docker到底做了什么。
![Daocloud-index-images-mcms-deploy4](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy4.png)
经过几分钟到最长20分钟的等待（20分钟执行无法完成将认为超时失败），应用成功部署完成。日志中显示:    
`Server startup in 9185ms`    
`#此处显示的完成日志输出，取决于应用内容器（此处的容器和应用容器不是一个概念，这里的容器特指Tomcat/Apache\Nginx……）。` 
![Daocloud-index-images-mcms-deploy5](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy5.png)
那么问题来了，我们如何访问这个已经部署成功的应用。方法：切换到容器选项卡，即可看到Docker自动分配的端口和访问地址。Docker提供了三个IP+Port的访问形式：    
10.0.0.15的IP是作者办公局域网的机器地址，也是真实的地址；
60.167.109.63这个是网关地址（PS：不用尝试了，所有正常的端口都没开）；
还有一个172.17.0.0网段的IP……这个所有的Docker机器都会显示这样一个，这是Docker容器与其宿主机通信的IP，Docker在宿主机上创建了一个网卡/网桥用于通信。（我们这里暂时用不着）
![Daocloud-index-images-mcms-deploy6](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy6.png)
尝试进行访问，http://10.0.0.15:32779，访问正常！
![Daocloud-index-images-mcms-deploy7](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy7.png)

##5.怎么样才能不加端口进行访问？
看见刚才的应用是需要加端口才能访问的，有没有一种感觉叫“我勒个去啊”，这样用户怎么记得端口（而且Docker应用的端口还会随着应用重新不断变化）。当然这是有解决方案的。易活网络提供的GitHub库中，提供了一个叫做NginxProxy的Docker镜像（非原创，感谢[Jwilder/nginx-proxy Docker](https://hub.docker.com/r/jwilder/nginx-proxy/)），可以实现将IP/域名加端口的访问形式变为直接输入域名访问，原理：Nginx反向代理。   
用Nginx作为前端负载均衡加反向代理，基本上对于不是很大的网站来说，是足够了。
这里我们只说如何使用，至于这个Nginx-Proxy如何安装，请看[传送门](setup-nginx-proxy.html "[setup-nginx-proxy.html]") [传送门-in Github](setup-nginx-proxy.md "[setup-nginx-proxy.md]")。    
当然，这个Nginx-Proxy也是工作在Docker环境内的，安装起来和正常的Docker应用一样安装。如果你按照上述传送门的说明，在每一台宿主机上安装了Nginx-Proxy应用。那么这里就可以用一个环境变量完成域名的绑定工作。    
添加一个环境变量：`VIRTUAL_HOST`，值为你希望绑定的域名，上述我们假定绑定的域名为“cms.com.yh”。点击保存更改，会提示重新部署应用。如果你已经设置好了类似于Upload、Attachments等等安装后会发生变化的目录的Volumes，这时就可以点击确认，否则**请先做好数据保存及Volumes的设置工作**。—— 当然这个`VIRTUAL_HOST`环境变量是可以在创建应用的时候就设置的。
![Daocloud-index-images-mcms-deploy8](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy8.png)
坐等重新部署完成，输入http://cms.com.yh/ 完美解析成功。
![Daocloud-index-images-mcms-deploy9](http://a.oss.yihuonet.com/storage/guide-book/Daocloud-images-mcms-deploy9.png)

Why？每一台都要安装是为什么？    
答案是：你不给每台宿主机装一个Nginx-Proxy。域名只能解析到你的宿主机IP（一般是公网IP或者网关IP，内部测试用可以解析到内网IP，然而Docker的那个IP和你并没有什么卵关系。），然而宿主机怎么知道你想“转发”到那个Docker应用？只有用Nginx-Proxy去充当反向代理，同时去监控Docker的内核（管理IP和Port），才能去实现这样一个转发。

----------
    
到此，说完了如何利用Daocloud去部署第一个项目的第一个应用，其他功能自行琢磨。    
下一节，我们展示如何自动化升级一个应用（持续构建和持续集成），然而篇幅小的你不敢相信。    
[点击这里进入传送门](first-docker-deploy-automatic.html "[first-docker-deploy-automatic.html]")，进入下一节。    
[点击这里进入传送门-in Github](first-docker-deploy-automatic.md "[first-docker-deploy-automatic.md]")，进入下一节。