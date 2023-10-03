### 介绍一下盒模型？怎么改变盒模型

content + padding +border + margin

正常盒模型：box-sizing: content-box 的宽度 内容宽度+左右padding+左右border

怪异盒模型：box-sizing: border-box  的宽度 包括内容宽度+左右padding+左右border，向内扩展

### 对比 display:none 与 visibility:hidden？

display:none  不占据空间

visibility:hidden  浏览器不渲染元素，占据空间，类似透明度为零

### 为什么使用 less scss ？

[LESS和SCSS使用与区别](../../前端/CSS/LESS和SCSS使用与区别.md)

### flex弹性盒模型的各个属性，flex在实际中的使用

display  

flex-direction  容器中项目的排列方向

flex-wrap 是否换行

justify-content 轴上的对齐方式

align-items 交叉轴上的对齐方式

align-content 定义了多行项目在交叉轴上的对齐方式（仅在多行时生效）。

实际中的使用：比如页面的顶部导航栏

