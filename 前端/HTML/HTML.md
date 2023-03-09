```html
<html></html>      		定义 HTML 文档
<head></head>   			文档的信息
<meta>                    	HTML 文档的元信息
<title></title>        	文档的标题
<link>                      文档与外部资源的关系
<style></style>   		 	文档的样式信息
<body></body>   			可见的页面内容
<!-- -->                 	注释
```

### 行内标签

```html
<img src="图像 URL" alt="图像描述" title="提示文本内容"/>		图片
title 属性 鼠标移到元素上会显示出现一段提示文本
```

``` html
<a href="…">…</a>    	超链接
通过超链接方式访问页面某一位置
定义书签
<a name="书签名称">文字</a>
链接到该书签的超链接
<a href="#书签名称">链接点</a> 
target 属性可以用来规定打开链接文档的位置
属性值	描述
_blank	在新窗口中打开被链接文档。
_self	在相同的框架中打开被链接文档。
_top	在整个窗口中打开被链接文档。
_parent	在父框架集中打开被链接文档。
<a target="_blank|_self|_top|_parent"></a>
<span>...</span>		组合行内元素，以便通过样式来格式化它们
<strong>...</strong>	文字加粗
<b>...</b>              粗体字
<i>...</i>              斜体字 
<em>...</em>            斜体字(强调)
<center>…</center>   	居中文本 
```

----

### 块级标签

```html
<div>...</div>
<h1>...</h1>            标题字大小（h1~h6）
<p>...</p>              分段
属性 align
属性值	说明
left	段落左对齐
right	段落右对齐
center	段落居中对齐
<p style="width: 200px; background-color:rgb(50, 148, 205)" align="center">
列表标签
<ul><li></li> </ul>              无序列表 
<ol><li></li> </ol>              有序列表      
type 属性
disc	实心圆 ●
circle	空心圆 ○
square	实心方块 ■
<ul type="circle|square"></ul> 
自定义列表
dl 标签表示自定义列表，其中的 dt 是代表列表项，而 dd 是列表项的描述
<dl>
  <dt>列表项一</dt>
  <dd>列表项一的描述</dd>
  <dt>列表项二</dt>
  <dd>列表项二的描述</dd>
</dl>
```

----

### 表单标签

```html
<form action="表单提交地址" method="提交方法"></form>
<input type="text" />
常用表单元素：
文本框： text
密码框： password
单选按钮： radio
<input type="radio" name="选项名" value="提交值" />
复选框： checkbox
<input type="checkbox" name="选项名" value="提交值" />
若 name 属性的取值相同，可以实现单选的效果，但 checkbox 不会因为 name 属性的取值相同变成单选
文件按钮： file
<input type="file" name="表单名字" accept="上传文件的格式" />
<input type="file" name="img" accept="image/gif, image/jpg" />
提交按钮： submit
<input type="submit" name="表单名字" value="表单名" />
普通按钮： button
重置按钮： reset
声明一个下拉列表： select
常用属性	描述
multiple	设置下拉列表可以选择多项。
size	设置下拉列表选择几个表项。
下拉列表项：option
常用属性	描述
selected	设置是否被选中。
value	设置列表项的默认值。
<select>
  <option>选项一</option>
  <option>选项二</option>
  <option>选项三</option>
</select>
----------------------------------------------
html5 新表单类型
带验证邮箱功能的文本框： email
输入网址： url
输入数字： number
number类型表单属性	描述
max			输入框允许的最大值。
min			输入框允许的最小值。
step		合法的数字间隔，例如 step=2，则合法为：2、4、6、8。
value		默认值。
一定范围内数值的输入： range
年、月、日： date
年、月、日、本地时间： datetime-local
输入搜索关键字的文本框： search
颜色： color
--新属性--
input 标签新增了一个 form 属性，通过该属性可以将表单元素绑定到指定的 form 标签上，这样就可以灵活进行布局，同时一个表单元素可以从属于多个表单，这就让表单和表单元素的组合变得更加灵活。
input 标签 文本框 autofocus 属性 获得光标焦点
<input type="text" autofocus />
表单属性 autocomplete 属性  当用户输入一次数据过后，再次输入相同的数据时可以自动补全内容。
input 标签 placeholder 属性提示用户设置的输入值
<input placeholder="提示" />
```

