---
title: Vue复习Todo案例
date: 2023-09-23
tags: 
description:
---

## Vue2

[ToDoList案例 $nextTick](../基础/ToDoList案例%20$nextTick.md)

```
数据
data() {
	return {
		todos: {
			type: Array,
			required: true,
			default: []
		}
	}
}
父传子
子 接收 props:[]
父
中有方法 exam()
模板 <Item @exam=“exam” />
子通过 this.$emit("exam",传给父的值)
```



## Vue3

*src\renderer\src\App.vue*

```
<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue'
import Input from './components/Input.vue'
import List from './components/List.vue'
import Footer from './components/Footer.vue'
import { Todo } from './types/todo'
export default defineComponent({
  name: 'App',
  components: {
    // eslint-disable-next-line vue/no-reserved-component-names
    Input,
    List,
    // eslint-disable-next-line vue/no-reserved-component-names
    Footer
  },
  setup() {
    const obj = reactive<{ todos: Todo[] }>({
      todos: [
        { id: 1, task: '吃饭', isCompleted: false },
        { id: 2, task: '睡觉', isCompleted: false },
        { id: 3, task: '打代码', isCompleted: false }
      ]
    })
    const addTodo = (todo) => {
      obj.todos.unshift(todo)
    }
    const deleteTodo = (index: number) => {
      obj.todos.splice(index, 1)
    }
    const updateTodo = (todo: Todo, isCompleted: boolean) => {
      todo.isCompleted = isCompleted
      console.log(todo)
    }
    const checkAll = (isCompleted: boolean) => {
      obj.todos.forEach((todo) => {
        todo.isCompleted = isCompleted
      })
    }
    const delCompleted = () => {
      obj.todos = obj.todos.filter((todo) => !todo.isCompleted)
    }
    return {
      // 使用toRefs函数将一个响应式对象转换为可引用的对象,在setup函数中返回多个属性
      ...toRefs(obj),
      addTodo,
      deleteTodo,
      updateTodo,
      checkAll,
      delCompleted
    }
  }
})
</script>

<template>
  <div>
    <el-card class="box-card">
      <div class="card-header">
        <Input :add-todo="addTodo"></Input>
      </div>
      <!-- 属性命名方式改变：驼峰转为 - 来连接 -->
      <List :todos="todos" :delete-todo="deleteTodo" :update-todo="updateTodo"></List>
      <Footer :todos="todos" :check-all="checkAll" :del-completed="delCompleted"></Footer>
    </el-card>
  </div>
</template>

<style lang="less" scoped></style>
```

*src\renderer\src\components\List.vue*

```
<script lang="ts">
import { defineComponent } from 'vue'
import Item from './Item.vue'
export default defineComponent({
  name: 'List',
  components: {
    Item
  },
  props: ['todos', 'deleteTodo', 'updateTodo']
})
</script>

<template>
  <div>
    <Item
      v-for="(todo, index) in todos"
      :key="todo.id"
      :todo="todo"
      :update-todo="updateTodo"
      :delete-todo="deleteTodo"
      :index="index"
    ></Item>
  </div>
</template>

<style lang="less" scoped></style>
```

*src\renderer\src\components\Item.vue*

```
<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import { Todo } from '../types/todo'
export default defineComponent({
  name: 'Item',
  props: {
    todo: {
    	// 类型断言，typeScript 编译器将该对象视为一个无参数返回类型为 Todo 的函数
      type: Object as () => Todo,
      required: true
    },
    deleteTodo: {
      type: Function,
      required: true
    },
    updateTodo: {
      type: Function,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  setup(props) {
    const bgColor = ref('white')
    const myColor = ref('black')
    const isShow = ref(false)
    const mouseHandler = (flag: boolean) => {
      if (flag) {
        bgColor.value = 'pink'
        myColor.value = 'green'
        isShow.value = true
      } else {
        bgColor.value = 'white'
        myColor.value = 'black'
        isShow.value = false
      }
    }
    const delTodo = () => {
      if (window.confirm('确定要删除嘛')) {
        props.deleteTodo(props.index)
      }
    }
    const isCompete = computed({
      get() {
        return props.todo.isCompleted
      },
      set(val) {
        props.updateTodo(props.todo, val)
      }
    })
    return {
      mouseHandler,
      bgColor,
      myColor,
      isShow,
      delTodo,
      isCompete
    }
  }
})
</script>

<template>
  <li
    :style="{ backgroundColor: bgColor, color: myColor }"
    @mouseenter="mouseHandler(true)"
    @mouseleave="mouseHandler(false)"
  >
    <input v-model="isCompete" type="checkbox" />
    <span>{{ todo.task }}</span>
    <el-button v-show="isShow" type="danger" size="small" @click="delTodo" round>Danger</el-button>
  </li>
</template>

<style lang="less" scoped></style>
```

*src\renderer\src\components\Input.vue*

```
<script lang="ts">
import { defineComponent, ref } from 'vue'
export default defineComponent({
  name: 'Input',
  props: {
    addTodo: {
      type: Function,
      required: true
    }
  },
  setup(props) {
    const task = ref('')
    const add = () => {
      const text = task.value
      if (!text.trim()) return
      const todo = {
        id: Date.now(),
        task: text,
        isCompleted: false
      }
      props.addTodo(todo)
      task.value = ''
    }
    return {
      task,
      add
    }
  }
})
</script>

<template>
  <input v-model="task" type="text" name="" placeholder="输入，回车确认" @keyup.enter="add" />
</template>

<style lang="" scoped></style>
```

*src\renderer\src\components\Footer.vue*

```
<script lang="ts">
import { defineComponent, computed } from 'vue'
import { Todo } from '../types/todo'
export default defineComponent({
  // eslint-disable-next-line vue/no-reserved-component-names
  name: 'Footer',
  components: {},
  props: {
    todos: {
      type: Array as () => Todo[],
      required: true
    },
    checkAll: {
      type: Function,
      required: true
    },
    delCompleted: {
      type: Function,
      required: true
    }
  },
  setup(props) {
    const count = computed(() => {
      return props.todos.reduce((pre, todo, index) => pre + (todo.isCompleted ? 1 : 0), 0)
    })
    const isCheckAll = computed({
      get() {
        return (count.value > 0 && props.todos.length) === count.value
      },
      set(val) {
        props.checkAll(val)
      }
    })
    return {
      count,
      isCheckAll
    }
  }
})
</script>

<template>
  <div>
    <input v-model="isCheckAll" type="checkbox" />
    <span>已完成{{ count }}/全部{{ todos.length }}</span>
    <el-button type="danger" @click="delCompleted">Default</el-button>
  </div>
</template>

<style lang="" scoped></style>
```

