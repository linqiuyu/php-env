FROM php:7.4-fpm

RUN apt-get update && \
    apt-get install -y libzip-dev libxslt-dev libmagickwand-dev default-mysql-client librdkafka-dev && \
    docker-php-ext-install bcmath zip pdo_mysql mysqli opcache pcntl xsl && \
    pecl install http://pecl.php.net/get/xdebug-3.1.2.tgz &&\
    pecl install imagick && \
    pecl install redis && \
    pecl install rdkafka && \
    rm -rf /var/cache/apt/*

RUN apt-get install -y supervisor

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp

RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

VOLUME /var/www/html
WORKDIR /var/www/html

COPY docker-php-entrypoint /usr/local/bin/