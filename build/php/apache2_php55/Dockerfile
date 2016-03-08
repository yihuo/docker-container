#Base Define
FROM php:5.5-apache
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-03-08 14:35

########################################
# History  
# 2015-11-27 v0.0.1 First Version
########################################
########################################
#Version Define - !!!!!!!!!!!!!!!MUST REVISE HERE FIRST!!!!!!!!!!!!!!!!!!!!!
ENV PROJECT_NAME sample-project
ENV PROJECT_VER 1.0.0
ENV YIHUONET_FILENAME $PROJECT_NAME-v$PROJECT_VER.zip

#Filename format: "project name"-v"version code".zip and upload to Download OSS(define in line 25).

########################################
ENV DOWNLOAD_FILE http://us.oss.yihuonet.com/program-base/project/$YIHUONET_FILENAME

RUN apt-get update && apt-get install -y wget unzip \
    && rm -rf /var/www/html \
    && mkdir /var/www/html \
	&& cd /var/www/html \
	&& wget $DOWNLOAD_FILE \
	&& unzip $YIHUONET_FILENAME \
	&& rm -f $YIHUONET_FILENAME \
