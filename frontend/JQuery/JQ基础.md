```
$(selector).each(function(index, element))
$('.option').each(function(){
    $(this).click(function(){
        $(this).addClass('active').siblings().removeClass('active')
    })
})
		<div class="option active">
        </div>
        <div class="option">
        </div>
        <div class="option">
        </div>
        <div class="option">
        </div>
        <div class="option">
        </div>
```

元素选择器

`$("div").css("text-align", "center")`

ID选择器  `$("#id名")`

类选择器  `$(".类名");`

### 伪类选择器

位置伪类选择器：

| 选择器 | 说明                                 |
| ------ | ------------------------------------ |
| :first | 选取指定元素的第一个该元素。         |
| :last  | 选取指定元素的最后一个该元素。       |
| :odd   | 选取指定元素序号为奇数的所有该元素。 |
| :even  | 选取指定元素序号为偶数的所有该元素。 |
| :eq(n) | 选取指定元素的第 n 个该元素。        |
| :lt(n) | 选择指定元素中小于 n 的所有该元素。  |
| :gt(n) | 选取指定元素中大于 n 的所有该元素。  |

可见性伪类选择器：

| 选择器   | 说明                 |
| -------- | -------------------- |
| :visible | 选取所有可见元素。   |
| :hidden  | 选取所有不可见元素。 |

内容伪类选择器：

| 选择器          | 说明                                 |
| --------------- | ------------------------------------ |
| :contains(text) | 对包含指定 text 文本的元素进行操作。 |
| :has(selector)  | 对包含指定选择器的元素进行操作。     |
| :parent         | 对含有文本或者子元素的元素进行操作。 |
| :empty          | 对空元素进行操作。                   |

表单对象属性选择器：

| 选择器     | 说明                         |
| ---------- | ---------------------------- |
| :checked   | 选取所有被选中的表单元素。   |
| :selected  | 选取被选中的表单元素项。     |
| :enabled   | 选取所有可用的表单元素。     |
| :disabled  | 选取所有不可用的表单元素。   |
| :read-only | 选取只读权限的表单元素。     |
| :focus     | 选取所有获得焦点的表单元素。 |

DOM操作

元素插入：

- 子级插入方法，包括 `prepend()`、`prependTo()`、`append()`、`appendTo()`。
- 同级插入方法，包括 `before()`、`insertBefore()`、`after()`、`insertAfter()`。

删除元素：

- `remove()`
- `empty()`

获取指定元素的属性值：

- `attr()`
- `removeAttr()`

样式操作：

- `css()`
- `addClass ()`
- `removeClass()`
- `toggleClass()`

内容操作：

- `html()`
- `text()`
- `val()`  获取表单

### 动画

`$(this).show(2000)`  显示

`$(this).hide(2000)`  隐藏

淡入与淡出

` $().fadeIn(speed, easing, callback); `

` $().fadeOut(speed, easing, callback);`

`$(this).fadeIn(500);`

自定义动画

`$().animate({ style }, speed, callback);`

```
$("div").animate({ left: "+=100px" }).animate({fontSize:"25px"},1000,function(){
	$("#title").css({"background-color":"yellow"})
});
```

停止动画

`$("div").stop();`

延迟动画

`$("div").delay(3000).animate({ "background-color": "#ddffbc" });`

### 查找

查找祖先元素

- `$().parent()` 方法是用来查找指定元素的父元素的。
- `$().parents()` 方法是用来查找指定元素的所有祖先元素的。

查找兄弟元素

```
$().prev(); // 查找指定元素前向第一个元素 
$().preAll(); // 查找指定元素前向所有元素
$().next(); // 查找指定元素的第一个后向兄弟元素 
$().nextAll(); // 查找指定元素的所有后向兄弟元素
$().siblings(); //查找所有兄弟元素
```

查找后代元素

`$(this).children("#title")`

`$(this).children()`

`$(this).find("li")`

### 过滤元素

类名过滤

