---
title: docker打包node.js
date: 2021-07-21 10:15:40
tags:
  - docker
  - node.js
categories:
  - node.js
  - 其他

---

### 在node.js 项目中创建 `Dockerfile` 文件

内容如下
```
FROM node

RUN mkdir -p /opt/app
WORKDIR /opt/app

# Bundle app source
COPY . /opt/app
RUN npm install

EXPOSE 3000
CMD [ "node", "app.js" ]

```