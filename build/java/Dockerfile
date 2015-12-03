#Base image Define
From daocloud.io/daocloud/dao-tomcat:v7.0.55
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
# This software is only use for inner training.
########################################
# History  
# 2015-11-27 v0.0.1 First Version
########################################
########################################

#Environment Var Define
ENV REFRESHED_AT 2015-11-27 16:50
ENV Version 0.0.2
ENV TOMCAT_SERVER_XML_DIR /tomcat/conf
ENV TOMCAT_SERVER_XML server.xml
ENV TOMCAT_ROOT_DIR ROOT
ENV PROJECT_DIR /tomcat/webapps
ENV PROJECT_NAME yihuonet_test

#Deploy
#Del root dir first
RUN cd $PROJECT_DIR
RUN rm -rf $TOMCAT_ROOT_DIR

#Revise server.xml
ADD $TOMCAT_SERVER_XML_DIR/$TOMCAT_SERVER_XML $TOMCAT_SERVER_XML_DIR/$TOMCAT_SERVER_XML
ADD $PROJECT_DIR/$PROJECT_NAME/ $PROJECT_DIR/$PROJECT_NAME/

