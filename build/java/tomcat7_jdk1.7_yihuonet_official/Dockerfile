#Base Define
FROM daocloud.io/library/java:7-jre
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-12-23 15:06

#Version Define
ENV YIHUONET_VER 0.1.1

########################################
# History  
# 2015-11-27 v0.0.1 First Version
# 2015-12-23 v0.1.0 Push Online-test Version
########################################
########################################
#Official Code by docker-library, https://hub.docker.com/_/tomcat/

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

# see https://www.apache.org/dist/tomcat/tomcat-8/KEYS
RUN gpg --keyserver pool.sks-keyservers.net --recv-keys \
	05AB33110949707C93A279E3D3EFE6B686867BA6 \
	07E48665A34DCAFAE522E5E6266191C37C037D42 \
	47309207D818FFD8DCD3F83F1931D684307A10A5 \
	541FBE7D8F78B25E055DDEE13C370389288584E7 \
	61B832AC2F1C5A90F0F9B00A1C506407564C17A3 \
	713DA88BE50911535FE716F5208B0AB1D63011C7 \
	79F7026C690BAA50B92CD8B66A3AD3F4F22C4FED \
	9BA44C2621385CB966EBA586F72C284D731FABEE \
	A27677289986DB50844682F8ACB77FC2E86E29AC \
	A9C5DF4D22E99998D9875A5110C01C5A2F6059E7 \
	DCFD35E0BF8CA7344752DE8B6FB21E8933C60243 \
	F3A04C595DB5B6A5F1ECA43E3B7BBB100D811BBE \
	F7DA48BB64BCB84ECBA7EE6935CD23C10D498E23

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.67
ENV TOMCAT_TGZ_URL https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz
#ENV TOMCAT_VERSION 7.0.67
#ENV TOMCAT_TGZ_URL http://mirrors.cnnic.cn/apache/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

RUN set -x \
	&& curl -fSL "$TOMCAT_TGZ_URL" -o tomcat.tar.gz \
	&& curl -fSL "$TOMCAT_TGZ_URL.asc" -o tomcat.tar.gz.asc \
	&& gpg --verify tomcat.tar.gz.asc \
	&& tar -xvf tomcat.tar.gz --strip-components=1 \
	&& rm bin/*.bat \
	&& rm tomcat.tar.gz*

#########################################[START]!Pause official code to deploy yihuonet code.
ENV TOMCAT_ORIGIN_ROOT webapps/ROOT
ENV MCMS_DOWNLOAD_FILE http://7xoylx.com1.z0.glb.clouddn.com/yihuonet/yihuonet-v$YIHUONET_VER.zip

#Deploy AND Delete origin root directory
RUN apt-get install -y wget unzip
WORKDIR $CATALINA_HOME/webapps
RUN rm -rf ROOT
RUN mkdir ROOT
WORKDIR $CATALINA_HOME/$TOMCAT_ORIGIN_ROOT
RUN wget $MCMS_DOWNLOAD_FILE
RUN unzip yihuonet-v$YIHUONET_VER.zip
ADD tomcat/conf/server.xml $CATALINA_HOME/conf/server.xml
#########################################[END]!Recovery official code to deploy yihuonet code.
WORKDIR $CATALINA_HOME/webapps
RUN mv manager management
WORKDIR $CATALINA_HOME

EXPOSE 8080
CMD ["catalina.sh", "run"]

