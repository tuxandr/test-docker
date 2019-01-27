FROM php:7.0-fpm

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        && docker-php-ext-install -j$(nproc) iconv mcrypt mbstring mysqli pdo_mysql zip \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-install opcache \
        && docker-php-ext-enable opcache

COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime
RUN "date"

COPY ./custom-php.ini /usr/local/etc/php/conf.d/custom-php.ini

RUN mkdir -p /var/lib/php/session

RUN chown -R www-data:www-data /var/lib/php/session

RUN chown -R www-data:www-data /var/www/html

CMD ["php-fpm"]