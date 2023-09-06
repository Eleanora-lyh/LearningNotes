## 1、前置知识

### 1.1、模块加载原理和加载方式

Node.js中的模块可以分为原生模块和文件模块。在Node.js中可以通过`require`方法导入模块、exports方法导出模块。

#### 1.1.0、需要注意的点

ES6 导出和 CommonJS 导出不能混用（即导出的时用了两种，错误写法如下）

```javascript
module.exports = { util};
export { x }; 
```

用了就会报如下方的错误，这个问题其实是在打包的 时候经过`bablejs`处理过程中产生的问题，修改bablejs文件可以同时使用两种写法，但是经试验后未成功，参考链接：https://lete114.github.io/article/webpack-es6-commonjs-export.html

![image-20230906111707102](D:\LYH\learning\LearningNotes\TyporaImgs\image-20230906111707102.png)

module.exports及require是属于commonJS，而export default及import则属于ES6。如果导出用了ES6 ，导入用CommonJS 是没有问题的，同理如果导出用了CommonJS ，导入用ES6 也是没有问题的。只有导出混用两种写法会报错哦！

#### 1.1.1、commonJS的require导入模块

先导出再导入

```javascript
module.exports = { util, x };
```

```javascript
const { x, util } = require('./utils/commonUtils');
var arr = [1, 2, 2, 2, 3];
console.log(util.noRepeat(arr));
console.log(util.add(arr));
x;
```

![image-20230906114914614](D:\LYH\learning\LearningNotes\TyporaImgs\image-20230906114914614.png)

**import 和 require的区别**：https://juejin.cn/post/7205487413350498360

```javascript
import { func1, func2 } from './myModule';
```
```javascript
const myModule = require('./myModule');
```

#### 1.1.2、commonJS的exports导出模块

一个模块中的变量和方法只能用于这个模块，如果想要与其他模块共享一些方法、属性等，就可以用exports导出一个对象。这个对象可以包含想要与其他模块共享的方法和属性等.

新建一个js文件位置为：src/utils/commonUtils，其中写下导出的方法

```javascript
const util = {
    noRepeat: function (arr) {
        return arr.filter(function (ele, index) {
            return arr.indexOf(ele) == index;
        });
    },
    add: function (arr) {
        return arr.reduce(function (a, b) {
            return a + b;
        })
    }
};
module.exports = util; 
```

省略function和return的匿名函数的写法（第二个方法更容易看懂些）

```javascript
const util = {
    noRepeat: arr =>
        arr.filter((ele, index) =>
            arr.indexOf(ele) == index)
    ,
    add: (arr) => {
        return arr.reduce((a, b) =>
            a + b
        )
    }
};
module.exports = util;
```



其中javascript中的.filter可以参考MDN文档：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

``indexOf(ele)``会获取该元素第一次出现的位置，所以``arr.indexOf(ele) == index``能够过滤掉在后面出现的重复元素。



在调用的时候使用require导入模块，导入时由于是默认导入所以可以改名字：

```javascript
    const func = require('./utils/commonUtils');
    var arr = [1,2,2,2,3];
    console.log(func.noRepeat(arr));
    console.log(func.add(arr));
```

调用的效果图：

![image-20230905142427855](D:\LYH\learning\LearningNotes\TyporaImgs\image-20230905142427855.png)



#### 1.1.3、ES6 的require导出、导入模块

```javascript
export { x, util };
```

```javascript
<script>
import { x, util } from "./utils/commonUtils";

export default {
  name: "App",
  data() {
    var arr = [1, 2, 2, 2, 3];
    console.log(util.noRepeat(arr));
    console.log(util.add(arr));
    x;
  },
};
</script>
```



### 1.2、es6 Pormise

异步请求包装为promise对象，异步执行成功调用resolve，若需将任务完成后的值传给下一个一步任务，则将值放到resolve中

```javascript
const x = new Promise((resolve, reject) => {
    province = '黑龙江省'
    setTimeout(() => {
        console.log(province)
        resolve(province)
    }, 1000)
    //任务完成时执行then
}).then(res => {
    // eslint-disable-next-line
    return new Promise((resolve, reject) => {
        city = '哈尔滨市'
        setTimeout(() => {
            console.log(res + city)
            resolve({ province, city })
        }, 1000)
    })
}).then(res => {
    // eslint-disable-next-line
    return new Promise((resolve, reject) => {
        region = '双城区'
        setTimeout(() => {
            console.log(res.province + res.city + region)
        }, 1000)
    })
})

export { x }; 
```

