FROM php:8.1.8-fpm-bullseye

USER root

RUN apt-get update && apt-get install -y \
            # curl \
            # libmemcached-dev \
            # libz-dev \
            # libpq-dev \
            # libjpeg-dev \
            # libpng-dev \
            # libfreetype6-dev \
            # libssl-dev \
            # libwebp-dev \
            # libmcrypt-dev \
            # libonig-dev; \
        # rm -rf /var/lib/apt/lists/*
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
    # docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install gd 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


COPY ./aliases.sh /root/aliases.sh

RUN sed -i 's/\r//' /root/aliases.sh && \
    echo "" >> ~/.bashrc && \
    echo "# Load Custom Aliases" >> ~/.bashrc && \
    echo "source ~/aliases.sh" >> ~/.bashrc && \
	echo "" >> ~/.bashrc


WORKDIR /var/www