题目地址

https://www.lanqiao.cn/problems/2282/learning/?contest_id=63&stop=false

主要考察字符串替换

```
<script>
  const toDesensitization = (str, rule, symbol = "*", dealPhone = true) => {
    if (!str) return null;
    if (str && !rule) return str;

    let obj = {
      ids: [],
      newStr: str,
    };
    const getNewStr = (ru) => {
      let reg = new RegExp(ru, "gim");
      obj.newStr = obj.newStr.replace(reg, function (word, index) {
        obj.ids.push(index);
        // new Array(word.length)生成word.length长度的数组，再fill(symbol)代表将数组内的元素全部设置为symbol的值，再调用join转换为字符串
        // return new Array(word.length).fill(symbol).join('')
        return symbol.repeat(word.length);
      });
    };
    if (Array.isArray(rule)) {
      // 如果rule是数组，则遍历
      for (const ru of rule) {
        getNewStr(ru);
      }
    } else {
      getNewStr(rule);
    }

    if (dealPhone) {
      obj.newStr = obj.newStr.replace(
        /(\d{3})\d{5}(\d{3})/g,
        `$1${symbol.repeat(5)}$2`
      );
    }
    console.log(obj);
    return obj;
  };
  toDesensitization(
    "不论这个世界多么糟糕，你的世界一定要精彩;不论人心多么黑暗，你的内心一定要明亮。不要用糟糕去对付糟糕，不要用黑暗去对付黑暗。心里充满阳光，世界就光明无比;心里充满感恩，世界因此灿烂。请记住：你的付出决定你的未来，你的汗水记得你的成就，你的态度决定你的一切.",
    ["糟糕", "记得", "定"],
    "*",
    true
  );
  // toDesensitization(
  //   "来好吗!怎样一向不打电话给我啊。知道吗?我还是我,但号码已经换成了 15273773888,多联络啊。",
  //   "号码",
  //   "*",
  //   true
  // );
  // toDesensitization("uofjjflsjhahf废旧塑料ffjsljfs", "jj", "*", true);
  // toDesensitization(
  //   "放假了电视剧理发店，杰弗里斯寄过来的15356895642结果劳动竞赛",
  //   ["了","发","结果"],
  //   "*"
  // );
</script>

```

