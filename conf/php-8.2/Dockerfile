# 使用镜像
FROM php:8.2-fpm

# 设置工作目录
WORKDIR /code

# 安装扩展
RUN apt-get update && apt install -y libzip-dev libpng-dev libfreetype-dev libjpeg-dev libwebp-dev \
    && docker-php-ext-install pdo_mysql bcmath gettext pcntl sockets zip \
    && docker-php-ext-configure gd --with-php-config=/usr/local/bin/php-config --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install gd && pecl install redis && pecl install xlswriter \
    && pecl install swoole \
    && php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer
