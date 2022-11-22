## **js中三种定义变量的方式 let，const， var的区别**

> 主要是let与const

### let

- 没有变量提升：在声明前调用会报错
- 块级作用域：函数内部使用let定义后，对函数外部无影响
- 变量不能重复声明

```javascript
    //console.log(a); 报错，没有变量提升
    let c = 3;
    console.log('函数外let定义c：' + c);//输出c=3 
    function change(){
        let c = 6;
        console.log('函数内let定义c：' + c);//输出c=6
    }
    change();
    console.log('函数调用后let定义c不受函数内部定义影响：' + c);//输出c=3
```

### const

- 没有变量提升
- 块级作用域
- 变量不能重复声明
- 声明常量不可以修改，必须初始化
- 对于数组和对象的元素正常修改

```javascript
    const B = 44; {
        // const NAME; 报错，必须初始化
        const NAME = "aaaaa";
        // const NAME="bbbbb"; 报错
        console.log(NAME);
        console.log(B);
        const HUMEN = ["aaa", "bbb", "ccc"];
        HUMEN.push("ddd");
        console.log(HUMEN);
        const STU = {
            name: "sss",
            age: 24
        }
        STU.age = 18;
        console.log(STU);
    }
    console.log();
```

```javascript
    //作用一：for循环经典例子
    const arr = [];
    for(let i = 0;i < 10;i++){
        arr[i] = function(){
            return i;
        }
    }
    console.log(arr[5]());
    //作用二：不会污染全局变量
    let RegExp = 10;
    console.log(RegExp);
    console.log(window.RegExp);
```

### var

**var定义的变量可以修改，如果不初始化会输出undefined，不会报错。**

```javascript
    var a = 1;
    // var a;//不会报错
    console.log('函数外var定义a：' + a);//可以输出a=1
    function change(){
        a = 4;
        console.log('函数内var定义a：' + a);//可以输出a=4
    }
    change();
    console.log('函数调用后var定义a为函数内部修改值：' + a);//可以输出a=4
```


