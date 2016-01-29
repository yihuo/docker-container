#易活办公网 私有.yh域名使用指南
![Docker-container](http://a.oss.yihuonet.com/storage/Docker-container.png)      
更新于：2016/1/29 13:25:33     | E-mail:kai.zhu#yihuonet.com (替换#为@)    

##1.为什么需要？
为方便在开发、测试环节中，缺少可用域名。避免“IP+端口”方式带来的不便，及可能程序上的兼容性问题。我们建立了.yh（易活的首字母缩写）域名进行内部使用，该域名在办公网外无效。    
本文中所有的链接地址，在公网均无法打开。

##2.怎么使用？
步骤非常简单，分为三步。熟练操作的话，一分钟可以完成所有步骤。    
第一步，打开DNS管理面板[https://dns.yh/namedmanager](https://dns.yh/namedmanager "[https://dns.yh/namedmanager]")，出现ssl证书错误请直接忽略，并用给定的用户名和密码进行登陆。
![Domain-yh-dns-login](http://a.oss.yihuonet.com/storage/guide-book/domain-yh-dns-login.png)

第二步，点击Domains/Zones添加域名。
![Domain-yh-dns-doamins-manager](http://a.oss.yihuonet.com/storage/guide-book/domain-yh-dns-doamins-manager.png)
点击Add New Domain，添加新的域名。    
只需填写DomainName和Description即可。DomainName为要创建的域名，无需加WWW。可以用的后缀有：  `.com.yh`,`.net.yh`,`.org.yh`。填写完成点击SaveChanges进行保存。Description填写谁在使用该域名，防止误修改。
![Domain-yh-dns-doamins-manager2](http://a.oss.yihuonet.com/storage/guide-book/domain-yh-dns-doamins-manager2.png)
如果该域名之前不存在，将出现下面页面，此时可以进行域名记录的添加。
![Domain-yh-dns-doamins-manager3](http://a.oss.yihuonet.com/storage/guide-book/domain-yh-dns-doamins-manager3.png)
办公网测试仅需使用A记录，请参考红线全出的进行填写。    
特别说明的是，@表示域名自身。图上填写的表示如下含义：    
`将域名 yourname.com.yh 指向IP 10.0.0.8` , `将域名 www.yourname.com.yh 指向IP 10.0.0.8`
![Domain-yh-dns-doamins-manager4](http://a.oss.yihuonet.com/storage/guide-book/domain-yh-dns-doamins-manager4.png)

第三步，联系管理员（也就是我），在服务器上注册这个域名，任何形式都可以。
