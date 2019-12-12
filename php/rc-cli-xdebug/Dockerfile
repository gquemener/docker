FROM php:rc-cli-alpine3.10

ENV PHPIZE_DEPS \
        autoconf \
        cmake \
        file \
        g++ \
        gcc \
        libc-dev \
        pcre-dev \
        make \
        git \
        pkgconf \
        re2c

RUN apk add --no-cache --virtual .persistent-deps postgresql-dev
RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS
RUN docker-php-ext-configure pdo_pgsql
RUN docker-php-ext-install -j$(nproc) pdo_pgsql pdo_mysql pcntl opcache
RUN pecl install xdebug
RUN apk del .build-deps && rm -rf /tmp/*
COPY config/xdebug-cli.ini /usr/local/etc/php/conf.d/
COPY config/php.ini /usr/local/etc/php/conf.d/
