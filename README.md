![Docker-container]<!--(mahua-logo.jpg)-->
##Docker-container是什么?<br/>What's Docker-container?

<br/>一个支持Java、PHP的混合式Docker容器库，本项目暂时处于开发环节，您通过Dockerfile文件生成的Docker应用可能会出现各种意想不到的情况，请不要在生产环境使用。
<br/>


<br/>

##目录说明<br/>The note of directory

* build 目录 ： Docker构建环境的主目录。
    * html 目录 
        * nginx 目录 ：
            * 功能：暂仅支持nginx容器，采用Debian Jessie + Nginx1.9.8 实现纯静态html网站的部署。
            * 版权说明：基于***构建，原地址为：*
            * 使用方法：
        * java 目录 ：
            * 功能：支持Tomcat和wildfly（即jboss）两种容器，基于OpenJDK1.7和OpenJDK1.6两种基础Docker镜像构建，实现Java网站的部署。 
            * 版权说明：基于***构建，原地址为：*
    		* 使用方法：
        * nginx-proxy 目录 ：
            * 功能：实现将Docker应用的访问方式从IP:PORT（IP地址加端口）变为直接通过域名访问，无需加端口访问。
			* 版权说明：基于***构建，原地址为：*
			* 使用方法：
* opt 目录 ： 用于本Git库部分相关数据的存放，即使丢失亦不影响该库的正常使用。
* README.md ： 本文件，说明文件。
* LICENSE.md ： 开源许可协议文件。
			

##问题反馈
在使用中有任何问题，欢迎反馈给，可以用以下联系方式取得联系：

* 邮件： kai.zhu#yihuonet.com, 把#换成@
* 官方网站: [易活网络](http://www.yihuonet.com)


##感激
感谢以下的项目,排名不分先后

* [Test](http://www.example.com/) 

