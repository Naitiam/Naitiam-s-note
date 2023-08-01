## 为什么使用CSS预处理

- 前端项目中存在大量重复的代码
- 无法定义变量（当然目前已经支持）, 如果一个值被修改, 那么需要修改大量代码, 可维护性很差; 
- 没有专门的作用域和嵌套, 需要定义大量的id/class来保证选择器的准确性, 避免样式混淆

## 区别

在 LESS 中，不支持像 SCSS 中的 @content 那样直接插入外部样式。

在SCSS中：

```scss
@mixin myMixin {
  color: red;
  @content;
  font-size: 16px;
}

.my-element {
  @include myMixin {
    background-color: blue;
    border: 1px solid black;
  }
}
// 编译后
.my-element {
  color: red;
  background-color: blue;
  border: 1px solid black;
  font-size: 16px;
}
```

## 在Vue环境中使用

> Vue项目中应用预处理器，可以有效减少css代码量。

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

## LESS

>https://less.nodejs.cn/features/

### 变量 

``` less
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

// 编译后
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

### 可变插值

```less
@my-selector: banner;

.@{my-selector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

### 嵌套

使用  `&`  引用父选择器

```less
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

## SCSS

> https://sass-lang.com/guide/

### 变量

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

### 嵌套

使用  `&`  引用父选择器

```scss
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

