FROM php:5.6-fpm

RUN set -xe \
# Dependence
  && buildDeps=" \
    git \
    build-essential \
    php5-dev \
    php5-mysql \
	php5-xmlrpc \
	libxml2 \
	libxml2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libpcre3-dev \
  " \

# Install env
ADD sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y ${buildDeps} --no-install-recommends \
	
# Install PHP extensions
COPY extensions/redis.tgz /home/redis.tgz
COPY extensions/xdebug.tgz /home/xdebug.tgz
COPY extensions/xhprof.tgz /home/xhprof.tgz

RUN  docker-php-ext-install zip mbstring mcrypt mysql mysqli pdo_mysql\
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install gd
RUN pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
        && pecl install /home/xhprof.tgz && echo "extension=xhprof.so" > /usr/local/etc/php/conf.d/xhprof.ini \
        && pecl install /home/xdebug.tgz && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/xdebug.ini
		
# PHP config
ADD php.ini /usr/local/etc/php/php.ini
ADD php-fpm.conf /usr/local/etc/php-fpm.conf

#Composer
ADD extensions/composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer

WORKDIR /www-root

# Write Permission
RUN usermod -u 1000 www-data

# php-fpm:8000 xdebug:9000
EXPOSE 8000 9000
VOLUME ["/www-root"]