```html
    <form autocomplete="on">
        您最喜欢前端技术: <input type="text" list="selectList" />
        <datalist id="selectList">
            <option>html</option>
            <option>css</option>
            <option>js</option>
            <option>vue</option>
        </datalist>
        <input type="submit" />
    </form>
    <form id="myForm1" action="#" method="GET"></form>
    <form id="myForm2" action="#" method="POST"></form>
    提交到 myForm1：<input type="text" form="myForm1" name="myForm1" />
    <input type="submit" value="提交" form="myForm1" />
    提交到 myForm2：<input type="text" form="myForm2" name="myForm2" />
    <input type="submit" value="提交" form="myForm2" />
    <form>
        <p><input type="text" autofocus /></p>
        <p>用户名：<input type="text" placeholder="用户名" /></p>
        <p>密码：<input type="password" /></p>
        <p>邮箱：<input type="email" /></p>
        <p>url: <input type="url" /></p>
        <p>number: <input type="range" /></p>
        date： <input type="date" /> <br />
        datetime-local：<input type="datetime-local" /> <br />
        <p><input type="number" value="5" step="2" /></p>
        <p>color: <input type="color" /></p>
        <p>search: <input type="search" /></p>
        <!-- search 类型和 text 类型的区别?如果使用不同的浏览器去看，就会发现有细微的差异，比如 Chrome 浏览器给 search 类型的输入框提供了清空按钮。
            如果在移动端的话，虚拟键盘会根据不同类型的输入框给出不同的反应。还有就是起到语义化的作用，我们一眼能够明白这里的 input 是起到搜索的效果。 -->
        <p><input type="file" name="img" accept="image/gif, image/jpg" /></p>
        性别：<input type="radio" name="sex" value="male" checked="checked" />男
        <input type="radio" name="sex" value="female" />女 <br />
        爱好：<input type="checkbox" name="hobby" value="basketball" />篮球
        <input type="checkbox" name="hobby" value="football" />足球<br />
        <p>
            学历：
            <select name="edu">
                <option value="0">初中</option>
                <option value="1">高中</option>
                <option value="2">大专</option>
                <option value="3" selected="selected">本科</option>
                <option value="4">硕士</option>
                <option value="5">博士</option>
                <option value="6">其他</option>
            </select>
            就业城市：
            <select name="city" multiple="multiple">
                <option value="A" selected="selected">北京</option>
                <option value="B">上海</option>
                <option value="C">深圳</option>
                <option value="D">广州</option>
                <option value="E">其他</option>
            </select>
        </p>
        <p><input type="reset" /></p>
        <p><input type="button" value="普通按钮" /></p>
        <p><input type="submit" name="submit" value="提交" /></p>
    </form>
```

----

### HTML5 新特性

> HTML5 的语法特征更加明显，可以更加便捷地处理多媒体内容，而且 HTML5 中还结合了其他元素，对原有的功能进行调整和修改，进行标准化工作。

- 新的语义标签，比如 header、nav、section、article、footer。
- **新的表单元素**，比如 calendar、date、time、email、url、search。
- 用于绘画的 canvas 元素。
- 用于媒介回放的 video 和 audio 元素。
- 对本地离线存储的更好支持。
- 地理位置、拖曳、摄像头等 API。

