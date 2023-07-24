安装

```
pnpm i vitepress -d
```

 package.json添加script

```
 "scripts": {
    "docs:dev": "vitepress dev docs",
    "docs:build": "vitepress build docs",
    "docs:serve": "vitepress serve docs"
  }
```

启动本地站点

```
pnpm run docs:dev
```

再 *.vuepress* 文件夹下创建 `config.js` 配置文件，配置主页面标题和描述

```
export default {
  title: 'maitui', //站点标题
  description: '一个vue3组件库',//mate标签description，多用于搜索引擎抓取摘要
}
```

当前目录结构如下

```
.
├─ docs
│  ├─ .vitepress
│  │  ├─ cache...
│  │  └─ config.js
│  └─ index.md
└─ package.json
```



