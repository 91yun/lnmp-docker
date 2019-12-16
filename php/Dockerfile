# FROM php:7.3-fpm-alpine
FROM php:7.3-fpm
# RUN apk --no-cache add shadow

# RUN apk update && apk add tzdata \
# 	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \ 
# 	&& echo "Asia/Shanghai" > /etc/timezone	


RUN apt-get update && apt-get install -y tzdata \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \ 
	&& echo "Asia/Shanghai" > /etc/timezone

RUN apt-get update && apt-get install -y libpng-dev libzip-dev libxml2-dev libc-client-dev
RUN docker-php-ext-install pdo_mysql mysqli pcntl gd zip soap xmlrpc
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer 

RUN usermod -u 1000 www-data


#安装imap
RUN apt-get update && apt-get install -y libc-client-dev libkrb5-dev && rm -r /var/lib/apt/lists/*
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

# 安装ioncube插件
ADD https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz /tmp/
RUN tar xfzvC /tmp/ioncube_loaders_lin_x86-64.tar.gz /tmp/ \
    && rm /tmp/ioncube_loaders_lin_x86-64.tar.gz \
    && mv /tmp/ioncube/ioncube_loader_lin_7.3.so `php-config --extension-dir` \
    && docker-php-ext-enable ioncube_loader_lin_7.3 \
    && rm -rf /tmp/ioncube