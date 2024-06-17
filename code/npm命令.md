---
title: npm命令
date: 2023-09-07
description: 
tags: []
---

`--save-dev` 和 `-D` 是用于将**开发依赖**添加到 `package.json` 中的 npm 命令选项，两者用法相同

## 报错解决

### NPM install报错certificate has expired

![image-20240122170913851](img/npm命令.assets/image-20240122170913851.png)

原因：网络做了代理

解决：取消ssl验证

```
npm config set strict-ssl false
```