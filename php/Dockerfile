FROM php:7.3-fpm

ARG DEBIAN_FRONTEND=noninteractive

# UPDATE OS
RUN apt-get update

# INSTALL apt-utils
RUN apt-get install -y apt-utils

# INSTALL mysql ext
RUN docker-php-ext-install pdo_mysql

# INSTALL mysqli ext
RUN docker-php-ext-install mysqli && \
    docker-php-ext-enable mysqli

# INSTALL zip ext
RUN apt-get install -y --no-install-recommends --no-install-suggests libzip-dev zip unzip && \
    docker-php-ext-install zip

# INSTALL git
RUN apt-get install -y --no-install-recommends --no-install-suggests git

# INSTALL composer
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/bin \
    --filename=composer && \
    composer global require hirak/prestissimo

# Add new commands here


# ADD aditional php config
ADD ./conf/php.ini /usr/local/etc/php/conf.d/php.ini

# CLEAN UP
RUN apt-get autoremove -y && \
    rm -rf /tmp/*