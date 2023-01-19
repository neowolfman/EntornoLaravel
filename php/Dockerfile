FROM php:8.1-fpm-alpine
RUN apk upgrade && \
    apk add bash git sudo openssh libxml2-dev oniguruma-dev autoconf gcc g++ make npm freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev icu-data-full

# PHP: Install php extensions
RUN pecl channel-update pecl.php.net
RUN pecl install pcov ssh2
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install mbstring xml pcntl gd zip pdo pdo_mysql bcmath json 
RUN docker-php-ext-install odbc opcache pdo_dblib pdo_odbc pdo_pgsql pdo_sqlite session snmp sockets
RUN docker-php-ext-enable mbstring xml gd zip pcov pcntl bcmath pdo pdo_mysql json odbc opcache pdo_dblib pdo_odbc pdo_pgsql pdo_sqlite session snmp sockets

RUN curl -sS https://getcomposer.org/installer​ | php -- \
     --install-dir=/usr/local/bin --filename=composer

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY --from=spiralscout/roadrunner:2.4.2 /usr/bin/rr /usr/bin/rr

WORKDIR /var/www/html/

RUN composer install

RUN php artisan key:generate
RUN php artisan storage:link
RUN php artisan optimize
