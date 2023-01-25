FROM php:8.1-fpm-alpine

COPY composer.lock composer.json /var/www/

WORKDIR /var/www/

#install packages
RUN apk update && apk add \
    build-base \
    vim \
    bash \
    curl

# Install extensions for php
RUN curl -sSLf \
    -o /usr/local/bin/install-php-extensions \
    https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions
RUN chmod +x /usr/local/bin/install-php-extensions
RUN install-php-extensions \
    pdo \
    pdo_pgsql \
    xdebug

# Clear cache
RUN rm -rf /var/cache/apk/* && docker-php-source delete


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY --chown=www-data:www-data . /var/www

EXPOSE 9000