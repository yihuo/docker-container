#Base Define
FROM daocloud.io/library/java:7-jre
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-12-23 15:06

#Version Define
ENV YIHUONET_VER 0.1.3

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

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.67
ENV TOMCAT_TGZ_URL https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz
#ENV TOMCAT_VERSION 7.0.67
#ENV TOMCAT_TGZ_URL http://mirrors.cnnic.cn/apache/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

RUN set -x \
	&& curl -fSL "$TOMCAT_TGZ_URL" -o tomcat.tar.gz \
	&& tar -xvf tomcat.tar.gz --strip-components=1 \
	&& rm bin/*.bat \
	&& rm tomcat.tar.gz*

#########################################[START]!Pause official code to deploy yihuonet code.
ENV TOMCAT_ORIGIN_ROOT webapps/ROOT
ENV MCMS_DOWNLOAD_FILE http://yihuonet.vpc100-oss-cn-hangzhou.aliyuncs.com/yihuonet-official-website/-v$YIHUONET_VER.zip

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

