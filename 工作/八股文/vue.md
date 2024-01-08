---
title: 
date: 2023-09-06
description: 
tags: 
   -  vue
   -  面试题
---

### *vuex中的action和mutation有何区别?

Mutation（变更）同步操作

Action（动作） 异步操作主要包括一下几个模块：

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。

----

> 扩展 

**什么时候使用vuex？**

- 组件的状态存在异步操作
- 做个组件需要共享状态

vuex是一个全状态数据管理

```
pnpm install vuex --save
```

*src\store\index.js*

导入 use 

```
import Vue from 'vue';
import Vuex from 'vuex';
Vue.use(Vuex)

export default new Vuex.Store({
  state: {},	// 状态
  mutations: {},	// 同步更新
  actions: {},	// 异步操作
  modules: {}	// 模块
})
```

*src\main.js*

挂在到new Vue上

```
import Vue from 'vue'
import App from './App.vue'
import store from './store';

Vue.config.productionTip = false

new Vue({
  store,
  render: h => h(App),
}).$mount('#app')
```

使用

```
html中 <h1>{{ $store.state.count }}</h1>
js中 this.$store.state.count
```

this.$store.dispatch('countAction') --> actions去commit触发 --> mutations --> state

```
组件中
methods:{
	addCount(){
		this.$store.dispatch('countAction') -
	}
}

src\store\index.js
  state: {
  	count: 0
  },
  mutations: {
		countMutations(state){
			state.cout++;
		}
  },
  actions: {
    countAction(obj){
  		obj.commit("countMutations")
  	}
  }
```

### *简要对比vue2和vue3？

2020年9月发布的正式版

Vue3支持大多数Vue2的特性

Vue中设计了一套强大的组合api代替了Vue2中的选项式api，复用性更强了

更好的支持TS

最主要：Vue3中使用了Proxy配合Reflect 代替了Vue2中的Object.defineProperty()方法实现数据的响应式（数据代理）

重写了虚拟DOM，速度更快

新的组件： Fragment（片段）/Teleport（瞬移）/Susoense（不确定）

新的脚手架工具Vite（Vite 对比传统脚手架工具，采用了基于 ES 模块的开发方式，构建速度大大提高

### *vue怎样实现组件传值

`props / $emit` 适用 父子组件通信

父传子 props

子传父 $emit

中央时间总线 bus 简单的跨组件通信 并不直接共享数据

组件间，异步，vuex pinia，全局的状态树

### *computed有啥特点？和watch，methods的区别

Computed是计算属性，会缓存结果，不变不会重新计算

watch是监听一个值得变化然后进行回调

使用场景 computed 当一个属性受到多个属性影响时使用computed比如购物车

watch 当多条数据影响多条数据的时候使用 watch 比如搜索框

### Composition Api 与 Options Api 有什么区别？

Options Api

包含一个描述组件选项（data、methods、props等）的对象 options；

API开发复杂组件，同一个功能逻辑的代码被拆分到不同选项 ；

使用mixin重用公用代码，也有问题：命名冲突，数据来源不清晰；

composition Api

vue3 新增的一组 api，它是基于函数的 api，可以更灵活的组织组件的逻辑。

解决options api在大型项目中，options api不好拆分和重用的问题。

### Vue3.0和2.0对比，哪些方面更加出色？

Vue.js 2.x 中响应式系统的核心是 Object.defineProperty

然后进行深度遍历所有属性

给每个属性添加`getter`和`setter`，实现响应式

Vue.js 3.x 中使用 Proxy 对象重写响应式系统 

通过Proxy（代理） 拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等

通过Reflect（反射）: 对源对象的属性进行操作。 

### **为什么vite比webpack更快**

webpack会先打包，然后启动开发服务器，请求服务器时直接给予打包结果。

vite是直接启动开发服务器，请求哪个模块再对该模块进行实时编译。

### v-if 和 v-show 的区别

v-show 只是简单的控制元素的 display 属性。

v-if  该元素节点被注释掉

### 说说你对 SPA 单页面的理解，它的优缺点分别是什么？

SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转

不利于搜索引擎优化，首屏加载慢

### computed 和 watch 的区别和运用的场景？

computed： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值；
watch： 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；
运用场景：
当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；

当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

### Vue 生命周期

开始创建、初始化数据、编译模版、挂载 Dom -> 渲染、更新 -> 渲染、卸载等一系列过程

| beforeCreate  | 组件实例被创建之初，组件的属性生效之前                       |
| ------------- | ------------------------------------------------------------ |
| created       | 组件实例已经完全创建，属性也绑定，但真实 dom 还没有生成，$el 还不可用 |
| beforeMount   | 在挂载开始之前被调用：相关的 render 函数首次被调用           |
| mounted       | el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子    |
| beforeUpdate  | 组件数据更新之前调用，发生在虚拟 DOM 打补丁之前              |
| update        | 组件数据更新之后                                             |
| activited     | keep-alive 专属，组件被激活时调用                            |
| deadctivated  | keep-alive 专属，组件被销毁时调用                            |
| beforeDestory | 组件销毁前调用                                               |
| destoryed     | 组件销毁后调用                                               |

### 在哪个生命周期内调用异步请求？

可以在钩子函数 created、beforeMount、mounted 中进行调用，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。但是本人推荐在 created 钩子函数中调用异步请求，因为在 created 钩子函数中调用异步请求有以下优点：

- 能更快获取到服务端数据，减少页面 loading 时间；
- ssr 不支持 beforeMount 、mounted 钩子函数，所以放在 created 中有助于一致性；

### 在什么阶段才能访问操作DOM？

在钩子函数 mounted 被调用前，Vue 已经将编译好的模板挂载到页面上，所以在 mounted 中可以访问操作 DOM。

### **路由守卫 / 导航守卫**

既然是守卫，首先是对咱们后台页面访问的一层保护，如果我没有进行登陆过，后台的操作页面是不允许用户访问的我们是用到vue路由中的一个钩子函数beforeEach，那么这个函数中有三个参数，分别是to from nextto是去哪里 from是从哪里来 next下一步说通俗点就是放行。

### **为什么在使用v-for的时候需要添加key属性**

因为vue在更新渲染dom的时候是根据新旧dom树进行对比的，使用key来给每个节点做一个唯一标识，Diff算法就可以正确的识别此节点，找到正确的位置区插入新的节点。Vue的优化点之一
