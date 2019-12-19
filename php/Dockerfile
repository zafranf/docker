FROM php:7.3-fpm

ARG DEBIAN_FRONTEND=noninteractive

# UPDATE OS
RUN apt-get update

# INSTALL apt-utils
RUN apt-get install -y apt-utils

# INSTALL mysql ext
RUN docker-php-ext-install pdo_mysql

# INSTALL zip ext
RUN apt-get install -y --no-install-recommends --no-install-suggests libzip-dev zip unzip && \
    docker-php-ext-install zip

# INSTALL imap ext
RUN apt-get install -y --no-install-recommends --no-install-suggests libc-client-dev libkrb5-dev && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

# INSTALL swoole ext
RUN git clone https://github.com/swoole/swoole-src.git -b v4.4.12 && \
    cd swoole-src && \
    phpize && \
    ./configure --enable-openssl && \
    make && make install && \
    docker-php-ext-enable swoole

# INSTALL git
RUN apt-get install -y --no-install-recommends --no-install-suggests git

# INSTALL composer
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/bin \
    --filename=composer

# INSTALL mongodb ext
RUN apt-get install -y libcurl4-openssl-dev pkg-config libssl-dev && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb

# INSTALL supervisor
RUN apt-get install -y --no-install-recommends --no-install-suggests supervisor

# Add new commands here

# ADD aditional php config
ADD ./conf/php.ini /usr/local/etc/php/conf.d/php.ini

# CLEAN UP
RUN apt-get autoremove -y && \
    rm -rf /tmp/*