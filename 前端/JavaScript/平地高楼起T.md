题目地址

https://www.lanqiao.cn/problems/2328/learning/?contest_id=65

考察

递归，数组处理

```
  return regions.filter(item => item.pid == rootId).map(item => {
    item.children = convertToTree(regions, item.id),
    return item
  })
```

