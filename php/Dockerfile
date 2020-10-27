FROM php:7.2-fpm

RUN apt-get update && apt-get install -y curl wget libfreetype6-dev libjpeg62-turbo-dev libxslt-dev libicu-dev \
libmcrypt-dev libxml2-dev libssh2-1-dev\
&& docker-php-ext-install -j$(nproc) iconv mbstring intl xsl soap bcmath mysqli pdo_mysql zip \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd

RUN pecl install ssh2-1.1.2;

RUN docker-php-ext-enable ssh2

RUN docker-php-ext-configure intl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

WORKDIR /var/www

CMD ["php-fpm"]
