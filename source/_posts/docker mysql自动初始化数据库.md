---
title: mysql自动初始化数据库
date: 2021-07-27 16:52:18
tags:
  - docker
  - docker-compose
  - mysql
categories:
  - 其他


## 创建 Dockerfile 文件如下

```
FROM mysql:5.7
COPY sql/*.sql /docker-entrypoint-initdb.d/
```

## 创建sql文件如下



```
DROP DATABASE IF EXISTS `koa`
CREATE DATABASE `koa` CHARACTER SET 'utf8' COLLATE 'utf8_general_ci';
USE koa

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for users
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '用户名',
  `create_time` datetime DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='用户表';

-- ----------------------------
-- Records of users
-- ----------------------------
BEGIN;
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
```

## 创建docker-compose.yml 文件如下

```
version: "3"
services:
    mysql:
        build: ./mysql
        container_name: mysql
        hostname: mysql
        restart: always
        volumes: 
            - ./mysql/data:/var/lib/mysql
            - ./mysql/conf/conf.d:/etc/mysql/conf.d
        ports:
            - "3406:3306"
        environment:
            MYSQL_ROOT_PASSWORD: 123456

```

## 运行测试

使用 `docker-compose up -d 命令启动容器`，然后连接数据库查看就好了


参考链接 https://blog.csdn.net/subfate/article/details/97687739