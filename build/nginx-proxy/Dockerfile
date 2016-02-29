FROM jwilder/nginx-proxy
MAINTAINER kai.zhu "kai.zhu@yihuonet.com"
ENV REFRESHED_AT 2015-12-31 16:37

##################################
#Update default index page.
##################################
RUN echo "client_max_body_size 50m;" >>  /etc/nginx/nginx.conf
RUN rm -f /usr/share/nginx/html/index.html
ADD defaultpages/index.html /usr/share/nginx/html/index.html