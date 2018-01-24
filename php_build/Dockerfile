FROM php:7.0-fpm

#RUN apt-get update && apt-get install -my wget gnupg
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
        vim 
        #libpng-dev \
        #libjpeg62-turbo-dev \
        #libfreetype6-dev \
        #libpng12-dev \
        #zlib1g-dev=1:1.2.8.dfsg-2+b1

RUN docker-php-source extract \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install pdo_mysql \
    #&& docker-php-ext-configure gd \
    #    --with-gd \
    #    --with-freetype-dir=/usr/include/ \
    #    --with-png-dir=/usr/include/ \
    #    --with-jpeg-dir=/usr/include/ \
    #&& docker-php-ext-install gd \
    && curl -L https://pecl.php.net/get/redis-3.1.3.tgz >> /usr/src/php/ext/redis.tgz \
    && tar -xf /usr/src/php/ext/redis.tgz -C /usr/src/php/ext/ \
    && rm /usr/src/php/ext/redis.tgz \
    && docker-php-ext-install redis-3.1.3 \
    && docker-php-source delete
