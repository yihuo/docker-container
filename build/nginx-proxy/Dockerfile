FROM jwilder/nginx-proxy
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-12-31 16:37

##################################
#Update default index page.
##################################
RUN echo "server_tokens off; client_max_body_size 512m;" > /etc/nginx/conf.d/my_proxy.conf
RUN rm -f /usr/share/nginx/html/index.html
ADD defaultpages/index.html /usr/share/nginx/html/index.html