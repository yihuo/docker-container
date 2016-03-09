#Base Define
FROM ubuntu:14.04
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-03-08 14:35

########################################
#Evnironment Vars Define

RUN apt-get update && apt-get install -y \
        automake \
		autotools-dev \
		g++ \
		git \
		libcurl4-gnutls-dev \
		libfuse-dev \
		libssl-dev \
		libxml2-dev \
		make \
		pkg-config
RUN mkdir /data \
    && git clone https://github.com/aliyun/ossfs.git \
	&& cd ossfs \
	&& ./autogen.sh \
    && ./configure \
    && make \
    && sudo make install \
	&& echo $OSS_BUCKET_NAME:$OSS_KEY:$OSS_KEY_ACCESS > /etc/passwd-ossfs \
	&& chmod 640 /etc/passwd-ossfs \
	&& ossfs your_oss_bucket your_mount_dir -ourl=your_oss_service_url