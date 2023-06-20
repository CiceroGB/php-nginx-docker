FROM php:8.1-fpm-alpine

# Install dependencies
RUN apk add --no-cache \
    libzip-dev \
    zip \
    linux-headers

# Install PHP Extensions
RUN docker-php-ext-install zip

# Install Xdebug
RUN apk add --no-cache $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug


ENV COMPOSER_ALLOW_SUPERUSER=1
# Install Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY ./php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# WORKDIR /app
COPY ./app /var/www/html

# Install PHP dependencies
RUN composer install

