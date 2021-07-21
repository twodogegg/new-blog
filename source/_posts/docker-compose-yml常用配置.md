---
title: docker-compose.yml常用配置
date: 2021-07-21 08:55:42
tags:
  - docker
  - docker-compose
categories:
  - 其他

---

### image

声明所使用的镜像

```
image: node
```

### hostname

声明在本容器中对应的 host 地址

```
# redis 容器
hostname: redis

## 其他容器
environment:
  - REDIS_URL=redis://redis:6379/
```

### restart

声明重启的选项

```
# 总是会自动重启
restart: always
```

### environment
声明环境变量
```
environment:
  - NODE_ENV=testing
```

在 `node.js` 中使用

```js
console.log(process.env)
```

### stdin_open, tty

运行使用进入容器
```
stdin_open: true
tty: true
```

### depends_on

要再该容器启动后再启动
```
depends_on:
      - redis
```

### volumes

声明文件映射关系

```
volumes:
    - ./data:/var/data
```

### command
容器启动后所执行的命令

```
command: ["redis-server", "--appendonly", "no"]
```

[执行多行命令](https://blog.csdn.net/biao0309/article/details/105318240)