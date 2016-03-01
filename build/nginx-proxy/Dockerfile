FROM jwilder/nginx-proxy
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-12-31 16:37

##################################
#Update default index page.
##################################
#This script by https://github.com/schmunk42/nginx-proxy
RUN { \
      echo 'server_tokens off;'; \
      echo 'client_max_body_size 100m;'; \
    } > /etc/nginx/conf.d/my_proxy.conf
RUN rm -f /usr/share/nginx/html/index.html
ADD defaultpages/index.html /usr/share/nginx/html/index.html