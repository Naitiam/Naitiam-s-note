### CSS盒子模型

content + padding +border + margin

正常盒模型：

box-sizing: content-box 的宽度 内容宽度+左右padding+左右border

怪异盒模型：

box-sizing: border-box  的宽度 包括内容宽度+左右padding+左右border，向内扩展

###  display:none 与 visibility:hidden

display:none  不占据空间

visibility:hidden  占据空间，类似透明度为零

### JS事件循环机制

> https://blog.csdn.net/Android_boom/article/details/127678182

JavaScript是一门单线程语言

分为同步任务和异步任务

同步任务是指在主线程上排队执行的任务，只有前一个任务执行完毕，才能继续执行下一个任务。

异步任务指的是，不进入主线程、而进入"任务队列"的任务；只有等主线程任务全部执行完毕，"任务队列"的任务才会进入主线程执行。

异步任务分为宏任务和微任务

|                    |                     宏任务（macrotask）                      |                   **微任务（microtask）**                    |
| :----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|      谁发起的      |                     宿主（Node、浏览器）                     |                            JS引擎                            |
|      具体事件      | 1.script (可以理解为外层同步代码) 2. **setTimeout/setInterval** 3. UI rendering/UI事件 4. postMessage，MessageChannel 5. setImmediate，I/O（Node.js） | 1. **Promise** 2. MutaionObserver 3. Object.observe（已废弃；Proxy 对象替代） 4. process.nextTick（Node.js） |
|      谁先运行      |                            后运行                            |                            先运行                            |
| 会触发新一轮Tick吗 |                              会                              |                             不会                             |

**执行过程: 同步任务 —> 微任务 —> 宏任务**

1. 先执行所有同步任务，碰到异步任务放到任务队列中
2. 同步任务执行完毕，开始执行当前所有的异步任务
3. 先执行任务队列里面所有的微任务
4. 然后执行一个宏任务
5. 然后再执行所有的微任务
6. 再执行一个宏任务，再执行所有的微任务·······依次类推到执行结束。

3-6的这个循环称为事件循环Event Loop

事件循环是JavaScript实现异步的一种方法，也是JavaScript的执行机制
