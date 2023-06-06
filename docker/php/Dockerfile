FROM php:8.2-fpm
COPY php.ini /usr/local/etc/php/
EXPOSE 5173

RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev \
  && docker-php-ext-install zip pdo_mysql

# Composer installation
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# Install Node.js and npm
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

# RUN composer global require "laravel/installer"

# RUN apt-get update \
#   && apt-get -y install \
#   git \
#   zip \
#   unzip \
#   vim \
#   && docker-php-ext-install pdo_mysql bcmath

WORKDIR /var/www/laravel-project

# COPY --from=node:16 /usr/local/bin /usr/local/bin
# COPY --from=node:16 /usr/local/lib /usr/local/lib
