---
title: LESS和SCSS使用与区别
date: 2023-07-25
description: 
tags:
  - LESS
  - SCSS
  - CSS
---

**LSES：https://less.nodejs.cn/features/**

**SCSS：https://sass-lang.com/guide/**

## 为什么使用CSS预处理

- 前端项目中存在大量重复的代码
- 无法定义变量（当然目前已经支持）, 如果一个值被修改, 那么需要修改大量代码, 可维护性很差; 
- 没有专门的作用域和嵌套, 需要定义大量的id/class来保证选择器的准确性, 避免样式混淆

## 在Vue环境中使用

安装

```
# less
pnpm install -D less-loader less
# scss
pnpm install -D sass-loader node-sass
```

使用

```
<styLe Lang="scss">
</style>
<styLe Lang="less">
</style>
```

## 语法差异

### 变量声明

LESS：

``` less
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```

SCSS：

```
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

### 嵌套规则

都可使用  `&`  引用父选择器

```
.card {
  &.title {
    color: red;
      &:hover {
      color: pink;
      }
  }
  >.footer {
    font-size: 12px;
  }
  ，main {
    font-size: 12px;
  }
  &::after {
    content: '';
  }
}
```

### 混合（Mixin）

LESS：

```
.mixin() {
  font-weight: bold;
}

.my-class {
  .mixin();
}
```

SCSS：

```
@mixin mixin {
  font-weight: bold;
}

.my-class {
  @include mixin;
}
```

### 选择器插值

LESS：

```less
@my-selector: banner;
@bg-property: background;

.@{my-selector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}

.my-class {
  @{bg-property}-color: #ff0000;
}
```

SCSS：

```
$bg-property: background;

.my-class {
  #{$bg-property}-color: #ff0000;
}
```

## #使用LESS实现页面的黑白切换效果

简易的

```
// 定义变量
@theme-color: #000;
@text-color: #fff;

// 定义样式类
.black-and-white {
  filter: grayscale(100%);
}

// 定义混合
.text-color(@color) {
  color: @color;
}

// 默认样式
body {
  background: @text-color;
  .text-color(@theme-color);
}

// 黑白切换
.is-black-and-white {
  body {
    background: @theme-color;
    .text-color(@text-color);
  }
}

<body>
  <h1>Hello, World!</h1>
  
  <button onclick="toggleBlackAndWhite()">切换黑白</button>

  <script>
    function toggleBlackAndWhite() {
      document.body.classList.toggle("is-black-and-white");
    }
  </script>
</body>
```



