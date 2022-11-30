`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

`./modules/index.js`

```javascript
// export const name = '张三';
// function sayName(){
//     return '李四';
// }
// export {sayName}

const name = '张三';
function sayName(){
    return '李四';
}
export {name,sayName,Animal}
const obj = {
    foo: 'foo'
}
export default obj;
class Animal{
    constructor(name){
        this.name = name;
    }
    sayName(){
        return this.name;
    }
}
```

```javascript
<script type="module">
    // import {name,sayName,Animal} from './modules/index.js'
    import * as fn from './modules/index.js'
    let a = new fn.Animal('dog');
    console.log(a.sayName());
    console.log(fn);
    // console.log(name);
</script>
```

