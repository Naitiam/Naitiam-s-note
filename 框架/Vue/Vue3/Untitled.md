> https://juejin.cn/post/7245682364932472888#heading-6

### 概括一下vue2和vue3区别

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

### vue2

```
<script>
export default {
  mounted() {   // 直接调用生命周期钩子
    // ... 
  },
}
</script>
```

### vue3

```
<script lang="ts">
export default defineComponent({
	name: 'App',
	components: {组件名,组件名},
  setup(props, context) {
    // ...
  },           
})
</script> 
```

#### setup() 函数

- ```
  setup(props, context) {}
  ```
  
  context 参数是一个对象，对象里面存在 attrs、 slots 、emit  三个属性。
  
  直接使用 props、context.attrs、context.slots、context.emit 
  
- ```
  <script setup>
  import { onMounted, computed } from 'vue';   // 使用前需引入生命周期钩子
   
  onMounted(() => {
    // ...
  });
  
  // 计算属性的写法
  // 基本写法
  const fn = computed(() => { ... })
  // 对象写法
  const fn = computed(() => {
      get() {
          return ...
      }
      set(val) { ... }
  })
  </script>
  
  //计算属性模板中的使用，双向绑定
  <input v-model="fn" type="..." />
  ```
  
  使用 `setup` 属性的 `script` 标签。里面的代码会被编译成组件 setup() 函数的内容。与普通的 `<script>` 只在组件被首次引入的时候执行一次不同，`<script setup>` 中的代码会在 **每次组件实例被创建的时候执行**。
  `setup` 函数里的参数，但是可以通过 `defineProps、defineEmits、useAttrs、useSlots `这几个函数来替代

#### 响应式数据 reactive 与 ref

| ref                                        | reactive                 |
| ------------------------------------------ | ------------------------ |
| 简单值的响应式引用                         | 返回一个对象的响应式代理 |
| 可以定义基本的数据类型，也可以定义引用类型 | 只能够定义引用数据类型   |
| 使用.value属性来访问和更新这个值           | 直接访问对象的属性       |

使用 **`toRefs`** 函数将一个响应式对象转换为可引用的对象,在setup函数中返回多个属性。

```
// 定义一个类型
interface Example{
  id: number
  name: string
}
// ...
 setup(props, context) {
    // ...         
		const count = ref(1)
    const obj = reactive<{ exam: Example[] }>({
    	exam:[{},{},{}]
    })
    const fn = () => {}
    return {
    	count,
    	// 返回其北部多个属性后，模板中可直接使用 :exam="exam"
    	...toRefs(obj),
    	fn
    }
  }
// ...
```

####  父子间数据传递

```
// 父组件，单向数据绑定
<List :exam="exam" :fn="fn"></List>

// 子组件，接收
<script lang="ts">
// ...
  props: {
    exam: {
      type: Array as () => exam[],
      required: true
    },
    fn: {
      type: Function,
      required: true
    }
  },
  setup(props) {
  	// 使用
  	// props.exam
  	// props.fn()
  }
// ...
</script>

<script setup lang="ts">

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

### 为什使用pinia代替vuex

> 忘了vuex是什么了，本身就没写过多少状态管理

Pinia 是 Vue 的专属状态管理库，它允许你跨组件或页面共享状态。

支持ts，服务器端渲染