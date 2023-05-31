饼图数据：键值对

柱状：数组数据

`option` 相当于是存放组件的容器，而在 `option` 中的都被称为 **组件**

`xAxis`（直角坐标系 X 轴）

`yAxis`（直角坐标系 Y 轴）

`grid`（直角坐标系底板）

`angleAxis`（极坐标系角度轴）

`radiusAxis`（极坐标系半径轴）

`polar`（极坐标系底板）

`geo`（地理坐标系）

`dataZoom`（数据区缩放组件）

`visualMap`（视觉映射组件）

`tooltip`（提示框组件）

`toolbox`（工具栏组件）

`legend` 图例组件

![img](https://doc.shiyanlou.com/courses/5788/1347963/2747f4ae9e45c0e6e6d93d9ad0373293-0)

#### 数据

`series.data`

数据

```js
[{
  name: 'Direct', // 
  type: 'line',
  stack: 'Total',
  data: [320, 332, 301, 334, 390, 330, 320]
},{},...]
```

数据集（`dataset`）

![img](img/ECharts.assets/fa00da1541cad6ee9a84d07ca8fb5555-0)

#### 事件处理

```
myChart.on("事件名称", 回调函数);
```

