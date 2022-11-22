
```javascript
    //表示独一无二的值
    //用来定义对象的私有变量
    const name = Symbol('name');
    const name2 = Symbol('name');
    console.log(name == name2);

    let s1 = Symbol('s1');
    console.log(s1);
    let obj = {
        [s1]: '张三',
        b : 2
    };
    // obj[s1] = '张三';
    //如果使用Symbol定义对象中的变量，取值时一定要用[变量名]
    console.log(obj[s1]);

    //遍历数组
    for(let key in obj){
        console.log(key);
    }
    //会发现获取不到Symbol定义的变量
    console.log(Object.keys(obj));

    //获取Symbol定义的变量名称
    let s = Object.getOwnPropertySymbols(obj);
    console.log(s[0]);

    //遍历数组，包括Symbol定义的变量
    let m = Reflect.ownKeys(obj);
    console.log(m);
```

