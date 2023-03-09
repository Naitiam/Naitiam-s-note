`console.log()  `控制台输出

`alert() `  对话框

`confirm() ` 确认框

`prompt("文本",“默认输入文本”) ` 输入框

`parseFloat()`  将字符串转换为浮点型

`parseInt()`    将字符串转换为整型 

| number | object | undefined |
| ------ | ------ | --------- |
| NaN    | null   | undefined |

自定义函数   `function 函数名(params) {}`

调用函数  `事件名=“函数名()”`

匿名函数  `function(){}`

**数据类型**

- **基本数据类型**：字符串（string）、数字（number）、布尔（boolean）、空（null）、未定义（undefined）。
- **引用数据类型**：对象（object）。

查看数据类型  `typeof`  关键字

全等（===）	当全等号左右两边的操作数相等且类型相同时，返回 true。

**运算符与表达式**

- 算术运算符：+、-、*、/、%、++、--
- 比较运算符：>、<、>=、<=、==、!=、===、!==
- 赋值运算符：=、+=、-=、*=、/=
- 逻辑运算符：&&、||、!
- 条件运算符：条件表达式 ? 表达式 1 : 表达式 2

## DOM文档对象模型

> Document Object Model（文档对象模型），它是浏览器为每个窗口内的 HTML 页面创建的一个 document 对象来对页面的元素进行操作。

### DOM获取元素对象  

`document.getElementById()`

`document.getElementsByTagName()`

`document.getElementsByClassName()`

`document.getElementsByName()`

`document.querySelector()`

`document.querySelectorAll()`

`document.write()`

### DOM事件 ! ! !

