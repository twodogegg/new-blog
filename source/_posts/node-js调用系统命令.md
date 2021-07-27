---
title: node.js调用系统命令
date: 2021-07-27 09:20:46
tags:
    - node.js
categories:
    - 前端
---

### node.js 调用系统命令

一般我用这个方法 

```
import { exec } from 'child_process'

exec("ls", ((error, stdout, stderr) => {
  if (error) {
    console.log(error)
  } else {
    console.log(stdout)
  }
}))

```