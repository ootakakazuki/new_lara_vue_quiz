FROM php:8.0-fpm
COPY php.ini /usr/localetc/php

RUN apt-get update \
    && apt-get install -y zlib1g-dev libzip-dev mariadb-client libpng-dev unzip

# composer install 
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# node install

COPY --from=node:lts /usr/local/bin /usr/local/bin
COPY --from=node:lts /usr/local/lib /usr/local/lib

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

RUN composer global require "laravel/installer"
RUN apt-get update && apt-get -y install vim
RUN docker-php-ext-install pdo_mysql
