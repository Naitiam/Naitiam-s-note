### 介绍一下盒模型？怎么改变盒模型

content + padding +border + margin

如果一个元素的内容框宽度为200px，内边距(padding)为10px，边框(border)为2px，外边距(margin)为20px

正常盒模型：box-sizing: content-box 的元素总宽度 = 200px + 10px(padding) + 2px(border) + 20px(margin) = 232px。

怪异盒模型（向内扩展）：box-sizing: border-box 的元素总宽度 = 200px。

box-sizing的其他属性 inherit 继承父

### 对比 display:none 与 visibility:hidden？

display:none  不占据空间

visibility:hidden  浏览器不渲染元素，占据空间，类似透明度为零

### 为什么使用 less scss ？

[LESS和SCSS使用与区别](../../前端/CSS/LESS和SCSS使用与区别.md)

### flex弹性盒模型的各个属性，flex在实际中的使用

display  

flex-direction  容器中项目的排列方向

flex-wrap 是否换行

justify-content 主轴上的对齐方式

align-items 交叉轴上的对齐方式

align-content 定义了多行项目在交叉轴上的对齐方式（仅在多行时生效）。

实际中的使用：比如页面的顶部导航栏

### CSS选择器有哪些？哪些属性可以继承？

**内联(style="")>ID>类=伪类>元素选择器！！** 

CSS选择符：id选择器(#myid)、类选择器(.myclassname)、标签选择器(div, h1, p)、相邻选择器(h1 + p)、子选择器（ul > li）、后代选择器（li a）、通配符选择器（*）、属性选择器（a[rel=”external”]）、伪类选择器（a:hover, li:nth-child）

可继承的属性：font-size, font-family, color

不可继承的样式：border, padding, margin, width, height

### CSS3新增伪类有哪些?

p:first-of-type 选择属于其父元素的首个元素

p:last-of-type 选择属于其父元素的最后元素

p:only-of-type 选择属于其父元素唯一的元素

p:only-child 选择属于其父元素的唯一子元素

p:nth-child(2) 选择属于其父元素的第二个子元素

:enabled :disabled 表单控件的禁用状态

:checked 单选框或复选框被选中

### div垂直上下左右居中

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

### 在哪些场景下⽤过 position 的哪些值，它们分别有什么特性

static（默认）：按照正常文档流进行排列；

relative（相对定位）：不脱离文档流，参考自身静态位置  通过 top, bottom, left, right 定位；

absolute(绝对定位)：参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位；

fixed(固定定位)：所固定的参照对像是可视窗口。

### CSS3有哪些新特性？

RGBA和透明度

background-image background-origin(content-box/padding-box/border-box) background-size background-repeat

word-wrap（对长的不可分割单词换行）word-wrap：break-word

文字阴影：text-shadow：5px 5px 5px #FF0000;（水平阴影，垂直阴影，模糊距离，阴影颜色）

font-face属性：定义自己的字体

圆角（边框半径）：border-radius 属性用于创建圆角

边框图片：border-image: url(border.png) 30 30 round

盒阴影：box-shadow: 10px 10px 5px #888888

### 用纯CSS创建一个三角形的原理是什么？

首先，需要把元素的宽度、高度设为0。然后设置边框样式。

width: 0; height: 0; border-top: 40px solid transparent; border-left: 40px solid transparent; border-right: 40px solid transparent; border-bottom: 40px solid #ff0000;

### 一个满屏品字布局如何设计?

第一种真正的品字：

三块高宽是确定的；

上面那块用margin: 0 auto;居中；

下面两块用float或者inline-block不换行；

用margin调整位置使他们居中。

第二种全屏的品字布局:

上面的div设置成100%，下面的div分别宽50%，然后使用float或者inline使其不换行。

### 行级元素和块元素

行级元素 `span`、`a`、`strong`、`em`、`input`、`button`

块级元素 `div`、`p`、`h1`~`h6`、`ul`、`li`、`header`、`footer`

元素类型转换 display

display: block ，义元素为块级元素

display: inline ，定义元素为行内元素

display: inline-block, 定义元素为行内块级元素。
