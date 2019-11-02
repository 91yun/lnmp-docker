FROM php:7.3-fpm-alpine

RUN apk --no-cache add shadow \
	&& usermod -u 1000 www-data

RUN cd ~ \
	&& apk add libstdc++ libpng-dev \
    && docker-php-ext-install pdo_mysql mysqli pcntl gd\
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \