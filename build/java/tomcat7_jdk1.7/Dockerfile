#Base Define
FROM tomcat:7-jre7
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-03-08 14:35

########################################
# History  
# 2015-11-27 v0.0.1 First Version
########################################
#Version Define - !!!!!!!!!!!!!!!MUST REVISE HERE FIRST!!!!!!!!!!!!!!!!!!!!!
ENV PROJECT_NAME sample-project
ENV PROJECT_VER 1.0.0
ENV YIHUONET_FILENAME $PROJECT_NAME-v$PROJECT_VER.zip

#Filename format: "project name"-v"version code".zip and upload to Download OSS(define in line 25).

########################################
# History  
# 2015-01-20 v0.1.0 Based by General-1 dockerfile
# 2016-01-25 v1.0.0 Final version update
########################################

#########################################[START]!Pause official code to deploy yihuonet code.
ENV TOMCAT_ORIGIN_ROOT webapps/ROOT
ENV DOWNLOAD_FILE http://us.oss.yihuonet.com/program-base/project/$YIHUONET_FILENAME

#Deploy AND Delete origin root directory
WORKDIR $CATALINA_HOME/webapps
RUN apt-get update && apt-get install -y wget unzip \
    && rm -rf ROOT \
    && mkdir ROOT \
	&& cd $CATALINA_HOME/$TOMCAT_ORIGIN_ROOT \
	&& wget $DOWNLOAD_FILE \
	&& unzip $YIHUONET_FILENAME \
	&& rm -f $YIHUONET_FILENAME \
    && cd $CATALINA_HOME/webapps \
	&& rm -rf manager
ADD tomcat/conf/server.xml $CATALINA_HOME/conf/server.xml