```html
语义化标签
<header></header> 		头部区域
<nav></nav>				导航区域
<article></article> 	内容区域
<section></section> 	文档中部分内容区域
<aside></aside> 		侧边内容栏区域
<footer></footer> 		底部信息区域

多媒体标签
controls 是 controls="controls" 简写形式，用于提供播放、暂停和音量控件。
autoplay 属性：音频自动播放。
loop 属性：音频自动重复播放。
preload 属性：用来缓冲 audio 标签的大文件，它有三个属性值 none（不缓冲）、auto（缓冲音频文件）、metadata （缓冲文件的元数据）。
可以通过子标签 source 来进行多数据源的设置。一个标签可以包含多个 source 标签，当播放器无法识别当前格式的播放源时会调用下一个 source 播放源进行播放。
<video src="URL" poster="封面.png"></video>  标签定义视频(需要定义其属性
poster 属性 给视频添加封面
<video controls>
  <source src="URL" />
</video>
<audio src="URL" controls></audio>    	     标签定义声音(需要定义其属性
<audio>
  <source src="filename.mp3" />
  <source src="filename.ogg" />
</audio>

<canvas id=""></canvas>   				标签定义图形,标签只是图形容器，您必须使用脚本来绘制图形
```


----

### HTML5 本地存储

两种 API，都可以用来存储客户端临时信息，并且二者存储的数据格式均为 key/value 对的数据。

区别在于生命周期，localStorage 除非手动清除，否则会永久保存在客户端，而 sessionStorage 仅仅在当前网页回话下有效，在关闭页面或者浏览器就会被清除。

- localStorage 对象
- sessionStorage 对象

二者提供的方法相同：

| 方法               | 说明                              |
| ------------------ | --------------------------------- |
| setItem(key,value) | 保存数据到本地存储                |
| getItem(key)       | 从本地存储获取数据                |
| removeItem(key)    | 根据指定 key 从本地存储中移除数据 |
| clear()            | 清除所有保存数据                  |

相比本地存储 cookie

- `localStorage` 解决了早期使用 `cookie` 存储遇到的存储空间不足的问题( 每条 `cookie` 的存储空间为 4k )。
- `localStorage` 一般浏览器支持的是 5M 大小，具体存储大小根据浏览器的不同会有所不同。
- 并且相较于 `cookie` 而言，`localStorage` 中的信息不会被传输到服务器。

```javascript
    // 语句 1： 保存数据到本地存储
    localStorage.setItem("ExpireTime", "1527592757");
    localStorage.UserId = "2021008";
    // 语句 2： 根据指定名称获取本地存储中的数据
    var expireTime = localStorage.getItem("ExpireTime");
    console.log(expireTime);
    // 语句 3： 根据指定名称从本地存储中移除
    localStorage.removeItem("ExpireTime");
    // 语句 4： 清除本地存储中所有数据
    localStorage.clear();
    // 语句 1： 保存数据到本地存储
    sessionStorage.setItem("ShopId", "SH1290333211");
    sessionStorage.ShopNumber = "10";
    // 语句 2： 根据指定名称获取本地存储中的数据
    var ShopId = sessionStorage.getItem("ShopId");
    console.log(ShopId);
    // 语句 3： 根据指定名称从本地存储中移除
    sessionStorage.removeItem("ShopId");
    // 语句 4： 清除本地存储中所有数据
    sessionStorage.clear();
```

----

其它

```html
<br/>                   换行
<code>					定义计算机代码文本(......未尝试
<hr>                   	水平线
表格
<table>=</table>   		定义表格
表格边框：border="1"
表格间距：cellspacing="0"
<caption></caption> 	定义表格标题
<col> 				为表格中一个或多个列定义属性值
<th></th>     	  	     	定义表格中的表头单元格
<tr></tr>       	      	定义表格中的行
<td></td>           		定义表格中的单元
跨列：colspan="2"
跨行：rowspan="2"

<label></label>	???

框架(少见不与body共存

<frameset cols=""></frameset>	定义一个框架集
<frame src="" />				定义 frameset 中的一个特定的窗口（框架）
```
