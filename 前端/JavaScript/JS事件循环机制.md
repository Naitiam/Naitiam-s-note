---
title: JS事件循环机制
date: 2023-08-02
tags:
  - JS
---
## 事件循环机制

JavaScript是一门单线程语言

分为同步任务和异步任务

同步任务是指在主线程上排队执行的任务，只有前一个任务执行完毕，才能继续执行下一个任务。

异步任务指的是，不进入主线程、而进入"任务队列"的任务；只有等主线程任务全部执行完毕，"任务队列"的任务才会进入主线程执行。

### 异步任务

异步任务分为宏任务和微任务。

|                    |                     宏任务（macrotask）                      |                   **微任务（microtask）**                    |
| :----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|      谁发起的      |                     宿主（Node、浏览器）                     |                            JS引擎                            |
|      具体事件      | 1.执行script标签内部代码2. **setTimeout/setInterval** 3. UI rendering/UI事件 4. postMessage，MessageChannel 5. setImmediate，I/O（Node.js）6.**ajax请求** | 1. **Promise.then(); Promise.cath()；** 2. MutaionObserver 3. Object.observe（已废弃；Proxy 对象替代） 4. process.nextTick（Node.js）5.**async/await** |
|      谁先运行      |                            后运行                            |                            先运行                            |
| 会触发新一轮Tick吗 |                              会                              |                             不会                             |

⚠️注意：

- **`new Promise()` 属于同步任务，但是 `Promise.then(); Promise.cath()` 属于异步任务的微任务。**
- **`async` 函数里遇到 `await` 之前的代码是同步里的，遇到 `await` 时，会执行 `await` 后面的函数，然后返回一个 `promise` ，把 `await` 下面的代码放入微任务，并且退出这个 `async` 函数。**
- **`Promise.resolve()`  返回一个 `promise` 对象，状态为 `resolved` 。 `resolved` 后的 `promise` 对象会在这该级别事件队列结束之后才开始执行，及执行与该轮微任务队列中，始于下一级别宏任务之前。**

### 执行过程

**同步任务 —> 微任务 —> 宏任务**

1. 先执行所有同步任务，碰到异步任务放到任务队列中
2. 同步任务执行完毕，开始执行当前所有的异步任务
3. 先执行任务队列里面所有的微任务
4. 然后执行一个宏任务
5. 然后再执行所有的微任务
6. 再执行一个宏任务，再执行所有的微任务·······依次类推到执行结束。

3-6的这个循环称为事件循环Event Loop

事件循环是JavaScript实现异步的一种方法，也是JavaScript的执行机制。

## 题目

### 题目一

```
  async function async1() {
    console.log("async1 start");
    await async2();
    console.log("async1 end");
  }
  async function async2() {
    console.log("async2");
  }
  console.log("script start");
  setTimeout(function () {
    console.log("settimeout");
  });
  async1();
  new Promise(function (resolve) {
    console.log("promise1");
    resolve();
  }).then(function () {
    console.log("promise2");
  });
  console.log("script end");
```

结果

```
script start
async1 start
async2
promise1
script end
async1 end
promise2
settimeout
```

详解：考察点 await上面的代码和后面的代码是直接执行的，await下面的代码是要进微任务队列的;new Promise()同步任务;resolve是同步执行的，then里的代码是要进微任务队列的。

执行过程：script start->async1()->async1 start->async2->promise1->script end->微任务处理->async1 end->promise2->宏任务处理->settimeout

### 题目二

```
  async function p1() {
    return 1;
  }
  async function p2() {
    return Promise.resolve(2);
  }
  async function p3() {
    return await Promise.resolve(3);
  }
  p3().then((o) => {
    console.log(o, "p3");
  });
  p2().then((o) => {
    console.log(o, "p2");
  });
  p1().then((o) => {
    console.log(o, "p1");
  });
  console.log(4, "p4");
```

结果

```
4 'p4'
1 'p1'
3 'p3'
2 'p2'
```

详解：Promise.resolve() 返回的 promise对象，在同级为任务之后执行

执行过程：同步任务p4 ->微任务

微任务队列： then((){p3}) --> then((){p3}) - then((){p2}) --> then((){p1})-then((){p3}) - then((){p2})

### 题目三

```
  console.log(1);
  setTimeout(() => {
    console.log(2);
  }, 0);
  new Promise((res) => {
    console.log(3);
    setTimeout(() => {
      console.log(4);
    }, 0);
    res();
    console.log(5);
  }).then(() => {
    console.log(6);
  });
  console.log(7);
```

结果

```
1
3
5
7
6
2
4
```

### 题目四

```
console.log('1');
setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})
 
setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
}) 
```

结果

```
1 7 6 8 2 4 3 5 9 11 10 12
```

详解：宏任务里有微任务

### 题目五

```
  const promise = new Promise((resolve, reject) => {
    resolve("10");
  })
    .then((res) => {
      console.log("res1:", res); //res1: 10
      return 9;
    })
    .then((res) => {
      console.log("res2:", res); //res2: 9
      return 8;
    })
    .then((res) => {
      console.log("res3:", res); //res3: 8
      let promise2 = new Promise((resolve, reject) => {
        resolve("p2");
      }).then((res) => {
        console.log(res);
        setTimeout(function () {
          console.log("setTimeout2");
        }, 0);
      });
    });
  console.log("aaa");
  setTimeout(function () {
    console.log("setTimeout1");
  }, 0);
  const promise1 = new Promise((resolve, reject) => {
    console.log("p1");
    resolve(989);
  })
    .then((res) => {
      console.log(res);
      return 990;
    })
    .then((res) => {
      console.log(res);
      return 991;
    })
    .then((res) => {
      console.log(res);
      return 0;
    });
```

结果

```
aaa
p1
res1: 10
989
res2: 9
990
res3: 8
991
p2
setTimeout1
setTimeout2
```

详解：同步代码aaa-》p1-》宏任务之前把两个微任务处理掉-》res1 10-》989-》处理过程中继续产生微任务，继续处理-》res2 9-》990-》res 8-》991-》处理宏任务之前的微任务p2-》产生了一个宏任务setTimeout放到任务队列里-》执行宏任务，第一个setTimeout-》setTimeout1-》第二个setTimeout-》setTimeout2