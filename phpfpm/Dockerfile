FROM php:7.1-fpm
RUN apt-get update \
 && apt-get install -y \
        git \
        unzip \
        libz-dev \
        aptitude \
        libpng12-dev \
        mysql-client \
        libmcrypt-dev \
        libmemcached-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install -j$(nproc) gd iconv mcrypt pdo_mysql \
 && pecl install xdebug-2.5.5 \
 && pecl install memcached \
 && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini

#COPY usr/local/etc/php-fpm.d/custom.conf /usr/local/etc/php-fpm.d/custom.conf

# install composer
RUN cd '/' \
 && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php composer-setup.php \
 && php -r "unlink('composer-setup.php');" \
 && mv composer.phar /usr/local/bin/composer

WORKDIR /var/www
# install vim-gnome
RUN aptitude install -y vim
