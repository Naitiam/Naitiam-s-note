## 核心模块

### fs模块

- `fs.readFile()`读取文件
- `fs.appendFile()`创建新文件，或将数据添加到已有文件中
- `fs.mkdir()`创建目录
- `fs.rmdir()`删除目录
- `fs.rm()`删除文件
- `fs.rename()`重命名
- `fs.copyFile(`)复制文件

```javascript
const fs = require('fs')
const path = require('path')
const textPath = path.join(__dirname, '/test.md')
//readFileSync同步的读取文件方法，会堵塞后边代码执行，返回Buffer对象
//Buffer是一个临时用来存储数据的缓冲区
const buf = fs.readFileSync(textPath);
console.log(buf.toString());//文件内容

//readFile()异步读取文件
fs.readFile(textPath, (err, buffer) => {
  if (err) {
    console.log("出错了~");
  } else {
    console.log(buffer.toString());
  }
});
///一般项目重要结合Promise使用
```

使用Promise版本的fs方法

```javascript
const fs = require("node:fs/promises"); //使用Promise版本的fs方法
fs.readFile(path.resolve(__dirname, "./readme.md")).then((buffer) => {
  console.log(buffer.toString()).catch((err) => {
    console.log(err);
  });
});
```

### http模块

```
//导入http模块
const http = require("http");
//创建web服务器实例  http.createServer()
const server = http.createServer();
//为服务器绑定request事件，监听客户端请求
server.on("request", (req, res) => {
  //req  请求对象
  console.log(req.url); //客户端请求的url路径
  console.log(req.method); //客户端请求类型
  console.log("收到请求");
  //res  响应对象
  //res.setHeader() 设置响应头解决中文乱码问题
  res.setHeader("Content-Type", "text/html;charset=utf-8");
  //res.end() 向客户端发送数据，并结束本次请求
  let data = [
    {
      id: 1001,
      title: "让我们一起写一个前端监控系统吧！",
      replayCount: 14,
      clickCount: 3612,
    },
    {
      id: 1002,
      title: "花了一天的时间，地板式扫盲了vue3所有API盲点",
      replayCount: 21,
      clickCount: 9812,
    },
    {
      id: 1003,
      title: "我被骂了，但我学会了如何构造高性能的树状结构🔥",
      replayCount: 8,
      clickCount: 973,
    },
  ];
  //根据不同url响应不同结果
  if (req.url === "/404.html") {
    data = ["这里是关于界面"];
  }
  res.end(JSON.stringify(data));
});
server.listen(8080, function () {
  console.log("server running");
});
```



