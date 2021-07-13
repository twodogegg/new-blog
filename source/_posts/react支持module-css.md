---
title: react支持module.css
date: 2021-07-13 09:45:07
tags:
  - react
categories:
  - 前端
---

先安装依赖
```shell
yarn add typescript-plugin-css-modules -D
```

配置 ts 插件
```shell
"plugins": [{
    "name": "typescript-plugin-css-modules"
}]
```

vscode 中设置如下配置
```json
{
	"typescript.tsdk": "node_modules/typescript/lib",
	"typescript.enablePromptUseWorkspaceTsdk": true
}
```