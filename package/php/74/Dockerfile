# 使用镜像
FROM php:7.4-fpm

# 设置工作目录
WORKDIR /code

COPY ./extension/ /tmp/extensions

# 生产环境
RUN apt-get update && apt install -y libzip-dev libpng-dev libfreetype-dev libjpeg-dev libwebp-dev libpq-dev \
    && docker-php-ext-configure gd --with-php-config=/usr/local/bin/php-config --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install pdo_mysql pdo_pgsql bcmath gettext pcntl sockets zip gd \
    && pecl install /tmp/extensions/redis/redis-6.2.0.tgz \
    && pecl install /tmp/extensions/xlswriter/xlswriter-1.5.8.tgz \
    && pecl install /tmp/extensions/swoole/swoole-4.8.10.tgz \
    && php /tmp/extensions/composer/composer-setup-2.8.10.php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 开发环境(方便调试，建议使用生产环境，构建docker镜像缓存层更少，体积更小)
# RUN apt-get update && apt install -y libzip-dev libpng-dev libfreetype-dev libjpeg-dev libwebp-dev libpq-dev
# RUN docker-php-ext-configure gd --with-php-config=/usr/local/bin/php-config --with-freetype --with-jpeg --with-webp && docker-php-ext-install pdo_mysql pdo_pgsql bcmath gettext pcntl sockets zip gd
# RUN pecl install /tmp/extensions/redis/redis-6.2.0.tgz
# RUN pecl install /tmp/extensions/xlswriter/xlswriter-1.5.8.tgz
# RUN pecl install /tmp/extensions/swoole/swoole-4.8.10.tgz
# RUN php /tmp/extensions/composer/composer-setup-2.8.10.php && mv composer.phar /usr/local/bin/composer && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
