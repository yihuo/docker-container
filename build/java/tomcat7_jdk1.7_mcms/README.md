#基于Dockerfile部署应用的注意事项
![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)      
更新于：2016/1/25 11:44:38    | E-mail:kai.zhu#yihuonet.com (替换#为@)    

##1.环境变量
需要设置以下环境变量，才能成功启动应用。    
`VIRTUAL_HOST`  使用nginx-proxy镜像才需使用这个环境变量。值为绑定的域名，请在域名解析处做A记录解析到宿主机IP（或Cname记录解析到宿主机名）。绑定多个域名的，以英文逗号分隔即可。    
`YIHUONET_MCMS_MYSQL_JDBC`  JDBC连接地址。    
`YIHUONET_MCMS_MYSQL_USER`  MySQL账号。    
`YIHUONET_MCMS_MYSQL_USER_PASS`  MySQL密码。    

如用.yaml格式，可以如下形式写:    
`- VIRTUAL_HOST=[$Domain]`    
`- YIHUONET_MCMS_MYSQL_JDBC=jdbc:mysql://[$MySQL_Database]:[$MySQL_PORT]/[$MySQL_Database_Name]?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull`    
`- YIHUONET_MCMS_MYSQL_USER=[$MySQL_Database_Username]`    
`- YIHUONET_MCMS_MYSQL_USER_PASS=[$MySQL_Database_Password]`    
形如`[$Parameter]`的请自行替换为真实值。
绑定多个域名的，以英文逗号分隔即可。

##2.卷
请按如下格式设置Volume值，以保证更新或重新部署应用后，通过后台上传的图片等信息不丢失。    

| 容器路径 | 主机路径 |
|:-------:|:-------:|
|/usr/local/tomcat/webapps/ROOT/upload|/data/[$Your_app_name]/upload|
请自行替换[$Your_App_name]为你的应用名称，当然/data这个目录可以更换为/home、/opt等等，你的数据盘地址。    
请给予Volume可以读写的权限。
	
