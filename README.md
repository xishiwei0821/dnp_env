# DOCKER  本地运行环境

#### 介绍
docker环境 docker + nginx + php + mariadb + redis + rabbitmq + mongodb
目前php环境尚未配置扩展，如需要安装扩展，手动配置或者进入php容器进行安装

```
    docker exec -it <php容器名> /bin/bash
```

#### 软件架构


#### 安装教程

1.  克隆代码

```
    git clone https://jihulab.com/xishiwei1/dnmp_environment.git
```

2.  docker compose运行

```
    docker-compose up -d
```