`$().hasClass("类名");`

下标过滤

`$().eq(n);`

`$li.eq(2).css("color", "#77acf1");`

判断过滤

` $("div").is(":animated");`  判断当前 div 元素是否处于动画状态

反向过滤

```
        $("div").click(function () {
          $(this).not(".div2").css("background", "#ffc478");
        });
```

### AJAX

load() 方法让 AJAX 去请求服务器，并从中获得数据，最后将获得的数据放入到指定的元素中。

`$().load(url, data, callback);`

```
      $(function () {
        $(".text").load("text.txt"); // 获取 text.txt 文件中的数据
      });
      $(".text").load("text.txt", function (response, status, xhr) {
          $("p").text(
            "请求结果为：" + response + "；" + "请求状态为：" + status
          );
      });
      
```

` get` 方法是通过 HTTP GET 请求从服务器请求数据

`$.get(url, data, callback(data, status, xhr), dataType);`

```
          $.get("food.html", function (data, status) {
            $("div").html(data);
            $("p").append(status);
          });
```

`post` 方法是用的 POST 请求，它向指定资源提交数据进行处理请求，该请求不会被缓存。

`$.post(url, data, callback(data, textStatus, jqXHR), dataType);`

- `url`：是请求的 url，它是必须参数。
- `data`：是发送到服务器的数据，它是可选参数。
- `callback`：是当请求成功时的回调函数，该方法包含三个参数，`data` 是请求的结果数据，`textStatus` 是包含请求的状态，`jqXHR` 是 `XMLHttpRequest` 对象。
- `dataType`：是服务器返回的数据格式，如 xml、html、json 等。

```
          $.post(
            "https://jsonplaceholder.typicode.com/posts",
            function (data, textStatus) {
              $("p").append(textStatus);
            }
          );
```

post 和 get 有个明显的区别，使用 POST 请求，提交的数据不会显示到 URL 上，查看历史记录不会看到提交的数据。而 GET 请求，则相反，它提交的数据会显示在 URL 上，并且查看历史记录可以看到提交的数据。

```
      $(function () {
        $.get(
          "https://jsonplaceholder.typicode.com/users",
          {
            id: "2",
            name: "Cici",
          },
          function (data, success) {
            $("div").text("请求状态：" + success);
          }
        );
        $.post(
          "https://jsonplaceholder.typicode.com/users",
          {
            id: "3",
            name: "Lee",
          },
          function (data, success) {
            $("p").text("请求状态：" + success);
          }
        );
      });
```

#### ajax 方法

```
$.ajax({ 配置项 });
```

| 参数        | 类型             | 描述                                                         |
| ----------- | ---------------- | ------------------------------------------------------------ |
| url         | String           | 发送请求地址，默认为当前页面地址。                           |
| type        | String           | 请求数据的方式（POST 或 GET），默认为 GET。                  |
| timeout     | Number           | 设置请求超时的时间，其单位为毫秒。                           |
| data        | Object 或 String | 发送到服务器的数据。                                         |
| dataType    | String           | 服务器返回的数据类型。                                       |
| beforeSend  | Function         | 发送请求前可以修改的 XMLHttpRequest 对象的函数。             |
| complete    | Function         | 请求完成后的回调函数，这里的回调函数无论请求成功或者失败都会被调用。 |
| success     | Function         | 请求成功后的回调函数。                                       |
| error       | Function         | 请求失败后被调用的函数。                                     |
| contentType | String           | 发送信息至服务器时内容的编码形式。                           |
| async       | Boolean          | 设置请求方式，当值为 true 时，所有请求为异步请求；当值为 false 时，所有请求为同步请求，默认值为 true。 |
| cache       | Boolean          | 设置浏览器是否缓存当前页面，当值为 true 时浏览器会缓存该页面，反之不会，默认值为 false。 |

### 遍历

遍历对象	`$.each( {}, ( key, value ) => {} )`

遍历数组  `$.each( [], ( index, item ) => {} )`



