# localStorage本地存储

sessionStorage使用同理:存储的内容会随着浏览器窗口关闭而消失

四个API

*   `localStorage.setItem('key', 'value') `

*   `localStorage.getItem('key')`

*   `localStorage.removeItem('key') `

*   `localStorage.clear() `

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>localStorage本地存储,sessionStorage会话存储同理</h2>
    <button onclick="saveData()">点击存储数据</button>
    <button onclick="readData()">点击读取数据</button>
    <button onclick="deleteData()">点击删除数据</button>
    <button onclick="clearData()">点击清空数据</button>
</body>
</html>
<script>
    function saveData(){
       localStorage.setItem('msg','这里是信息')
       localStorage.setItem('num',1111)
       const person = {name:'张三',age:14}
       //将对象转化为字符串存储
       localStorage.setItem('obj',JSON.stringify(person))
    }
    function readData(){
        console.log(localStorage.getItem('msg'))
        console.log(localStorage.getItem('num'))
        console.log(JSON.parse(localStorage.getItem('obj')))
    }
    function deleteData(){
        localStorage.removeItem('msg')
    }
    function clearData(){
        localStorage.clear()
    }
</script>
```
