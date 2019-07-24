FROM orsolin/docker-php-5.3-apache

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list


RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    libmcrypt4 \
    libmcrypt-dev \
    php5-mcrypt \
    nano \
    && pecl install xdebug-2.2.7

RUN sed -i -- 's/\/usr\/local\/etc\/php/$PHP_INI_DIR/g' /usr/local/bin/docker-php-ext-enable
RUN docker-php-ext-enable xdebug

RUN php5enmod mcrypt

RUN docker-php-ext-install mcrypt \
    && docker-php-ext-enable mcrypt

RUN docker-php-ext-install bcmath

RUN php5enmod xdebug

RUN apt-get update && apt-get install -y --no-install-recommends \
    libfontconfig-dev \
    libfreetype6-dev \
    libgd3 \
    libjpeg-dev \
    libpng-dev \
    libwebp-dev \
    libtiff-dev \
    libxpm-dev \
    libxt-dev \
    libz-dev \
    libxml2-dev \
    libcurl4-openssl-dev

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html

EXPOSE 80

CMD ["apache2-foreground"]