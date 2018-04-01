FROM php:7.0-fpm

#RUN apt-get update && apt-get install -my wget gnupg
COPY ./redis.tgz /usr/src/php/ext/
COPY ./sources.list /etc/apt/
RUN cat /etc/apt/sources.list
#RUN apt-key adv --recv-keys --keyserver mirrors.aliyun.com 40976EAF437D05B5
#RUN apt-key adv --recv-keys --keyserver mirrors.aliyun.com 3B4FE6ACC0B21F32

#RUN apt-key adv --keyserver mirrors.aliyun.com --recv-keys 40976EAF437D05B5
#RUN apt-key adv --keyserver mirrors.aliyun.com --recv-keys 3B4FE6ACC0B21F32
RUN apt-get update -y \
    && apt-get install -y \
        git \
        zip \
        vim \
        alien
        #libpng-dev \
        #libjpeg62-turbo-dev \
        #libfreetype6-dev \
        #libpng12-dev \
        #zlib1g-dev=1:1.2.8.dfsg-2+b1
        #software-properties-common
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN docker-php-source extract \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install bcmath \
    && apt-get install -y \
        libfreetype6-dev \
        libmcrypt-dev \
        libpng12-dev \
        libjpeg-dev \
        libpng-dev \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && tar -xf /usr/src/php/ext/redis.tgz -C /usr/src/php/ext/ \
    && rm /usr/src/php/ext/redis.tgz \
    && docker-php-ext-install redis-3.1.3 \
    && docker-php-ext-install opcache \
    && docker-php-source delete

#ADD ./oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
#ADD ./oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm

#RUN alien -i /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
#RUN alien -i /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm
#RUN pear config-set http_proxy http://myproxy.us.oracle.com:80/
#RUN pecl channel-update pecl.php.net
#RUN pear config-show
#RUN pecl install oci8-1.3.4.tgz
#RUN pecl install oci8
#RUN docker-php-ext-enable oci8
