FROM php:8.1-fpm-alpine

RUN apk update && apk upgrade && \
    apk add --no-cache bash git sudo openssh libxml2-dev oniguruma-dev autoconf gcc g++ \ 
        make npm freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev icu-data-full nodejs

RUN apk add --no-cache --update \
  bzip2-dev \
  enchant2-dev \
  libpng-dev \
  gmp-dev \
  imap-dev \
  icu-dev \
  openldap-dev \
  freetds-dev \
  postgresql-dev \
  aspell-dev \
  net-snmp-dev \
  libxml2-dev \
  tidyhtml-dev  \
  libxslt-dev \
  libzip-dev

RUN docker-php-source extract
# PHP: Install php extensions
RUN pecl channel-update pecl.php.net
RUN pecl install pcov ssh2
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install \
  bcmath \
  bz2 \
  calendar \
  dba \
  enchant \
  exif \
  ffi \
  gd \
  gettext \
  gmp \
  imap \
  intl \
  ldap \
  mysqli \
  opcache \
  pcntl \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  pspell \
  shmop \
  snmp \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \
  tidy \
  xsl \
  zend_test \
  zip

RUN docker-php-ext-install mbstring xml pdo 
RUN docker-php-ext-enable mbstring xml pdo bcmath \
  bz2 \
  calendar \
  dba \
  enchant \
  exif \
  ffi \
  gd \
  gettext \
  gmp \
  imap \
  intl \
  ldap \
  mysqli \
  opcache \
  pcntl \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  pspell \
  shmop \
  snmp \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \
  tidy \
  xsl \
  zend_test \
  zip

#RUN curl -sS https://getcomposer.org/installer​ | php -- --install-dir=/usr/local/bin --filename=composer

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN chmod 2775 /var/www/html
#RUN chmod o+w /var/www/html/storage/ -R
RUN rm -rf /var/www/html/public/storage

WORKDIR /var/www/html/

#CMD ["php", "artisan", "key:generate"]
#CMD ["php", "artisan storage:link"]
#CMD ["php", "artisan config:cache"]
#CMD ["php", "artisan route:cache"]
#CMD ["php-fpm", "artisan optimize"]

