# Vue管理CSS样式

!!!!!高级用法

```
:style="{'background-color': item.meta.title.includes(msg) && msg!==''?'yellow':''}"
:style="{
          'background-color': bgList[curColorIndex],
          'color': curColorIndex==(bgList.length-1)?'#fff':'#333',
          'font-size': curFontSize + 'px',
          'line-height': (curFontSize+10)+'px'
         }"
:class="['iconfont',curColorIndex == index?'icon-selected':'']"
:class="[item.meta.title.includes(msg) && msg!==''?'bg':'']"
.bg{
	background-color: yellow;
}
```

```vue
    <style>
        .basic{
            width: 100px;
            height: 100px;
            background-color: antiquewhite;
        }
        .pink{
            background-color: pink;
        }
        .green{
            background-color: green;
        }
        .grey{
            background-color: grey;
        }
        .add1{
            font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
            color: cadetblue;
        }
        .add2{
            font-size: 30px;
        }
    </style>

<body>
    <div id="root">
        <!-- 点击切换样式 -->
       <div class="basic" :class="mood" @click="changcolor">moji</div>
       <!-- 数组写法 追加样式 -->
       <div class="basic" :class="classArr">moji</div>
       <!-- 对象写法 判断是否启用该样式 -->
       <div class="basic" :class="classObj">moji</div>
        <!-- 数组写法 -->
       <div class="basic" :style="styleArr">moji</div>
       <!-- 对象写法-->
       <div class="basic" :style="styleObj">moji</div>
    </div>
</body>

<script>
    new Vue({
        el:'#root',
        data:{
           mood:'normal',
           classArr:['add1','add2'],
           classObj:{
                add1:false,
                add2:true
           },
           styleArr:[
                {
                    fontSize: '25px'
                },
                {
                    color:'#666'
                }
            ],
            styleObj:{
                fontSize:'35px',
                color:'white',
                backgroundColor:'#888'
            }
        },
        methods: {
            changcolor(){
                const arr = ['pink','green','grey']
                this.mood = arr[Math.floor(Math.random()*3)]
            }
        },
    })
</script>

```
