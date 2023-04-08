## Generater 函数

- 可以通过**yield关键字**，将函数挂起，为了改变执行流提供了可能，**异步**
- function 后 函数名前 有个*
- 只能在函数内部使用yield表达式，让函数挂起

```javascript
    function* func(a){
        console.log('start');
        yield 2;
        yield 3;
        console.log('end');
    }
    let fn = func();
    console.log(fn);
    console.log(fn.next());
    console.log(fn.next());
    console.log(fn.next());
```

类似打断点，yield暂停执行，next继续执行

```javascript
    function* add() {
        console.log('start');
        let x = yield '2';
        console.log(x);
        let y = yield '3';
        console.log(y);
        console.log('end');
        return x + y;
    }
    const a = add();
    console.log(a.next());
    console.log(a.next(10));
    console.log(a.next(20));
```

## async函数

> async 是 Generator 的一个语法糖。
> 用 async 和 await 解决 回调地狱。

对Generater 函数的改进：

- `async`函数的返回值是 Promise 对象，`Generator` 函数的返回值是 Iterator 对象
- `yield`命令后面只能是 Thunk 函数或 Promise 对象，而`async`函数的`await`命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）

只有`async`函数内部的所有异步操作执行完，才会执行`then`方法指定的回调函数。

```
    let promise = new Promise((resolve, reject) => {
      resolve(10);
    });
    //等价于
    async function fn() {
      return await Promise.resolve(10);
    }
    promise.then((res) => {
      console.log(res);
    });
    fn().then((res) => {
      console.log(res);
    });
```

### await 关键字

`await`命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

`await` 只能在**async异步函数**或**es模块**中内使用

```html
  <script type="module">
    await console.log(1);
  </script>
```

```javascript
    async function f() {
        let s = await 'hello world';
        let data = await s.split(' ');
        return data;
    }
    console.log(f());
    f().then(v=>{
        console.log(v);
    }).catch(e=>{
        console.log(e)
    })
```

```
// 函数 p 返回的是一个 Promise 对象，在对象中，延时 2 秒，执行成功回调函数，相当于模拟一次异步请求
function p(v) {
  return new Promise(function (resolve) {
    setTimeout(function () {
      // 在 p 函数执行时，将函数的实参值 v ，作为执行成功回调函数的返回值。
      resolve(v);
    }, 2000);
  });
}

// 一个用于正常输出内容的函数
function log() {
  console.log("2.正在操作");
}

async function fn() {
  console.log("1.开始");
  await log();
  let p1 = await p("3.异步请求");
  console.log(p1);
  console.log("4.结束");
}
fn();
```

### 多层嵌套传参数的优化

```
// 函数 p 返回的是一个 Promise 对象，在对象中，延时 2 秒，执行成功回调函数，相当于模拟一次异步请求
function p(v) {
  return new Promise(function (resolve) {
    setTimeout(function () {
      // 在 p 函数执行时，将函数的实参值 v ，作为执行成功回调函数的返回值。
      resolve(v);
    }, 2000);
  });
}
async function fn() {
  let p1 = await p("1");
  let p2 = await p(p1 + "2");
  let p3 = await p(p2 + "3");
  console.log(p3);
  console.log("登录成功！");
}
fn();
```

### 多个并列异步请求的调优

> `await` 在处理多个异步请求时，如果请求之间有嵌套关系，可以一次一次按顺序发送请求，但是如果各个请求之间无任何关联，则可以将这些请求借助 `Promise.all` 一次性并列发送，使用 `await` 关键字获取请求的结果，并根据返回的结果进行下一步操作。如下列需求。

```
// 函数 p 返回的是一个 Promise 对象，在对象中，延时 2 秒，执行成功回调函数，相当于模拟一次异步请求
function p(v) {
  return new Promise(function (resolve) {
    setTimeout(function () {
      // 在 p 函数执行时，将函数的实参值 v ，作为执行成功回调函数的返回值。
      resolve(v);
    }, 2000);
  });
}
async function fn() {
  await Promise.all([p("a"), p("b"), p("c")]);
  console.log("隐藏加载动画！");
}
fn();
```

**涉及错误处理：**

以下第二个await语句是不会执行的，因为第一个语句将Promise对象状态变为结束。

```javascript
    async function fn() {
        await Promise.reject('出错了');
        return await Promise.resolve('hello');
    }
```

即使有异步任务出错，也不影响下面异步任务的执行。

```javascript
	//方法一：在异步函数内部使用try-catch语句
	async function fn() {      
        try {
            await Promise.reject('出错了');
        } catch (error) {
        }
        return await Promise.resolve('hello');
    }
    //方法二：await后面的 Promise对象再跟一个catch方法
    async function fn() {      
        await Promise.reject('出错了').catch((error) => { 
            console.log(error);
         })
        return await Promise.resolve('hello');
    }
    console.log(fn());
    fn().then(v => {
        console.log(v);
    }).catch(e => {
        console.log(e);
    })
```

