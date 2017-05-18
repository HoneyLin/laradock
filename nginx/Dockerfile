FROM nginx:alpine

MAINTAINER Mahmoud Zalt <mahmoud@zalt.me>

ADD nginx.conf /etc/nginx/
#COPY sites/*.conf /etc/nginx/sites-available/

ARG PHP_UPSTREAM=php-fpm

RUN rm -r /etc/apk/repositories \
	&& echo -e 'http://mirrors.ustc.edu.cn/alpine/v3.4/main\nhttp://dl-cdn.alpinelinux.org/alpine/v3.4/main\nhttp://dl-cdn.alpinelinux.org/alpine/v3.4/community' >> /etc/apk/repositories \
	&& cat /etc/apk/repositories \
	&&apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data \
    && rm /etc/nginx/conf.d/default.conf \
    && echo "upstream php-upstream { server ${PHP_UPSTREAM}:9000; }" > /etc/nginx/conf.d/upstream.conf

CMD ["nginx"]

EXPOSE 80 443
