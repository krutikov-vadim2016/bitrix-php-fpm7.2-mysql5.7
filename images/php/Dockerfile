# Для начала указываем исходный образ, он будет использован как основа
FROM php:7.2-fpm

# Необязательная строка с указанием автора образа
MAINTAINER PHPtoday.ru <info@phptoday.ru>

# RUN выполняет идущую за ней команду в контексте нашего образа.
# В данном случае мы установим некоторые зависимости и модули PHP.
# Для установки модулей используем команду docker-php-ext-install.
# На каждый RUN создается новый слой в образе, поэтому рекомендуется объединять команды.
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
	libmemcached-dev \
	libzip-dev \
    && docker-php-ext-install -j$(nproc) mbstring mysqli pdo_mysql zip opcache \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Куда же без composer'а.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Добавим свой php.ini, можем в нем определять свои значения конфига
ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini
ADD php-fpm.d/www.conf /usr/local/etc/php-fpm.d/www.conf

# Указываем рабочую директорию для PHP
WORKDIR /var/www
RUN chown -R 33:33 /var/www /tmp

# Запускаем контейнер
# Из документации: The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, 
# or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
CMD ["php-fpm"]
