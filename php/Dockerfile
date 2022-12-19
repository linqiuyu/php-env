FROM php:7.4-fpm

COPY pecl-packages/swoole-4.8.12.tgz /root/pecl-packages
COPY pecl-packages/xdebug-3.1.2.tgz /root/pecl-packages
COPY pecl-packages/imagick-3.7.0.tgz /root/pecl-packages
COPY pecl-packages/redis-5.3.6.tgz /root/pecl-packages
COPY pecl-packages/rdkafka-6.0.0.tgz /root/pecl-packages

RUN apt-get update && \
    apt-get install -y libzip-dev libxslt-dev libmagickwand-dev default-mysql-client librdkafka-dev && \
    docker-php-ext-install bcmath zip pdo_mysql mysqli opcache pcntl xsl sockets && \
    pecl install /root/pecl-packages/xdebug-3.1.2.tgz &&\
    pecl install /root/pecl-packages/imagick-3.7.0.tgz && \
    pecl install /root/pecl-packages/redis-5.3.6.tgz && \
    pecl install /root/pecl-packages/rdkafka-6.0.0.tgz && \
    pecl install -D 'enable-sockets="yes" enable-openssl="no" enable-http2="yes" enable-mysqlnd="yes" enable-swoole-json="no" enable-swoole-curl="no" enable-cares="no"' /root/pecl-packages/swoole-4.8.12.tgz && \
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