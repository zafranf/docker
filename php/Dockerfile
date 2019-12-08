FROM php:7.3-fpm

ARG DEBIAN_FRONTEND=noninteractive

# UPDATE OS
RUN apt-get update

# INSTALL apt-utils
RUN apt-get install -y apt-utils

# ADD aditional php config
ADD ./conf/php.ini /usr/local/etc/php/conf.d/php.ini

# INSTALL mysql ext
RUN docker-php-ext-install pdo_mysql

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

# CLEAR
RUN apt-get autoremove -y && \
    rm -rf /tmp/*