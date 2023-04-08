https://www.lanqiao.cn/courses/10532/learning/?id=565247&compatibility=false

- 全局上下文中的 `this`

  - 不管有没有启用严格模式，都指向 `window` 对象

  - ```
    console.log(this === window); // 输出 true
    ```

- 函数上下文中的 `this`

  - 优先级是 `new` 调用 > `call`、`apply`、`bind` 调用 > 对象上的函数调用 > 普通函数调用

![img](img/this指向.assets/b22ee17fe82bc646faf62b838fad0983-0)