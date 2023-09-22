---
title: 
date: 2023-09-06
description: 
tags: 
   - 
---

## 传值

父传子 props

子传父 $emit

兄弟传值 $bus

组件间传值，共用值 vuex

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
  state: {},
  mutations: {},
  actions: {},
  modules: {}
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
<h1>{{ $store.state.count }}</h1>
this.$store.state.count
```

## 对比vue2和vue3

**vue3** 

2020年9月发布的正式版

Vue3支持大多数Vue2的特性

Vue中设计了一套强大的组合api代替了Vue2中的选项式api，复用性更强了

更好的支持TS

最主要：Vue3中使用了Proxy配合Reflect 代替了Vue2中的Object.defineProperty()方法实现数据的响应式（数据代理）

重写了虚拟DOM，速度更快

新的组件： Fragment（片段）/Teleport（瞬移）/Susoense（不确定）

新的脚手架工具Vite（Vite 对比传统脚手架工具，采用了基于 ES 模块的开发方式，构建速度大大提高

### 生命周期

vue3的组合式API（Composition API）  vue2的选项式API（Options API）

组合式API必须在setup配置项中使用，这个配置项替代了vue2中的created和beforecreate两个生命周期函数。

| vue2          | vue3            |
| ------------- | --------------- |
| beforeCreate  |                 |
| created       |                 |
| beforeMount   | onBeforeMount   |
| mounted       | onMounted       |
| beforeUpdate  | onBeforeUpdate  |
| updated       | onUpdated       |
| beforeDestroy | onBeforeUnmount |
| destroyed     | onUnmounted     |

> 要展开来去理解还有其基础格式，定义变量等等，定义响应式数据使用ref函数？什么是响应式数据

vue2

```
<script>
export default {
  mounted() {   // 直接调用生命周期钩子
    // ... 
  },
}
</script>
```

vue3

setup函数

```
<script>
export default {
  setup(props, context) {
    // ...         
    // 对于context参数，它是一个对象，对象里面存在attrs、slots、emit三个属性。
		// 如果需要使用它们直接使用props、context.attrs、context.slots、context.emit就可以获取或者是触发了。
  },           
}
</script> 
```

使用`setup`属性的`script`标签。里面的代码会被编译成组件 setup() 函数的内容。与普通的 `<script>` 只在组件被首次引入的时候执行一次不同，`<script setup>` 中的代码会在**每次组件实例被创建的时候执行**。

`setup` 函数里的参数，但是可以通过 `defineProps、defineEmits、useAttrs、useSlots `这几个函数来替代

```
<script setup>
import { onMounted } from 'vue';   // 使用前需引入生命周期钩子
 
onMounted(() => {
  // ...
});
 
// 可将不同的逻辑拆开成多个onMounted，依然按顺序执行，不会被覆盖
onMounted(() => {
  // ...
});
</script>
```

### 模板

`vue2` 中需要用  `<div>`  标签包裹所有标签，`vue3 `  不需要

```
<template>
  <header></header>
  <main></main>
  <footer></footer>
</template>
```

## 为什使用pinia代替vuex

> 忘了vuex是什么了，本身就没写过多少状态管理

Pinia 是 Vue 的专属状态管理库，它允许你跨组件或页面共享状态。

支持ts，服务器端渲染

