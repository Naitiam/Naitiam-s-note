https://www.lanqiao.cn/courses/10532/learning/?id=565235&compatibility=false

```js
// 目标
// ['boolean', 'number', 'string', 'bigint', 'null', 'undefined', 'symbol', 'array', 'object', 'function', 'date', 'regexp', 'error', 'map', 'set', 'weakmap', 'weakset'] ['boolean', 'number', 'string', 'bigint', 'null', 'undefined', 'symbol', 'array', 'object', 'function', 'date', 'regexp', 'error', 'map', 'set', 'weakmap', 'weakset']
const testArr = [
  true,
  100,
  "abc",
  100n,
  null,
  undefined,
  Symbol("a"),
  [],
  {},
  function fn() {},
  new Date(),
  /abc/,
  new Error(),
  new Map(),
  new Set(),
  new WeakMap(),
  new WeakSet(),
];
```

判断一个数据的类型，比较常用的有下面几种方式：

- `typeof`
  - 无法判断 `null`。
  - 无法判断除了 `function` 之外的引用类型。
- `instanceof`
  - `instanceof` 可以判断引用类型

```
function getType(data) {
  // TODO：待补充代码
  if (typeof data == "boolean") {
    return "boolean";
  }
  if (typeof data == "number") {
    return "number";
  }
  if (typeof data == "string") {
    return "string";
  }
  if (typeof data == "bigint") {
    return "bigint";
  }
  if (data === null) {
    return "null";
  }
  if (typeof data == "undefined") {
    return "undefined";
  }
  if (typeof data == "symbol") {
    return "symbol";
  }
  if (typeof data == "function") {
    return "function";
  }
  if (Array.isArray(data)) {
    return "array";
  }
  if (data instanceof Date) {
    return "date";
  }
  if (data instanceof Map) {
    return "map";
  }
  if (data instanceof WeakMap) {
    return "weakmap";
  }
  if (data instanceof Set) {
    return "set";
  }
  if (data instanceof WeakSet) {
    return "weakset";
  }
  if (data instanceof RegExp) {
    return "regexp";
  }
  if (data instanceof Error) {
    return "error";
  }
  if (typeof data == "object") {
    return "object";
  }
}
```

- `Object.prototype.toString.call(xxx)`

调用 `Object.prototype.toString` 方法，会统一返回格式为 `[object Xxx]` 的字符串，用来表示该对象（原始类型是[包装对象](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive#javascript_中的基本类型包装对象)）的类型。

```
function getType(data) {
  var type = typeof data;
  if (type !== "object") {
    return type;
  }
  //如果不是object类型的数据，直接用typeof就能判断出来
  //如果是object类型数据，准确判断类型必须使用Object.prototype.toString.call(obj)的方式才能判断
  return Object.prototype.toString
    .call(data)
    .replace(/^\[object (\S+)\]$/, "$1")
    .toLowerCase();
}
```

正则表达式在替换中的使用  `$1`是第一个小括号（分组）中的匹配结果

```
const result = testArr.map((item) => getType(item));
console.log("得到的结果：", result);
```

