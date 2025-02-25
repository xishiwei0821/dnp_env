# DOCKER  本地运行环境

#### 介绍
docker环境 docker + nginx + php + mariadb + redis + rabbitmq + mongodb

~~ 目前php环境尚未配置扩展，如需要安装扩展，手动配置或者进入php容器进行安装 ~~

####  添加php Dockerfile文件，编译一些常用扩展。
- pdo_mysql
- bcmath
- gettext
- pcntl
- sockets
- zip
- gd
- swoole
- redis
- xlswriter
- composer

#### 安装教程

1.  克隆代码

``` bash
    git clone <git地址>
```

3. 配置文件

``` bash
    # 复制 .env.sample .env 添加配置文件
```

4.  docker compose运行

``` bash
    docker-compose up -d

    # 如果运行慢 配置文件中配置镜像源
    "registry-mirrors": [
        "https://registry.docker-cn.com",
    ]
    
```

#### php扩展配置

### 以下内容已加入到php Dockerfile中，无需配置。

``` bash
    # 先进入到php容器内部
    docker exec -it <docker-name> /bin/bash

    # 更新apt包
    apt update

    # 安装常用（pdo_mysql,bcmath,gettext,pcntl,sockets）
    docker-php-ext-install pdo_mysql bcmath gettext pcntl sockets

    # 安装zip扩展
    apt install -y libzip-dev
    docker-php-ext-install zip

    # 安装gd库并配置freetype
    apt install -y libpng-dev libjpeg-dev libwebp-dev libfreetype-dev
    docker-php-ext-configure gd --with-php-config=/usr/local/bin/php-config --with-freetype --with-jpeg --with-webp
    docker-php-ext-install gd

    # 安装swoole
    pecl install swoole
    # 如果版本过低，无法安装最新版
    pecl install https://pecl.php.net/get/swoole-4.8.10.tgz
    # 安装redis
    pecl install redis
    # 安装xlswriter
    pecl install xlswriter

    # 安装supervisor
    apt install -y supervisor
    supervisord -c /etc/supervisor/supervisord.conf

    # pecl安装的扩展，需要在php.ini中添加
    extension=swoole
    extension=redis
    extension=xlswriter

    # 安装composer
    php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    mv composer.phar /usr/local/bin/composer
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```
