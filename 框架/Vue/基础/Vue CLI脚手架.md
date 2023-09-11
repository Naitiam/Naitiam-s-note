## 目录

*   [组件](#组件)

*   [render函数](#render函数)

*   [vue.config.js 配置文件](#vueconfigjs-配置文件)

# Vue CLI脚手架

创建项目vue create xxx

*   babel.config.js babel配置文件

*   package.json 应用包配置文件

*   package-lock.json 包版本配置文件

## 组件

复用率高

> 从p53开始就究极迷茫。因为知道后期脚手架中如何使用，以及这些都没使用，所以仅记录部分要点

```vue
<script type="text/javascript">
  //定义组件
  const hello = Vue.extend({
    name:'hello',
    template:'',
    //data必须写成函数的形式
    data(){
        return{

        }
    }
  })

  //全局注册组件
  Vue.component('hello',hello)

  new Vue({
    el: '#root',
    data: {
    },
    //局部注册组件
    components:{
        hello
    }
  })
</script>
```

**VueComponent 组件实例对象** 无需el ，data只能写为data(){}

**Vue 实例对象** 需el，data可为函数型也可为对象型

## render函数

main.js

为何使用render函数挂载模板？

**vue.js** 是完整版的Vue，包含：核心功能+模板解析器

\*\*vue.runtime.xxx.js \*\*是运行版的Vue，只包含核心功能，没有模板解析器。所以不能使用template配置项，需使用render函数接收到的createElement函数去指定具体内容。

```vue
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  el:'#app',
  // render函数功能：将App组件放入容器中
  // 简写形式
  render: h => h(App),
  // 完整形式
  // render(createElement){
  //   return createElement(App)
  // }
})
```

## vue.config.js 配置文件

查看脚手架默认配置：`vue inspect > output.js`

<https://cli.vuejs.org/zh/config/#vue-config-js>

注意：和 `package.json` 同级的目录下

```vue
module.exports = {
  pages: {
    index: {
      entry: 'src/index/main.js' // 入口
    }
  },
  lineOnSave: false  // 关闭语法检查
}
```
