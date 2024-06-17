更好的解决办法  [用JS解析CSV数据和导出 - 掘金 (juejin.cn)](https://juejin.cn/post/6905595101931077640)

```
时间,上月,本月
1日,128.7,200.71
2日,217.760001,258.109998
3日,166.01,210.539999
4日,201.870001,242.369999
5日,152.62,251.749997
6日,127.27,207.04
```

```typescript
// 一个处理csv的js工具
// 假设csv文件的内容是这样的：
// name,age,gender
// Alice,20,Female
// Bob,25,Male
// Charlie,30,Male

// 引入fs模块
const fs = require('fs');

// 定义一个函数，用于将csv文件转换为json对象数组
function csvToJson(csvFile) {
  // 读取csv文件的内容，返回一个字符串
  let csvData = fs.readFileSync(csvFile, 'utf8');
  // 按换行符分割字符串，返回一个字符串数组
  let lines = csvData.split('\n');
  // 取出第一行，作为表头，按逗号分割字符串，返回一个字符串数组
  let headers = lines[0].split(',');
  // 定义一个空数组，用于存放json对象
  let json = [];
  // 遍历除了第一行之外的每一行
  for (let i = 1; i < lines.length; i++) {
    // 按逗号分割字符串，返回一个字符串数组
    let values = lines[i].split(',');
    // 定义一个空对象，用于存放键值对
    let obj = {};
    // 遍历每一列
    for (let j = 0; j < headers.length; j++) {
      // 将表头作为键，将对应的值作为值，添加到对象中
      obj[headers[j]] = values[j];
    }
    // 将对象添加到数组中
    json.push(obj);
  }
  // 返回json对象数组
  return json;
}

export default csvToJson
```

```
import csvToJson from "../../utils/toJson.ts"
const data = csvToJson('csv/近两月尖峰平谷走势.csv');
```

