FROM php:7.0-fpm

COPY ./redis.tgz /usr/src/php/ext/
COPY ./sources.list /etc/apt/
RUN cat /etc/apt/sources.list

RUN apt-get update -y \
    && apt-get install -y \
        git \
        zip \
        vim \
        alien \
        libfreetype6-dev \
        libmcrypt-dev \
        libpng12-dev \
        libjpeg-dev \
        libpng-dev \
        zlib1g-dev \
        zlib1g=1:1.2.8.dfsg-2+b1 --allow-downgrades \
        #pdftk

RUN docker-php-source extract \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include \
        --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd \
    && tar -xf /usr/src/php/ext/redis.tgz -C /usr/src/php/ext/ \
    && docker-php-ext-install redis-3.1.3
    #&& docker-php-source delete

#ADD ./oracle-instantclient-basic-10.2.0.5-1.x86_64.rpm /tmp/oracle-instantclient-basic-10.2.0.5-1.x86_64.rpm
#ADD ./oracle-instantclient-devel-10.2.0.5-1.x86_64.rpm /tmp/oracle-instantclient-devel-10.2.0.5-1.x86_64.rpm
#RUN alien -i /tmp/oracle-instantclient-basic-10.2.0.5-1.x86_64.rpm
#RUN alien -i /tmp/oracle-instantclient-devel-10.2.0.5-1.x86_64.rpm

#RUN ln -s /usr/include/oracle/10.2.0.5/client64 /usr/include/oracle/10.2.0.5/client
#RUN ln -s /usr/lib/oracle/10.2.0.5/client64 /usr/lib/oracle/10.2.0.5/client

#ENV LD_LIBRARY_PATH /usr/lib/oracle/10.2.0.5/client64/lib
#ENV ORACLE_HOME /usr/lib/oracle/10.2.0.5/client64
#ENV PATH $PATH:$ORACLE_HOME/bin:$ORACLE_HOME/lib
#ENV TNS_ADMIN $ORACLE_HOME/network/admin
#COPY ./oci8-2.1.8.tgz /tmp/oci8-2.1.8.tgz

#RUN cd /tmp && tar -xzf oci8-2.1.8.tgz \
#    && cd oci8-2.1.8 && phpize \
#    && ./configure --with-oci8=shared,instantclient,/usr/lib/oracle/10.2.0.5/client64/lib --with-php-config=/usr/local/bin/php-config \
#    && make && make install
#COPY ./pdo_oci /tmp/pdo_oci
#RUN cd /tmp/pdo_oci && phpize \
#    && ./configure --with-php-config=/usr/local/bin/php-config --with-pdo-oci=instantclient,/usr/,10.2.0.5 \
#    && make && make install
#RUN docker-php-ext-enable oci8 && docker-php-ext-enable pdo_oci

#COPY ./oracle.sh /etc/profile.d/
