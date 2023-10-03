### 为什么说js是单线程的？

js中的代码都是串行的，前面没有执行完毕后面不能执行。

### == 和 === 的区别？

== 对比操作数，类型不同则会转换后比较

=== 全等 ，操作数值和数据类型都相同，引用类型会比较内存的引用地址

### JS操作节点，添加，移除，移动，复制，创建，查找？

```
appendChild()
removeChild()
appendChild()
cloneNode()
createElement()
createTextNode()
getElementById() ...
```

### 数组常用方法

增删 slice( ) unshift()  push() shift()  pop() splice() concat() 

遍历处理查（不改变原数组）

sort()  includes() indexOf() lastIndexof() find() findIndex() map() reduce() filter()

转字符串 join()  toString() 

扁平化 flat(Infinity)

### 创建一个新对象发生了什么(new的过程)

> 其实考察原型链

`new` 关键字成功创建了一个**新的对象**，(**关联到原型对象，绑定this指向，执行构造函数，返回新对象**)并将其作为构造函数的实例返回。

用new一个新对象做实例

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const john = new Person('John', 25);
console.log(john);
```

`new Person('John', 25)` 首先创建了一个空对象，然后将该空对象的原型链关联到 `Person` 的 `prototype` 属性指向的对象上，接着将 `this` 指向新对象，执行构造函数代码，并对新对象进行属性赋值。最后，`new` 表达式返回了这个新对象 `john`，它具有 `name` 和 `age` 属性。

### 深浅拷贝的区别，vue中的实现深浅拷贝的方法分别有哪些

> 虽说是vue，但实际上还是js

vue中实现浅拷贝可以使用 `Object.assign()` 或扩展运算符，而实现深拷贝可以使用 `JSON.parse(JSON.stringify())` 或 lodash 库的 `cloneDeep()` 函数。

详情见  [JS高级](../前端/JavaScript/JS高级.md)

注意手撕深拷贝浅拷贝

### 性能优化，如果页面白屏怎么解？

异步加载资源

延迟加载非关键资源 广告

利用浏览器缓存机制

使用服务端渲染（SSR）

点击事件切换页面样式的过程中出现白屏

使用css预加载*未实践过

```
<link rel="preload" href="your-styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="your-styles.css"></noscript>
```

