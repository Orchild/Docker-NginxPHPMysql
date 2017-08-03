FROM php:5.6-fpm

# PHP config
COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/php-fpm.conf

#Composer
COPY extensions/composer.phar /usr/local/bin/composer

# Install env
COPY sources.list /etc/apt/sources.list

# Install PHP extensions
COPY extensions/redis.tgz /home/redis.tgz
COPY extensions/xdebug.tgz /home/xdebug.tgz
COPY extensions/xhprof.tgz /home/xhprof.tgz

RUN apt-get update
    && apt-get install -y \
        git \
        zlib1g-dev \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-install zip
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql\
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd
    && pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    && pecl install /home/xhprof.tgz && echo "extension=xhprof.so" > /usr/local/etc/php/conf.d/xhprof.ini \
    && pecl install /home/xdebug.tgz && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && chmod 755 /usr/local/bin/composer \
    # Write Permission
    && usermod -u 1000 www-data

WORKDIR /www-root

# php-fpm:8000 xdebug:9000
EXPOSE 8000 9000
VOLUME ["/www-root"]