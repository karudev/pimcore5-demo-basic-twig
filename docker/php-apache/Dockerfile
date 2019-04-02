FROM php:7.1.27-apache-stretch
MAINTAINER Dolyveen Renault <d.renault@karudev-informatique.fr>

COPY etc/php/php.ini /usr/local/etc/php
RUN a2enmod rewrite

# Install vim..
RUN apt-get update && apt-get install -y vim \
    zlib1g-dev \
    libicu-dev \
    g++ \
    libxml2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    wget \
    git \
    libxml2-dev \
    gnupg \
    build-essential \
    libfontconfig1 \
    libxrender1 \
    libbz2-dev \
    #&& docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl

# Install pdo_mysql, zip, soap, mysqli
RUN docker-php-ext-install intl pdo pdo_mysql zip soap mysqli exif bz2

# Install opcache
RUN docker-php-ext-install opcache

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
# Install PHPUNIT
RUN wget https://phar.phpunit.de/phpunit-6.1.phar \
    && chmod +x phpunit-6.1.phar \
	&& mv phpunit-6.1.phar /usr/local/bin/phpunit

#RUN apt-get install xvfb libfontconfig wkhtmltopdf -y
#RUN cd /tmp && wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
#    && tar xvf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
#    && mv wkhtmltox/bin/wkhtmlto* /usr/bin/