[HTML DOM 事件对象 | 菜鸟教程 (runoob.com)](https://www.runoob.com/jsref/dom-obj-event.html)


#### 事件监听与移除

```
.addEventListener("click",function(){});
.removeEventListener()
```

#### 鼠标事件

```
onclick	鼠标点击事件
onmouseover	鼠标移入事件
onmouseout	鼠标移出事件
onmousedown	鼠标按下事件
onmouseup	鼠标松开事件
onmousemove	鼠标移动事件
```

#### 键盘事件

```
onkeydown 键盘按下会触发的事件
onkeyup 键盘松开会触发的事件
```

#### 表单事件

```
onfocus	表单元素聚焦时触发
onblur	表单元素失焦时触发
```

### DOM元素对象属性和方法

#### 元素的新增，删除

```
.createTextNode();   创建文本的节点
.createElement("tr");   创建元素<tr>
.appendChild()  添加节点
.removeChild()  删除节点
```

```html
    <div id="box">
        <input type="text" id="txt">
        <button onclick="add()">添加</button>
        <p id="p1">这是一个段落。</p>
        <p id="p2">这是另外一个段落。</p>
    </div>
    <script>
        function add() {
            var txtName = document.getElementById("txt").value;
            let txt = document.createTextNode(txtName);
            var para = document.createElement("p");
            para.appendChild(txt);
            var box = document.getElementById("box");
            box.appendChild(para);
        }
        var parent = document.getElementById("box");
        var child = document.getElementById("p1");
        parent.removeChild(child); //删除父元素中的子元素
    </script>
```

#### 操作元素内容

```
.innerHTML
.innerText
```

> 以上两个以及document.write()的差别
>
> document.write是直接将内容写入页面的内容流，会导致页面全部重绘，innerHTML将内容写入某个DOM节点，不会导致页面全部重绘
>
> ![image-20221017212023387](img/JS基础.assets/image-20221017212023387.png)

#### 操作元素内容属性

```
.src
.href
.getAttribute()
```

#### 操作表单属性

```
.value	更换表单内容
.disabled	表单是否可用，默认false
```

#### 操作样式属性

```
.className
.style.样式
```

## 内置对象

### 数组对象Array

```
var 数组名 = new Array(元素1, 元素2,...,元素n);
var 数组名 = [元素1, 元素2,...,元素n];
```

`.length` 获取数组长度

常用方法：

- `slice(x,y)`  数组切片 下标
- `unshift()`  数组头部增加新元素
- `shift()`  删除数组首元素
- `sort()`  对元素进行从小到大排序
- `reverse()`  逆序排列
- `pop()`   删除并返回数组的最后一个元素
- `push()`   像数组末尾添加一个元素，并返回新的长度
- `indexOf()`  查找元素的下标值

- `concat()`  拼接多个数组
- `join()`   把数组的所有元素放入一个字符串并返回该字符串。可以指定间隔符
- `includes(元素)`  判断该数组中是否包含某个元素
- `数组名.toString()`  数组转换为字符串并返回结构

````
var a = new Array();
var b = new Array();
a = [2,9,6]
b = [3,8]
console.log(a)
console.log(a.concat(b))
console.log(a.join("-"))
console.log(a.pop())
console.log(a.push(3))
console.log(a.reverse())
console.log(a.sort())
console.log(a.toString())
````

![image-20221006150609241](img/JS基础.assets/image-20221006150609241.png)

### 字符串对象String

`字符串.charAt(下标值)`   返回在指定下标的字符

`toLowerCase()`  把字符串转换为小写

`toUpperCasc()`   把字符串转换为大写

`substring(x,y)`  提取字符串中两个指定的下标之间的字符

`replace(x,y)`   替换字串

`split()`   使用指定的分隔符将一个字符串分割成子字符串数组

`concat()`   连接字符串

`indexOf()`  某个字符在字符串中首次出现的位置

`anchor()`   创建锚点

`lastIndexOf(字符串)`   在字符串中寻找指定的子串，并返回子串的终止位置

`substr(起始索引,长度)`   获取字符串的“起始索引”位置至长度的字符

### 日期对象Date

`getDate()`    返回在一一个月中的哪天(1~31)

`getDay()`    返回在一一个星期中的哪天**(0~6**),其中星期天为0

`getHours()`    返回在一天中的哪个小时(0~23 )

`getMinutes()`    返回在-小时中的哪- 分钟(0~59 )

`getMonth()`   返回在一年中的哪-月(0~11)

`getSeconds()`	返回在一分钟中的哪-秒(0~59)

`getFullYear()`	以4位数字返回年份，如2010

`setDate()`	设置月中的某一天(1~31)

`setHours()`	设置小时数(0~23)

`setMinutes()`	设置分钟数(0~59)

`setSeconds()`	设置秒数(0~59)

`setFullYear()`	以4位数字设置年份

**扩展：**

`setInterval("showDate()", 1000);`

`setTimeout("showDate()", 10000);`   //间隔多久执行一次

**动态显示当前时间**

```html
    <body onload="showTime()">
        <script>
            function showTime() {
                var date = new Date();
                var year = date.getFullYear();
                var month = date.getMonth() + 1; //因为month属性从0开始所以加1
                var day = date.getDate(); // 日
                var week = date.getDay(); // 星期几，是个数字
                switch (week) {
                    case 1:
                        week = "星期一";
                        break;
                    case 2:
                        week = "星期二";
                        break;
                    case 3:
                        week = "星期三";
                        break;
                    case 4:
                        week = "星期四";
                        break;
                    case 5:
                        week = "星期五";
                        break;
                    case 6:
                        week = "星期六";
                        break;
                    case 0:
                        week = "星期日";
                        break;
                }
                var hour = date.getHours();
                var minute = date.getMinutes();
                var second = date.getSeconds();
                var t = "AM";
                if (hour > 13) {
                    hour = date.getHours() - 12;
                    t = "PM"
                } else {
                    hour = date.getHours();
                }
                second = second < 10 ? "0" + second : second;
                var current = year + "年" + month + "月" + day + "日 " + hour + ":" + minute + ":" + second + " " + t +
                    " " + week;
                document.getElementById("time").innerHTML = current;
            }
            setInterval("showTime()", 1000); //每隔1000毫秒（即1秒）显示一次当前时间
        </script>
        <h3>你好，现在是北京时间：</h3>
        <h3><span id="time"></span></h3>
    </body>
```

### 数学对象Math

> 用于执行常用的数学任务，它包含了若干个数字常量和函数 

**常用属性：**

`Math.PI`	圆周率

**常用方法：**

`ceil() `		返回大于等于数字参数的最小整数，对数字进行上舍人

`floor()  `		返回小于等于数字参数的最小整数，对数字进行下舍入

`random()`	返回一个[0,1]的随机小数

`abs()`			返回一个数的绝对值。

`sqrt()`		返回一个数的平方根。

`round()`		返回四舍五入后的整数。

`pow(x, y)`		返回一个数的 y 次幂。

## event对象

type	查看事件类型

```html
    <script>
      window.onload = function () {
        var value = document.getElementById("btn");
        value.onclick = function (e) {
          console.log("这是一个" + e.type + "事件"); // 控制台打印事件类型
        };
      };
    </script>
```

## 原生AJAX

> AJAX 的英文全称为 Asynchronous JavaScript And XML，Asynchronous 是异步的意思。何为异步呢？在这里异步是指通过 AJAX 向服务器请求数据，在不刷新整个页面的情况下，更新页面上的部分内容。

![image-20230302160748277](img/JS基础.assets/image-20230302160748277.png)

用户在浏览器执行一些操作，通过 AJAX 引擎发送 HTTP 请求到服务器请求数据，请求成功后，由服务器把请求的数据拿给 AJAX 引擎，再由 AJAX 拿给浏览器。AJAX 在这个过程中相当于是服务员，用户点好菜，由服务员把菜单交给厨师，厨师做好菜，由服务员把菜送到用户的餐桌上。

同学们可能会想，我直接把菜单交给厨师，省去中间人沟通岂不是更简单？

浏览器如果直接向服务器请求数据的话，在请求过程中，你是不能对页面进行其他操作的，这叫同步请求，而把请求数据这个活外包给 AJAX 后，在请求过程中，用户还是可以对页面进行其他操作，这就是我们的异步请求了，也是 AJAX 的核心特点。

**1. 创建 XMLHttpRequest 对象**

在 AJAX 中，`XMLHttpRequest` 对象是用来与服务器进行数据交换的。其创建如下所示：

```js
var httpRequest = new XMLHttpRequest();
```

为了保证浏览器的兼容性，我们可以用以下方式来创建。

```js
if (window.XMLHttpRequest) {
  // Mozilla，Safari，IE7+ 等浏览器适用
  httpRequest = new XMLHttpRequest();
} else if (window.ActiveXObject) {
  // IE 6 或者更老的浏览器适用
  httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
}
```

**2.向服务器发送请求**

在步骤一中我们已经创建了用于服务器交换数据的 `XMLHttpRequest` 对象，要向服务器发送请求，我们需要调用该对象中的 `open` 和 `send` 方法。

其使用如下：

```js
// 规定发送请求的一些要求
httpRequest.open("method", "url", async);
// 将请求发送到服务器
httpRequest.send();
```

`open` 方法中的参数说明如下：

- `method` 是请求的类型，常见的有 `GET` 和 `POST`。
- `url` 是请求的地址。
- `async` 是设置同步或者异步请求，其值为布尔类型，当为 true 时，使用异步请求；当为 false 时，使用同步请求，默认为 true。

**3.服务器响应状态**

我们使用 HTTP 请求数据后，请求是否成功，会反馈给我们相应的请求状态。我们使用 `onreadystatechange` 去检查响应的状态，当 `httpRequest.readyState` 为 4 并且 `httpRequest.status` 等于 200 时，说明数据请求成功，其使用如下：

```js
httpRequest.onreadystatechange = function () {
  if (httpRequest.readyState == 4 && httpRequest.status == 200) {
    // 请求成功执行的代码
  } else {
    // 请求失败执行的代码
  }
};
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>AJAX 的使用</title>
    <script>
      window.onload = function () {
        if (window.XMLHttpRequest) {
          // Mozilla，Safari，IE7+ 等浏览器适用
          var httpRequest = new XMLHttpRequest();
        } else if (window.ActiveXObject) {
          // IE 6 或者更老的浏览器适用
          var httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
        }
        // 规定发送请求的一些要求
        httpRequest.open(
          "GET",
          "https://jsonplaceholder.typicode.com/users",
          true
        );
        // 将请求发送到服务器
        httpRequest.send();
        httpRequest.onreadystatechange = function () {
          console.log(httpRequest.readyState);
          console.log(httpRequest.status);
          if (httpRequest.readyState == 4 && httpRequest.status == 200) {
            // 请求成功执行的代码
            document.getElementById("item").innerHTML = "请求成功";
          } else {
            // 请求失败执行的代码
            document.getElementById("item").innerHTML = "请求失败";
          }
        };
      };
    </script>
  </head>
  <body>
    <div id="item"></div>
  </body>
</html>
```

![image-20230302164131924](img/JS基础.assets/image-20230302164131924.png)

 2、3、4 是 `readyState` 的值，它的取值有以下几种：

- 0 代表未初始化请求。
- 1 代表已与服务器建立连接。
- 2 代表请求被接受。
- 3 代表请求中。
- 4 代表请求完成。