FROM php:7.3-fpm-alpine

RUN apk --no-cache add shadow \
	&& usermod -u 1000 www-data

RUN apk update && apk add tzdata \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \ 
	&& echo "Asia/Shanghai" > /etc/timezone	

RUN cd ~ \
	&& apk add libstdc++ libpng-dev \
    && docker-php-ext-install pdo_mysql mysqli pcntl gd\
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer 

# 安装ioncube插件
ADD https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz /tmp/
RUN tar xfzvC /tmp/ioncube_loaders_lin_x86-64.tar.gz /tmp/ \
    && rm /tmp/ioncube_loaders_lin_x86-64.tar.gz \
    && mv /tmp/ioncube/ioncube_loader_lin_7.3.so `php-config --extension-dir` \
    && docker-php-ext-enable ioncube_loader_lin_7.3 \
    && rm -rf /tmp/ioncube