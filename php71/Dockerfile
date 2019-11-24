FROM php:7.1-cli

MAINTAINER Yu-Hsien Chou  <slps970093@gmail.com>

# install modules : GD iconv
RUN apt-get update && apt-get install -y \
        procps \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        openssl \
        libssh-dev \
        libpcre3 \
        libpcre3-dev \
        libnghttp2-dev \
        libhiredis-dev \
        curl \
        wget \
        zip \
        unzip \
        git && \
        apt autoremove && apt clean

# install php ext
RUN docker-php-ext-install \
    iconv \
    gd \
    pdo_mysql \
    mysqli \
    iconv \
    mbstring \
    json \
    opcache \
    sockets \
    pcntl

# enable php ext
RUN docker-php-ext-enable \
    iconv \
    gd \
    pdo_mysql \
    mysqli \
    iconv \
    mbstring \
    json \
    opcache \
    sockets \
    pcntl

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
# install redis
RUN pecl install redis && docker-php-ext-enable redis
# install composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update --clean-backups
# install swoole
RUN pecl install swoole
RUN docker-php-ext-enable swoole
# set Taipei timezone
RUN /bin/cp /usr/share/zoneinfo/Asia/Taipei /etc/localtime && \
    echo 'Asia/Taipei' > /etc/timezone && \
    echo "[Date]\ndate.timezone=Asia/Taipei" > /usr/local/etc/php/conf.d/timezone.ini