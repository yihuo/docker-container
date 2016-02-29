#Base Define
FROM daocloud.io/library/java:7-jre
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2016-01-28 13:27

#Version Define - !!!!!!!!!!!!!!!MUST REVISE HERE FIRST!!!!!!!!!!!!!!!!!!!!!
ENV YIHUONET_MCMS_SERIES general-1
ENV YIHUONET_MCMS_VER 1.1.0
ENV YIHUONET_MCMS_FILENAME mcms-$YIHUONET_MCMS_SERIES-v$YIHUONET_MCMS_VER.zip
########################################
# History  
# 2015-11-27 v0.0.1 First Version
# 2015-12-23 v0.1.0 Push Online-test Version
# 2016-01-04 v1.0.1 Land
# 2016-01-25 v1.1.0 Final version update
########################################
########################################
#Official Code by docker-library, https://hub.docker.com/_/tomcat/

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.68
ENV TOMCAT_TGZ_URL http://mirrors.aliyun.com/apache/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

RUN set -x \
	&& curl "$TOMCAT_TGZ_URL" -o tomcat.tar.gz \
	&& tar -xvf tomcat.tar.gz --strip-components=1 \
	&& rm bin/*.bat \
	&& rm tomcat.tar.gz*

#########################################[START]!Pause official code to deploy yihuonet code.
ENV TOMCAT_ORIGIN_ROOT webapps/ROOT
ENV MCMS_DOWNLOAD_FILE http://a.oss.yihuonet.com/program-base/mcms/$YIHUONET_MCMS_FILENAME

#Deploy AND Delete origin root directory
WORKDIR $CATALINA_HOME/webapps
RUN apt-get install -y wget unzip \
    && rm -rf ROOT \
    && mkdir ROOT \
	&& cd $CATALINA_HOME/$TOMCAT_ORIGIN_ROOT \
	&& wget $MCMS_DOWNLOAD_FILE \
	&& unzip $YIHUONET_MCMS_FILENAME \
	&& rm -f $YIHUONET_MCMS_FILENAME \
    && cd $CATALINA_HOME/webapps \
	&& mv manager management
ADD tomcat/conf/server.xml $CATALINA_HOME/conf/server.xml
#########################################[END]!Recovery official code to deploy yihuonet code.
WORKDIR $CATALINA_HOME

EXPOSE 8080
CMD ["catalina.sh", "run"]

