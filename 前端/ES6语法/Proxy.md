> 报错处理

`Proxy` 可以对目标对象的读取、函数调用等操作进行拦截，然后通过对象的代理对象进行操作

用 Proxy 创建代理需要传入两个参数：目标对象（target）和处理程序（handler）。语法格式如下：

```js
var proxy = new Proxy(target, handler);
```

### get(target, propKey, receiver)

```
let dog = {
  name: "闷墩儿",
};
var proxy = new Proxy(dog, {
  get(target, propKey) {
    // 遍历目标对象的属性键值
    if (propKey in target) {
      return target[propKey]; // 返回相应的属性值
    } else {
      throw new ReferenceError(propKey + " 属性不存在");
    }
  },
});
console.log("访问 dog 对象中的 name 属性值为：" + proxy.name);
console.log("访问不存在的 age 属性：" + proxy.age);
```

### set(target, propKey, value, receiver)

```
let validator = {
  set(target, propKey, value) {
    if (propKey === "age") {
      // 判断 age 属性值是否时数字
      if (!Number.isInteger(value)) {
        throw new TypeError("狗狗的年龄只能是整型哦！");
      }
    }
    target[propKey] = value;
    return true;
  },
};

let dog = new Proxy({}, validator);
console.log((dog.age = "22"));
```

### has(target, propKey)

```
let dog = {
  name: "闷墩儿",
  age: 2,
};
let handler = {
  has(target, propKey) {
    if (propKey == "age" && target[propKey] < 5) {
      console.log(`${target.name}的年龄小于 5 岁哦！`);
      return true;
    }
  },
};
let proxy = new Proxy(dog, handler);

console.log("age" in proxy);
```

