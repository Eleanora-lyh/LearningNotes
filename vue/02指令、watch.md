详细看：https://cn.vuejs.org/guide/essentials/watchers.html

## 1、声明式渲染 ref 和 reactive（响应系统的核心）

reactive：接收一个普通对象然后返回该普通对象的响应式代理

ref：可以将 `ref` 看成 `reactive` 的一个变形版本，这是由于 `reactive` 内部采用 [Proxy](https://vue3js.cn/es6/) 来实现，而 `Proxy` 只接受对象作为入参，这才有了 `ref` 来解决值类型的数据响应，如果传入 `ref` 的是一个对象，内部也会调用 `reactive` 方法进行深层响应转换 

```
<script setup>
import { ref } from 'vue'
import {reactive} from 'vue'
  
const counter = reactive({ //只适用于对象，如数组、map、set
  count:0 //声明一个变量，赋值为reactive对象，对象中包括一个count属性
})
console.log(counter.count)
counter.count--
  
const message = ref('Hello World!')
console.log(message.value)
message.value = 'changed'
// 组件逻辑
// 此处声明一些响应式状态
</script>


<template>
<h1>{{ message }}</h1>
<p>count is: {{ counter.count }}</p>
</template>
```

效果：

![img](https://uploader.shimo.im/f/FJtwsM4obYv1sC8j.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

```
{{ message }} 访问变量值
```

## 2、Attribute 绑定：v-bind

给 attribute 绑定一个动态值，需要使用 v-bind 指令 (v-bind:class="titleClass"中的v-bind可省略）

- 如果绑定的值是 `null` 或者 `undefined`，那么该 attribute 将会从渲染的元素上移除。 

![img](https://uploader.shimo.im/f/Rldp1joej1sJqoCy.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

 

- 布尔型 Attribute

 

## 3、事件监听：v-on

使用 v-on 指令监听 DOM 事件，简写为 @

 

![img](https://uploader.shimo.im/f/QdLmLW8flUlW6X5h.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

 

## 4、表单绑定：v-model

简化双向绑定，Vue 提供了一个 v-model 指令 ,`v-model` 会将被绑定的值与 `<input>` 的值自动同步，这样我们就不必再使用事件处理函数了 

![img](https://uploader.shimo.im/f/swr4TInEPz9NumlG.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

## 5、条件渲染：v-if

我们可以使用 `v-if` 指令来有条件地渲染元素 

![img](https://uploader.shimo.im/f/V9dtCkfS1IoaMrwW.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

## 6、列表渲染：v-for

我们可以使用 `v-for` 指令来渲染一个基于源数组的列表 

我们还给每个 todo 对象设置了唯一的 `id`，并且将它作为[特殊的 ](https://cn.vuejs.org/api/built-in-special-attributes.html#key)`key`[ attribute](https://cn.vuejs.org/api/built-in-special-attributes.html#key) 绑定到每个 `<li>`。`key` 使得 Vue 能够精确的移动每个 `<li>`，以匹配对应的对象在数组中的位置 

![img](https://uploader.shimo.im/f/KrO7bZMPjR6P1Mrc.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

## 7、计算属性：computed()

介绍一个新 API：`computed()`。它可以让我们创建一个计算属性 ref，这个 ref 会动态地根据其他响应式数据源来计算其 `.value`： 

![img](https://uploader.shimo.im/f/KUmdVTRiapszws6F.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

![img](https://uploader.shimo.im/f/9BxVdSDuBwoQSK3H.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

```
<script setup>
import { ref, computed } from 'vue'


let id = 0


const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])


const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
 	  //todos.value.filter((t) => t.done == false)
    : todos.value
})


const filteredTodos2 =  hideCompleted.value
    ? todos.value.filter((t) => !t.done)
 	  //todos.value.filter((t) => t.done == false)
    : todos.value




function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}


function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>
```

 

 

```
<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos2" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>


<style>
.done {
  text-decoration: line-through;
}
</style>
```

## 8、生命周期和模板引用

生命周期：https://cn.vuejs.org/guide/essentials/lifecycle.html#registering-lifecycle-hooks

模版语法：https://cn.vuejs.org/guide/essentials/template-syntax.html#raw-html

每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。

![img](https://uploader.shimo.im/f/b1Opxh4NvCP5ksC5.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)

 

## 9、侦听器：watch(pram,func)

当一个数字改变时将其输出到控制台。我们可以通过侦听器来实现它：

![img](https://uploader.shimo.im/f/gELUTlmjzXAzbzxR.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)除了在监听到变化后调用匿名方法外，还可以填入函数名

这里此外还处理了当接口请求过程中暂时没有返回值的情况：

- todoData=null时显示Loading
- 获取到结果时todoData!=null，显示todoData

![img](https://uploader.shimo.im/f/XOGlNevqoMgDHKZV.png!thumbnail?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTQ3NDIyNjgsImZpbGVHVUlEIjoiOTAzMEpSS0J5S3NvUDFrdyIsImlhdCI6MTY5NDc0MTk2OCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjo5MDUyNzEzN30.pTmkyhH60L2EJK-c9DlMEH25IVPPDzwLvsbR8J1ebvg)