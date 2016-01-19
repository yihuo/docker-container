![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)
##Docker-container是什么? - What's Docker-container?

  
一个支持Java、PHP、Html和Nginx反向代理（SLB）的混合式Docker容器库，本项目暂时处于开发环节，您通过Dockerfile文件生成的Docker应用可能会出现各种意想不到的情况，请不要在生产环境使用。）的混合式Docker容器库，本项目暂时处于开发环节，您通过Dockerfile文件生成的Docker应用可能会出现各种意想不到的情况，请不要在生产环境使用。
 
A container warehouse which support java, php, html and nginx proxy(slb). This project on building now. When you use the dockerfile to build your docker app may happened such more situation we don't want to see it, so please don't use it in formal environment.
  
##目录说明 - The note of directory
* build 目录 ： Docker构建环境的主目录。
    * html 目录 
        * nginx 目录 ：
            * 功能：暂仅支持nginx容器，采用Debian Jessie + Nginx1.9.8 实现纯静态html网站的部署。
            * 版权说明：基于Docker下列官方库debian:jessie、nginx:latest构建。
            * 使用方法：
        * java 目录 ：
            * 功能：支持Tomcat和wildfly（即jboss）两种容器，基于OpenJDK1.7和OpenJDK1.6两种基础Docker镜像构建，实现Java网站的部署。 
            * 版权说明：基于Docker下列官方库Tomcat(OpenJDK1.6 OpenJDK1.7)、Wildfly构建。
    		* 使用方法：
        * nginx-proxy 目录 ：
            * 功能：实现将Docker应用的访问方式从IP:PORT（IP地址加端口）变为直接通过域名访问，无需加端口访问。
			* 版权说明：基于Docker镜像Jwilder/nginx-proxy构建。
			* 使用方法：
* opt 目录 ： 用于本Git库部分其他数据的存放，即使丢失亦不影响该库的正常使用。
* README.md ： 本文件，说明文件。
* LICENSE.md ： 开源许可协议文件。


----------


* build directory： The build environment of docker.
    * html directory
        * nginx directory ：
            * Function：Only support nginx container now, use Debian Jessie + Nginx1.9.8 to support html website deploy.
            * License：Build based by Docker official images "Debian:jessie" and "nginx:latest".
            * Usage：
        * java directory ：
            * Function：Support Tomcat and wildfly(old name is jboss), based OpenJDK1.7 and OpenJDK1.6 images to develop, support java website deploy. 
            * License：Build based by Docker official images "Tomcat(OpenJDK1.6 OpenJDK1.7)" and "Wildfly".
    		* Usage：
        * nginx-proxy directory ：
            * Function：To realize visit docker app from ip:port to domain, you can visit docker app by domain to instead ip:port from today.
			* License：Build based by Docker images "Jwilder Nginx-proxy".
			* Usage：
* opt directory ： To save some data with this git, the github will be normal use if this directory lost.
* README.md ： This file which give a readme to everyone.
* LICENSE.md ： License file.	

  
  
##问题反馈 - Feedback question  

在使用中有任何问题，欢迎反馈，可以用以下联系方式取得联系：  
  
If you has any question in use, please contact with us by below way. We hope to get your feedback.

* 邮件/E-mail： kai.zhu#yihuonet.com （把#换成@，to convert # to @）
* 官方网站/Offical Website: [易活网络 Yihuonet](http://www.yihuonet.com)

  
  
##感激 - Thanks
感谢以下的项目,排名不分先后。请在使用时，遵守相关使用协议的约定。  
Thanks to the following items withour ranking. Please allow the rules of copyrights or license file by this project.


* [Debian Docker](https://hub.docker.com/_/debian/) 
* [Nginx Docker](https://hub.docker.com/_/nginx/) 
* [Tomcat Docker](https://hub.docker.com/_/tomcat/) 
* [Wildfly(Jboss) Docker](https://hub.docker.com/r/jboss/wildfly/) 
* [Jwilder/nginx-proxy Docker](https://hub.docker.com/r/jwilder/nginx-proxy/) 
