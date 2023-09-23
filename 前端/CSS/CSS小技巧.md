[toc]

[CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS)

### 文本样式

文本阴影：text-shadow: 5px 5px 2px red;

文本字加线：text-decoration: underline;

首行缩进：text-indent: 2em;

=========================================================================

### div居中

margin:0 auto

```
  用在父组件上
  display: flex;
  justify-content: center;
  align-items: center;
```

定位+transform

```
.parent {
	width: 300px;
	height: 300px;
	border: 1px solid pink;
	position: relative;
}

.son {
	width: 100px;
	height: 100px;
	background-color: red;
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
}
```

定位+margin:auto

```
.parent {
	width: 300px;
	height: 300px;
	border: 1px solid pink;
	position: relative;
}

.son {
	width: 100px;
	height: 100px;
	background-color: red;
	position: absolute;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	margin: auto;
}
```

使用flex布局+margin:auto

```
.parent {
	width: 300px;
	height: 300px;
	border: 1px solid pink;
	display: flex;
}

.son {
	width: 100px;
	height: 100px;
	background-color: red;
	margin: auto;
}

```

https://blog.csdn.net/qq_40951289/article/details/104621645

=========================================================================

### 文字居中

居中 text-align:center

上下居中height + line-heigh

=========================================================================

### 圆角边框：border-radius:100%;

=========================================================================

### z-index只对定位元素奏效 

z-index 属性设置元素的堆叠顺序 ,数值越大越在最上层，仅能在定位元素上奏效（例如 position:absolute;）

=========================================================================

### 标准CSS盒模型

标准盒子模型：宽度=内容的宽度（content）+ border + padding + margin

低版本IE盒子模型：宽度=内容宽度（content+border+padding）+ margin

=========================================================================

### box-sizing 属性

box-sizing: content-box|border-box|inherit:

| 值          | 说明                                                         |
| :---------- | :----------------------------------------------------------- |
| content-box | 默认值。如果你设置一个元素的宽为 100px，那么这个元素的内容区会有 100px 宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。 |
| border-box  | 告诉浏览器：你想要设置的边框和内边距的值是包含在 width 内的。也就是说，如果你将一个元素的 width 设为 100px，那么这 100px 会包含它的 border 和 padding，内容区的实际宽度是 width 减 去(border + padding) 的值。大多数情况下，这使得我们更容易地设定一个元素的宽高。 **注：**border-box 不包含 margin。 |
| inherit     | 指定 box-sizing 属性的值，应该从父元素继承                   |

=========================================================================

### 背景透明度

background-color: rgba(255, 0, 0, 0.3);

=========================================================================

### 光标属性cursor: pointer;

光标呈现为指示链接的指针（一只手）

https://www.runoob.com/cssref/pr-class-cursor.html

=========================================================================

### 行内块元素和块元素

行内元素不可以设置宽高，宽度高度随文本内容的变化而变化，但是可以设置行高（line-height），同时在设置外边距margin上下无效，左右有效，内填充padding上下无效，左右有效

行级元素和块级元素

1. 行级元素不会自动换行，块级元素自带换行

2. 行级元素设置宽高无效，块级元素宽高随便设

3. 行级元素左右外边距有效，上下外边距无效，块级元素上下左右都有效

行级元素 input img smalii i b br span textarea

块级元素



