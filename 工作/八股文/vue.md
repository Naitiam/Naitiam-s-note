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

Action（动作） 异步操作

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

### *传值

父传子 props

子传父 $emit

兄弟传值 $bus

组件间传值，共用值 vuex pinia

### *computed有啥特点？和watch，methods的区别

计算属性：会缓存结果，不变不会重新计算

监听 对单个属性

方法
