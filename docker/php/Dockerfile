FROM php:7.4-fpm
ARG USER_ID

RUN apt-get update \
  && apt-get install -y \
             vim \
             libfreetype6-dev \
             libjpeg62-turbo-dev \
             libmcrypt-dev \
             libpng-dev \
             zlib1g-dev \
             libxml2-dev \
             libzip-dev \
             libonig-dev \
             graphviz \
             libcurl4-openssl-dev \
             pkg-config \
             libpq-dev \
             git \
             curl \
             unzip \
             libmemcached-dev \
             libgeoip-dev \
             geoip-bin \
             geoip-database

RUN pecl install memcached-3.1.3 geoip-1.1.1
RUN docker-php-ext-enable memcached opcache

RUN docker-php-ext-install pdo pdo_mysql mysqli \
  && docker-php-ext-install intl \
  && docker-php-ext-install zip \
  && docker-php-ext-install exif \
  && docker-php-ext-install opcache \
  && docker-php-ext-install bcmath \
  && docker-php-source delete

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-source delete

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN usermod -u ${USER_ID} www-data
USER www-data
WORKDIR /var/www/app