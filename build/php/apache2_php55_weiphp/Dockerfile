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
ENV PROJECT_NAME weiphp
ENV PROJECT_VER 1.0.0
ENV YIHUONET_FILENAME $PROJECT_NAME-v$PROJECT_VER.zip

#Filename format: "project name"-v"version code".zip and upload to Download OSS(define in line 25).

########################################
ENV DOWNLOAD_FILE http://us.oss.yihuonet.com/yihuonet-official-website/weiphp/$YIHUONET_FILENAME

#Setup GD, iconv, mcrypt, php-mbstring
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
		php-pear \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd


#Setup pdo_mysql and php-mbstring
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install mbstring
	
RUN apt-get install -y wget unzip \
    && rm -rf /var/www/html \
    && mkdir /var/www/html \
	&& cd /var/www/html \
	&& wget $DOWNLOAD_FILE \
	&& unzip $YIHUONET_FILENAME \
	&& rm -f $YIHUONET_FILENAME \
	&& chmod 777 -R ./Runtime/ ./Uploads/Download ./Uploads/Picture ./Uploads/Editor ./Addons ./Data ./Application/Install/Data ./Application/Common/Conf/config.php
	
