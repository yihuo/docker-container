#Base Define
FROM php:5.5-apache
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-03-08 14:35

########################################
# History  
# 2015-11-27 v0.0.1 First Version
########################################
# YOU SHOULD BE DO THIS BEFORE USING THE IMAGE.
# Add volumes {host directory}:{container directory}
########################################
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

