FROM php:8.1.0-fpm

USER root
WORKDIR /var/www/api.thamelmart.test
RUN apt-get update && apt-get install -y \
            libpng-dev \
            zlib1g-dev \ 
            libxml2-dev \
            libzip-dev \
            zip \
            curl \
            unzip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-source delete

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# RUN composer install