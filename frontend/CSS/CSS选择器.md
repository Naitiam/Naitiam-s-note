[toc]

## CSS哪些属性可以继承？

可继承的属性：font-size, font-family, color

不可继承的样式：border, padding, margin, width, height

## CSS选择器

[css选择器大全]: https://www.w3school.com.cn/cssref/css_selectors.asp

### id选择器(#id)

### 类选择器(.classname)

### 标签选择器(div, h1, p)

>选择所有 <div> 元素和所有<h1> 元素和所有 <p> 元素。

### 相邻选择器(h1 + p)

### 子选择器（ul > li）

### 后代选择器（li a)

> 选择 <li> 元素内的所有 <a> 元素

### 通配符选择器（*）

> 选择所有元素。

```css
*{
    padding:0;
    margin: 0;
}
```

### 属性选择器（a[rel=”external”]）

[属性选择器的使用]: https://www.w3school.com.cn/cssref/selector_attribute.asp

```html
<style>
a[target = "w3c" ]
{
	background-color:yellow;
}
</style>
<a href="http://www.w3school.com.cn" target="w3c">w3school.com.cn</a>

```

### 伪类选择器

> 关于使用的案例。用到再说

a:link 超链接未点击状态

a:hover 光标移到超链接上的状态(未点击)

a:active  点击超链接时的状态

a:visited 被访问后的状态

:first-child

:last-child

p:first-of-type  选择属于其父元素的首个元素

p:last-of-type  选择属于其父元素的最后元素

p:only-of-type  选择属于其父元素唯一的元素

p:only-child  选择属于其父元素的唯一子元素

p:nth-child(2)  选择属于其父元素的第二个子元素

```css
button:nth-child(2)::before{
	content:'aaa';
}
```

:enabled   :disabled  表单控件的禁用状态。

:checked  单选框或复选框被选中。

## CSS选择器优先级？

**内联(style="")>ID>类=伪类>元素选择器！！** 

id选择器 100 

类名选择器 10

伪类选择器 10

标签名选择器 1