```javascript
<script>
import { x, util } from "./utils/commonUtils";

export default {
  name: "App",
  data() {
    x;
  },
};
</script>
```

```javascript
createApp(App).mount('#app')
```

等价于

```javascript
let app = createApp(App);
app.mount();
```

## 2、VueRouter安装

- npm安装VueRouter

- ```powershell
  npm install vue-router@4
  ```

  npm安装yarn

  ```powershell
  npm install --global yarn
  ```

  

## 3、在html中测试vue router

### 代码：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>

    <body>
        <div id="app">
            <h1>Hello App!</h1>
            <p>
                <!--使用 router-link 组件进行导航 -->
                <!--通过传递 `to` 来指定链接 -->
                <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
                <router-link to="/">Go to Home</router-link>
                <router-link to="/about">Go to About</router-link>
            </p>
            <!-- 路由出口 -->
            <!-- 路由匹配到的组件将渲染在这里 -->
            <router-view></router-view>
        </div>
        <script src="https://unpkg.com/vue@3"></script>
        <script src="https://unpkg.com/vue-router@4"></script>
        <script>
            // 1. 定义路由组件.
            // 也可以从其他文件导入
            const Home = { template: '<div>Home</div>' }
            const About = { template: '<div>About</div>' }

            // 2. 定义一些路由
            // 每个路由都需要映射到一个组件。
            // 我们后面再讨论嵌套路由。
            const routes = [
                { path: '/', component: Home },
                { path: '/about', component: About },
            ]

            // 3. 创建路由实例并传递 `routes` 配置
            // 你可以在这里输入更多的配置，但我们在这里
            // 暂时保持简单
            const router = VueRouter.createRouter({
                // 4. 内部提供了 history 模式的实现。为了简单起见，我们在这里使用 hash 模式。
                history: VueRouter.createWebHashHistory(),
                routes, // `routes: routes` 的缩写
            })
            // 5. 创建并挂载根实例
            const app = Vue.createApp({})
            //确保 _use_ 路由实例使
            //整个应用支持路由。
            app.use(router)

            app.mount('#app')
        </script>
    </body>

</html>
```

### 效果：

点击Go to Home 则在``<router-view></router-view>``处加载``/``地址所指的页面内容；点击Go to About则在``<router-view></router-view>``处加载``/About``地址所指的页面内容

![vueRouter](D:\LYH\learning\LearningNotes\TyporaImgs\vueRouter.gif)

## 4、在vue项目中测试vue router

在显示主页信息的 app.vue中，描述显示内容

```vue
<template>

  <div id="app">
    <h1>Hello App!</h1>
    <p>
      <!--使用 router-link 组件进行导航 -->
      <!--通过传递 `to` 来指定链接 -->
      <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
      <router-link to="/">Go to Home</router-link>
      <router-link to="/about">Go to About</router-link>
    </p>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </div>
</template> 

<script>

export default {
  name: "App",
  components: {
  },
  data() {
    return {
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```

在components中新建两个组件用来分别显示Home和About页面

```vue
<template>
    <div>
        this is about
    </div>
</template>

<script>

export default {
    
}
</script>

<style lang="scss" scoped></style>

```

在 main.js中配置路由

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import { createRouter, createWebHashHistory } from 'vue-router'
import Home from './components/Home.vue'
import About from './components/About.vue'

// 1. 定义路由组件.
// 也可以从其他文件导入
// const Home = { template: '<div>Home</div>' }
// const About = { template: '<div>About</div>' }

// 2. 定义一些路由
// 每个路由都需要映射到一个组件。
// 我们后面再讨论嵌套路由。
const routes = [
    { path: '/', component: Home },
    { path: '/about', component: About },
]

// 3. 创建路由实例并传递 `routes` 配置
// 你可以在这里输入更多的配置，但我们在这里
// 暂时保持简单
const router = createRouter({
    // 4. 内部提供了 history 模式的实现。为了简单起见，我们在这里使用 hash 模式。
    history: createWebHashHistory(),
    routes, // `routes: routes` 的缩写
})

// createApp(App).mount('#app')
let app = createApp(App)

app.use(router)

app.mount('#app')

```

