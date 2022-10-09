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

## DOM文档对象模型

>  文档对象模型
>
>  https://blog.csdn.net/weixin_48376132/article/details/118500474
>
>  https://blog.csdn.net/egg_er/article/details/121572126

### DOM获取元素对象  

`document.getElementById()`

`document.getElementsByTagName()`

`document.getElementsByClassName()`

`document.getElementsByName()`

`document.write()`

### DOM事件

[HTML DOM 事件对象 | 菜鸟教程 (runoob.com)](https://www.runoob.com/jsref/dom-obj-event.html)

### DOM元素对象属性和方法

#### 事件监听与移除

> 使用的不多啊，移除监听

```
.addEventListener("click",function(){});
.removeEventListener()
```

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

## JavaScript核心对象

### 数组对象Array

常用函数：

- `concat()`  拼接多个数组
- `pop()`   删除并返回数组的最后一个元素

- `push()`   像数组末尾添加一个元素，并返回新的长度
- `reverse()`  颠倒元素顺序

- `sort()`  对元素进行排序

- `join()`   把数组的所有元素放入一个字符串并返回该字符串。可以指定间隔符
- `toString()`  数组转换为字符串并返回结构

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

`charAt()`   返回在指定位置的字符

`concat()`   连接字符串

`substring()`  提取字符串中两个指定的索引号之间的字符

`indexOf()`  检索指定的字符串位置

`Split()`   把字符串分割为字符串数组

`toLowerCase()`  把字符串转换为小写

`toUpperCasc()`   把字符串转换为大写

`replace()`   替换字串

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

`ceil() `  	返回大于等于数字参数的最小整数，对数字进行上舍人

`floor()  ` 	返回小于等于数字参数的最小整数，对数字进行下舍入

`random()`	返回一个[0,1]的随机小数