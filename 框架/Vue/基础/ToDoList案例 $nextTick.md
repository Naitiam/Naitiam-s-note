## 目录

*   [ToDoList案例 \$nextTick](#todolist案例-nexttick)

*   [\$nextTick](#nexttick)

*   [ToDoList案例](#todolist案例)

# ToDoList案例 \$nextTick

# \$nextTick

语法： `this.$nextTick(回调函数)`

作用：在下一次dom更新结束后执行其指定的回调

什么时候用：当改变数据后，要基于更新后的新dom进行某些操作时，要在nextTick所指定的回调函数中执行。

# ToDoList案例

src/main.js

```
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  beforeCreate(){
    Vue.prototype.$bus = this;
  }
}).$mount('#app')

```

src/App.vue

```
<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <!-- <MyHeader :addTodo="addTodo" /> -->
        <!-- 添加自定义事件 -->
        <MyHeader @addTodo="addTodo" />
        <!-- <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" /> -->
        <MyList :todos="todos" />
        <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo" />
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyList from './components/MyList.vue'
import MyFooter from './components/MyFooter.vue'
import pubsub from 'pubsub-js'

export default {
    name: "App",
    components: { MyHeader, MyList, MyFooter },
    data(){
      return {
          todos:JSON.parse(localStorage.getItem('todos')) || []
      }
    },
    methods:{
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      checkTodo(msgName,id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      updateTodo(id,title){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.title = title
        })
      },
      deleteTodo(id){
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      checkAllTodo(done){
        this.todos.forEach((todo)=>{
          todo.done = done
        })
      },
      clearAllTodo(){
        this.todos = this.todos.filter(todo => !todo.done)
      }
    },
    watch:{
      // todos(value){
        // localStorage.setItem('todos',JSON.stringify(value)) 
        // 单纯的监视不会检测到对象内部数值的变化,比如这里的勾选done的true和false
      // }
      todos:{
        deep:true,
        handler(value){
          localStorage.setItem('todos',JSON.stringify(value)) 
        }
      }
    },
    mounted(){
      this.pubId = pubsub.subscribe('checkTodo',this.checkTodo);
      this.$bus.$on('deleteTodo',this.deleteTodo);
      this.$bus.$on('updateTodo',this.updateTodo);
    },
    destroyed(){
      pubsub.unsubscribe(this.$childrenpubId);
      this.$bus.$off('deleteTodo');
      this.$bus.$off('updateTodo');
    }
}

</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-edit {
  color: #fff;
  background-color: #49acda;
  border: 1px solid #2f89bd;
  margin-right: 5px;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>

```

src/components/myHeader.vue

```
<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
    </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
    name:'MyHeder',
    // props:['addTodo'],
    data(){
      return{
        title:""
      }
    },
    methods:{
      add(){
        const todoObj = { id:nanoid(), title:this.title, done:false }
        // this.addTodo(todoObj)
        this.$emit("addTodo",todoObj);
        this.title = ""
      }
    }
}
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
```

src/components/myList.vue

```
<template>
  <ul class="todo-main">
    <MyItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
  </ul>
</template>

<script>
import MyItem from './MyItem'
export default {
    name:'MyList',
    components:{MyItem},
    props:['todos','checkTodo','deleteTodo']
}
</script>
<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
```

src/components/myItem.vue

```
<template>
    <li>
        <label>
            <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
            <!-- <input type="checkbox"  v-model="todo.done" /> -->
            <span v-show="!todo.isEdit">{{todo.title}}</span>
            <input v-show="todo.isEdit" type="text" :value="todo.title" ref="inputTitle" @blur="handleBlur(todo,$event)">
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
        <button class="btn btn-edit" v-show="!todo.isEdit" @click="handleEdit(todo)">编辑</button>
    </li>
</template>

<script>
import pubsub from 'pubsub-js'

export default {
    name: 'MyItem',
    // props:['todo','checkTodo','deleteTodo'],
    props:['todo'],
    methods:{
        handleCheck(id){
            // this.checkTodo(id)
            // this.$bus.$emit('checkTodo',id);
            pubsub.publish('checkTodo',id);
        },
        handleDelete(id){
            // this.deleteTodo(id)
            this.$bus.$emit('deleteTodo',id);
        },
        handleEdit(todo){
            // todo.isEdit = true;//dame
            // console.log(todo);//会有isEdit属性但不是响应式的，没有getset方法
            if(todo.isEdit != undefined){//或者todo.hasOwnProperty.call('isEdit')，检测todo中有无isEdit这个属性
                todo.isEdit = true;
            }else{
                this.$set(todo,'isEdit',true);//给todo添加新属性
            }
            //执行本方法后inpu框才出现
            //所以要进行异步操作
            //setTimeout或者nextTick
            //定时器是异步的宏任务。需要等到全部同步任务执行结束和异步微调任务结束才能执行
            // setTimeout(()=>{
            //     this.$refs.inputTitle.focus()
            // })
            this.$nextTick(function(){
                this.$refs.inputTitle.focus()
            })
        },
        handleBlur(todo,e){
            todo.isEdit = false;
            if(!e.target.value.trim()) return alert('输入不能为空！')
            this.$bus.$emit('updateTodo',todo.id,e.target.value)
        }
    }
}
</script>

<style scoped>
/*item*/
li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
}

li label {
    float: left;
    cursor: pointer;
}

li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
}

li button {
    float: right;
    display: none;
    margin-top: 3px;
}

li:before {
    content: initial;
}

li:last-child {
    border-bottom: none;
}
li:hover{
    background-color: #ddd;
}
li:hover button{
    display: block;
}
</style>
```

src/components/myFooter.vue

```
<template>
  <div class="todo-footer" v-show="total">
        <label>
          <input type="checkbox" :checked="isAll" @change="checkAll"/>
        </label>
        <span>
          <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
      </div>
</template>

<script>
export default {
    name:'MyFooter',
    // props:['todos','checkAllTodo','clearAllTodo'],
    props:['todos'],
    computed:{
      total(){
        return this.todos.length  
      },
      doneTotal(){
        //方法一
        // let i = 0
        // this.todos.forEach((todo)=>{
        //   if(todo.done) i++
        // }) 
        // return i 
        return this.todos.reduce((pre,current)=>{
          console.log("#",pre,current)
          return pre + (current.done?1:0)
        },0)
      },
      isAll(){
        return this.total === this.doneTotal && this.total>0
      },
    },
    methods:{
      checkAll(e){
        console.log("checkall"+e.target)
        // this.checkAllTodo(e.target.checked)
        this.$emit('checkAllTodo',e.target.checked)
      },
      clearAll(){
        // this.clearAllTodo()
        this.$emit("clearAllTodo")
      }
    }
}
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
```
