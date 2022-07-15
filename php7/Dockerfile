FROM php:7.4.0-fpm
ARG UID=1000
ARG GID=1000
USER root

WORKDIR /var/www
RUN apt-get update && apt-get install -y \
            libxpm-dev \
            libfreetype6-dev \
            libwebp-dev \
            libjpeg-dev \
            libpng-dev \
            build-essential \
            libssl-dev \
            zlib1g-dev \ 
            libxml2-dev \
            libzip-dev \
            zip \
            curl \
            unzip  
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis
RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install exif \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-source delete
RUN docker-php-ext-configure gd \
            --enable-gd \
            --with-jpeg \
            --with-webp \
            --with-xpm \
            --with-freetype \ 
    && docker-php-ext-install gd 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
