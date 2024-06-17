```
function getweather() {
  //TODO：请补充代码
  //方法一，使用 $.get('',(data) => {})
  //通过 innerHTML 来 替换 week-weather 的内容。
  $.get("js/weather.json", (data) => {
    let res = "";
    for (const i in data.result) {
      let weather = data.result[i];
      let html = `
            <div class="item" id="weather">
                <img src="${weather.weather_icon}">
                <div class="item-mess">
                    <div>${weather.weather}</div>
                    <div>${weather.temperature}</div>
                    <div>${weather.winp}</div>
                    <div>
                        <span>${weather.days}</span>
                        <span>${weather.week}</span>
                    </div>
                </div>
            </div>
            `;
      res += html;
    }
    document.getElementsByClassName("week-weather")[0].innerHTML = res;

    $.ajax({
      url: "js/weather.json",
      success: (weatherData) => {
        let data = weatherData.result;
        $.each(data, (i, item) => {
          //jQuery形式
          //   $(".item").eq(i).children().eq(0).attr("src", item.weather_icon);
          //   $(".item").eq(i).children().eq(1).children().eq(0).text(item.weather);
          //   $(".item")
          //     .eq(i)
          //     .children()
          //     .eq(1)
          //     .children()
          //     .eq(1)
          //     .text(item.temperature);
          //   $(".item").eq(i).children().eq(1).children().eq(2).text(item.winp);
          //   $(".item")
          //     .eq(i)
          //     .children()
          //     .eq(1)
          //     .children()
          //     .eq(3)
          //     .children()
          //     .eq(0)
          //     .text(item.days);
          //   $(".item")
          //     .eq(i)
          //     .children()
          //     .eq(1)
          //     .children()
          //     .eq(3)
          //     .children()
          //     .eq(1)
          //     .text(item.week);
          //js形式
          // divs[i].children[0].src = item.weather_icon;
          // divs[i].children[1].children[0].innerHTML = item.weather;
          // divs[i].children[1].children[1].innerHTML = item.temperature;
          // divs[i].children[1].children[2].innerHTML = item.winp;
          // divs[i].children[1].children[3].children[0].innerHTML = item.days;
          // divs[i].children[1].children[3].children[1].innerHTML = item.week;
        });
      },
    });
  });
}

getweather();
```

```
<!DOCTYPE html>
<html>

<head>
    <title>天气查询</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" type="text/css" href="style.css">
    <script src="js/jquery-3.6.0.min.js"></script>
</head>

<body>

    <nav class="navbar">
        <hearder class="title">天气查询</hearder>
        <div class="dialog">
            <div class="input-dialog">
                <input type="text" name="input-weather" id="input-weather" placeholder="杭州">
            </div>
        </div>
    </nav>

    <article class="mainbody">
        <section class="week-weather">
            <div class="item" id="Monday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Tuesday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Wednesday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Thursday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Friday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Saturday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
            <div class="item" id="Sunday">
                <img src="">
                <div class="item-mess">
                    <div></div>
                    <div></div>
                    <div></div>
                    <div>
                        <span></span>
                        <span></span>
                    </div>
                </div>
            </div>
        </section>
    </article>
    <script type="text/javascript" src="js/index.js"></script>
</body>

</html>
```

