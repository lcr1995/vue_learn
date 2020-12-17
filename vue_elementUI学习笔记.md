# element UI

## 如何使用element UI

- 在HTML中引入VUE和element UI

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
```

- ​    使用npm以及vue-cli脚手架来创建vue项目并引入element UI

```vue
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
```

## 组件学习

### Basic



### Form

####  Form 表单

##### 使用说明：

- `<el-from>`为整个表单，在`<el-from>`中可以放置多个表单域`<el-form-item>`，在表单域中放置输入框、选择器、单选框、多选框等控件

- 在 Form 组件中，每一个表单域由一个 Form-Item 组件构成，表单域中可以放置各种类型的表单控件，包括 Input、Select、Checkbox、Radio、Switch、DatePicker、TimePicker
- 当一个 form 元素中只有一个输入框时，在该输入框中按下回车应提交该表单。如果希望阻止这一默认行为，可以在 `<el-form>` 标签上添加 `@submit.native.prevent`。
- `<el-from>`具有以下属性

| 属性名                  | 说明                                                         | 类型    | 可选值                | 默认值 |
| ----------------------- | ------------------------------------------------------------ | ------- | --------------------- | ------ |
| model                   | 表单数据对象                                                 | object  | ——                    | ——     |
| rules                   | 表单验证规则                                                 | object  | ——                    | ——     |
| inline                  | 行内表单模式                                                 | boolean | ——                    | false  |
| label-position          | 表单域标签的位置，如果值为 left 或者 right 时，则需要设置 `label-width` | string  | right/left/top        | right  |
| label-width             | 表单域标签的宽度，例如 '50px'。作为 Form 直接子元素的 form-item 会继承该值。支持 `auto`。 | string  | ——                    | ——     |
| label-suffix            | 表单域标签的后缀                                             | string  | ——                    | ——     |
| hide-required-asterisk  | 是否显示必填字段的标签旁边的红色星号                         | boolean | ——                    | false  |
| show-message            | 是否显示校验错误信息                                         | boolean | ——                    | true   |
| inline-message          | 是否以行内形式展示校验信息                                   | boolean | ——                    | false  |
| status-icon             | 是否在输入框中显示校验结果反馈图标                           | boolean | ——                    | false  |
| validate-on-rule-change | 是否在 `rules` 属性改变后立即触发一次验证                    | boolean | ——                    | true   |
| size                    | 用于控制该表单内组件的尺寸                                   | string  | medium / small / mini | ——     |
| disabled                | 是否禁用该表单内的所有组件。若设置为 true，则表单内组件上的 disabled 属性不再生效 | boolean | ——                    | false  |

- **model**的绑定要使用`:model="fromData"`，不能使用`v-model="fromData"`
- 在`<el-from>`中绑定**rules**时，使用`:rules="ruleFrom"`进行绑定 ，在`<el-from-item>`中定义prop，prop的名称要与ruleFrom中对象键值对应
- **data中的form要和rules结构完全一样，一一对应，在prop中要定义的和v-model的一样**
- :inline="true"

##### 实例：

```vue
<el-form :inline="true" :model="formInline" rules="rules" class="demo-form-inline">
  <el-form-item label="审批人" prop="user">
    <el-input v-model="formInline.user" placeholder="审批人"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="onSubmit">查询</el-button>
  </el-form-item>
</el-form>
<script>
  export default {
    data() {
      return {
        formInline: {
          user: ''
        },
        rules:{
            user:[{required:true,message:'请输入用户名', trigger: 'blur'}]
        }
      }
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      }
    }
  }
</script>
```

##### **注意：**

- **data中的form要和rules结构完全一样，一一对应，在prop中要定义的和v-model的一样**
- 

### Data



### Notice



### Navigation



### Others

# Vue

## [v-on](https://cn.vuejs.org/v2/api/#v-on)

- ### **缩写：**`@`

- ### **参数**：`event`

- ### **修饰符：**

  - `.stop` - 调用 `event.stopPropagation()`。
  - `.prevent` - 调用 `event.preventDefault()`。
  - `.capture` - 添加事件侦听器时使用 capture 模式。
  - `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
  - `.{keyCode | keyAlias}` - 只当事件是从特定键触发时才触发回调。
  - `.native` - 监听组件根元素的原生事件。
  - `.once` - 只触发一次回调。
  - `.left` - (2.2.0) 只当点击鼠标左键时触发。
  - `.right` - (2.2.0) 只当点击鼠标右键时触发。
  - `.middle` - (2.2.0) 只当点击鼠标中键时触发。
  - `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

- ### **用法：**

  绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。

  用在普通元素上时，只能监听[**原生 DOM 事件**](https://developer.mozilla.org/zh-CN/docs/Web/Events)。用在自定义元素组件上时，也可以监听子组件触发的**自定义事件**。

  在监听原生 DOM 事件时，方法以事件为唯一的参数。如果使用内联语句，语句可以访问一个 `$event` property：`v-on:click="handle('ok', $event)"`。

  从 `2.4.0` 开始，`v-on` 同样支持不带参数绑定一个事件/监听器键值对的对象。注意当使用对象语法时，是不支持任何修饰器的。

- ### **示例**：

  ```html
  <!-- 方法处理器 -->
  <button v-on:click="doThis"></button>
  
  <!-- 动态事件 (2.6.0+) -->
  <button v-on:[event]="doThis"></button>
  
  <!-- 内联语句 -->
  <button v-on:click="doThat('hello', $event)"></button>
  
  <!-- 缩写 -->
  <button @click="doThis"></button>
  
  <!-- 动态事件缩写 (2.6.0+) -->
  <button @[event]="doThis"></button>
  
  <!-- 停止冒泡 -->
  <button @click.stop="doThis"></button>
  
  <!-- 阻止默认行为 -->
  <button @click.prevent="doThis"></button>
  
  <!-- 阻止默认行为，没有表达式 -->
  <form @submit.prevent></form>
  
  <!--  串联修饰符 -->
  <button @click.stop.prevent="doThis"></button>
  
  <!-- 键修饰符，键别名 -->
  <input @keyup.enter="onEnter">
  
  <!-- 键修饰符，键代码 -->
  <input @keyup.13="onEnter">
  
  <!-- 点击回调只会触发一次 -->
  <button v-on:click.once="doThis"></button>
  
  <!-- 对象语法 (2.4.0+) -->
  <button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
  ```

  在子组件上监听自定义事件 (当子组件触发“my-event”时将调用事件处理器)：

  ```html
  <my-component @my-event="handleThis"></my-component>
  
  <!-- 内联语句 -->
  <my-component @my-event="handleThis(123, $event)"></my-component>
  
  <!-- 组件中的原生事件 -->
  <my-component @click.native="onClick"></my-component>
  ```

- ### **参考**：

  - [事件处理器](https://cn.vuejs.org/v2/guide/events.html)
  - [组件 - 自定义事件](https://cn.vuejs.org/v2/guide/components.html#监听子组件事件)

## [v-bind](https://cn.vuejs.org/v2/api/#v-bind)

- ### **缩写**：`:`

- ### **参数**：`attrOrProp (optional)`

- ### **修饰符**：

  - `.prop` - 作为一个 DOM property 绑定而不是作为 attribute 绑定。([差别在哪里？](https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html#answer-6004028))
  - `.camel` - (2.1.0+) 将 kebab-case attribute 名转换为 camelCase。(从 2.1.0 开始支持)
  - `.sync` (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 `v-on` 侦听器。

- ### **用法**：

  动态地绑定一个或多个 attribute，或一个组件 prop 到表达式。

  在绑定 `class` 或 `style` attribute 时，支持其它类型的值，如数组或对象。可以通过下面的教程链接查看详情。

  在绑定 prop 时，prop 必须在子组件中声明。可以用修饰符指定不同的绑定类型。

  没有参数时，可以绑定到一个包含键值对的对象。注意此时 `class` 和 `style` 绑定不支持数组和对象。

- ### **示例**：

  ```html
  <!-- 绑定一个 attribute -->
  <img v-bind:src="imageSrc">
  
  <!-- 动态 attribute 名 (2.6.0+) -->
  <button v-bind:[key]="value"></button>
  
  <!-- 缩写 -->
  <img :src="imageSrc">
  
  <!-- 动态 attribute 名缩写 (2.6.0+) -->
  <button :[key]="value"></button>
  
  <!-- 内联字符串拼接 -->
  <img :src="'/path/to/images/' + fileName">
  
  <!-- class 绑定 -->
  <div :class="{ red: isRed }"></div>
  <div :class="[classA, classB]"></div>
  <div :class="[classA, { classB: isB, classC: isC }]">
  
  <!-- style 绑定 -->
  <div :style="{ fontSize: size + 'px' }"></div>
  <div :style="[styleObjectA, styleObjectB]"></div>
  
  <!-- 绑定一个全是 attribute 的对象 -->
  <div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>
  
  <!-- 通过 prop 修饰符绑定 DOM attribute -->
  <div v-bind:text-content.prop="text"></div>
  
  <!-- prop 绑定。“prop”必须在 my-component 中声明。-->
  <my-component :prop="someThing"></my-component>
  
  <!-- 通过 $props 将父组件的 props 一起传给子组件 -->
  <child-component v-bind="$props"></child-component>
  
  <!-- XLink -->
  <svg><a :xlink:special="foo"></a></svg>
  ```

  `.camel` 修饰符允许在使用 DOM 模板时将 `v-bind` property 名称驼峰化，例如 SVG 的 `viewBox` property：

  ```html
  <svg :view-box.camel="viewBox"></svg>
  ```

  在使用字符串模板或通过 `vue-loader`/`vueify` 编译时，无需使用 `.camel`。

- ### 详细使用

  #### **一、绑定HTML Class**

  1. ##### 对象语法

     - 可以使用`v-bind:class`来绑定一个对象，以动态地切换class。**注意：**<u>`v-bind:class`指令可以与普通的class特性共存</u>

     -  代码示例：

       ```html
       <template>
           <div id="app">
               <ul class="box" v-bind:class="{'textColor':isColor, 'textSize':isSize}">
                   <li>学习Vue</li>
                   <li>学习Node</li>
                   <li>学习React</li>
               </ul>
               <ul class="box" :class="classObject"> //等同于上面的
                   <li>学习Vue</li>
                   <li>学习Node</li>
                   <li>学习React</li>
               </ul>
           </div>
       </template>
       <script>
           var vm= new Vue({
               el:'#app',
               data:{
                   isColor:true,
                   isSize:true,
                   classObject:{'textColor':false,'textSize':true}
               }
           })
       </script>
       <style>
           .box{
           	border:1px dashed #f0f;
           }
           .textColor{
               color:#f00;
               background-color:#eef;
           }
           .textSize{
               font-size:30px;
               font-weight:bold;
           }
       </style>
       ```

       从图中可以看到，HTML最终渲染为 `<ul class="box textColor textSize"></ul>`

       当 isColor 和 isSize 变化时，class列表将相应的更新。

       例如，将isSize改成false，class列表将变为`<ul class="box textColor"></ul>`

  2. #####  数组语法

     ###### 把一个数组传给v-bind:class，以应用一个class列表

     ```html
     <ul class="box" :class="[classA, classB]">
         <li>学习Vue</li>
         <li>学习Node</li>
         <li>学习React</li>
     </ul>
     
     var vm= new Vue({
         el:‘.box‘,
         data:{
             classObject:{
                 ‘textColor‘:true,
                 ‘textSize‘:false //不渲染，注意看下面的截图
             }
         }
     })
     ```

     **如果想根据条件切换列表中的class，可以用三目运算**

     ```html
     <ul class="box" :class="[isA?classA:'', classB]">
         <li>学习Vue</li>
         <li>学习Node</li>
         <li>学习React</li>
     </ul>
      
     var vm= new Vue({
         el:‘.box‘,
         data:{
             classA:‘textColor‘,
             classB:‘textSize‘,
             isA:false 
         }
     })
     ```

     在这个例子中，首先判断isA的boolean值，如果为true，则渲染classA；如果为false，则不渲染。classB没有做三目运算，所以是始终显示的，看看页面截图

     ![img](http://s2.51cto.com/wyfs02/M01/89/2F/wKioL1gLFw7zSxVrAACvZz_XHmk974.png)

  #### **二、绑定内联样式**

  1. ##### 对象语法

     ```html
     <ul class="box" :class="classObject">
         <li>学习Vue</li>
         <li>学习Node</li>
         <li>学习React</li>
     </ul>
     
     var vm= new Vue({
         el:‘#box‘,
         data:{
             activeColor:‘#f00‘,
             size:‘30px‘,
             shadow:‘5px 2px 6px #000‘
         }
     })
     
     ```

     

  2. ##### 数组语法

- ### **参考**：

  - [Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html)
  - [组件 - Props](https://cn.vuejs.org/v2/guide/components.html#通过-Prop-向子组件传递数据)
  - [组件 - `.sync` 修饰符](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符)

## [v-model](https://cn.vuejs.org/v2/api/#v-model)



## [v-text](https://cn.vuejs.org/v2/api/#v-text)



## [v-html](https://cn.vuejs.org/v2/api/#v-html)



## [v-pre](https://cn.vuejs.org/v2/api/#v-pre)



## [v-cloak](https://cn.vuejs.org/v2/api/#v-cloak)



## [v-once](https://cn.vuejs.org/v2/api/#v-once)



## [v-if](https://cn.vuejs.org/v2/api/#v-if)



## [v-else](https://cn.vuejs.org/v2/api/#v-else)



## [v-else-if](https://cn.vuejs.org/v2/api/#v-else-if)



## [v-show](https://cn.vuejs.org/v2/api/#v-show)



## [v-for](https://cn.vuejs.org/v2/api/#v-for)



## [v-slot](https://cn.vuejs.org/v2/api/#v-slot)









## VUE Router

### 一、vue-router是什么

这里的路由并不是指我们平时所说的硬件路由器，**这里的路由就是SPA（单页应用）的路径管理器**。再通俗的说，vue-router就是WebApp的链接路径管理系统。
 vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。传统的页面应用，是用一些超链接来实现页面切换和跳转的。在vue-router单页面应用中，则是路径之间的切换，也就是组件的切换。**路由模块的本质 就是建立起url和页面之间的映射关系**。

至于我们为啥不能用a标签，这是因为用Vue做的都是单页应用（**当你的项目准备打包时，运行`npm run build`时，就会生成dist文件夹，这里面只有静态资源和一个index.html页面**），所以你写的<a></a>标签是不起作用的，你必须使用vue-router来进行管理。

### 二、vue-router实现原理

SPA(single page application):单一页面应用程序，只有一个完整的页面；它在加载页面时，不会加载整个页面，而是只更新某个指定的容器中内容。**单页面应用(SPA)的核心之一是: 更新视图而不重新请求页面**;vue-router在实现单页面前端路由时，提供了两种方式：Hash模式和History模式；根据mode参数来决定采用哪一种方式。

#### 1、Hash模式：

**vue-router 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。** hash（#）是URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说**hash 出现在 URL 中，但不会被包含在 http 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面**；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说**Hash模式通过锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据。hash 模式的原理是 onhashchange 事件(监测hash值变化)，可以在 window 对象上监听这个事件**。

#### 2、History模式：

由于hash模式会在url中自带#，如果不想要很丑的 hash，我们可以用路由的 history 模式，只需要在配置路由规则时，加入"mode: 'history'",**这种模式充分利用了html5 history interface 中新增的 pushState() 和 replaceState() 方法。这两个方法应用于浏览器记录栈，在当前已有的 back、forward、go 基础之上，它们提供了对历史记录修改的功能。只是当它们执行修改时，虽然改变了当前的 URL ，但浏览器不会立即向后端发送请求**。

```csharp
//main.js文件中
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

当你使用 history 模式时，URL 就像正常的 url，例如 [http://yoursite.com/user/id](https://links.jianshu.com/go?to=http%3A%2F%2Fyoursite.com%2Fuser%2Fid)，比较好看！
 不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 [http://oursite.com/user/id](https://links.jianshu.com/go?to=http%3A%2F%2Foursite.com%2Fuser%2Fid) 就会返回 404，这就不好看了。
 所以呢，**你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。**

```cpp
 export const routes = [ 
  {path: "/", name: "homeLink", component:Home}
  {path: "/register", name: "registerLink", component: Register},
  {path: "/login", name: "loginLink", component: Login},
  {path: "*", redirect: "/"}]
```

此处就设置如果URL输入错误或者是URL 匹配不到任何静态资源，就自动跳到到Home页面

### 三、使用路由模块来实现页面跳转的方式

- 方式1：直接修改地址栏
- 方式2：this.$router.push(‘路由地址’)
- 方式3：`<router-link to="路由地址"></router-link>`

### 四、vue-router的基本使用

1:下载 `npm i vue-router -S`
2:在main.js中引入 `import VueRouter from 'vue-router'`;
3:安装插件`Vue.use(VueRouter)`;
4:创建路由对象并配置路由规则 `let router = new VueRouter({routes:[{path:'/home',component:Home}]})`;
5:将其路由对象传递给Vue的实例，options中加入 `router:router`
6:在app.vue中留坑 `<router-view></router-view>`

具体实现请看如下代码：

```javascript
//main.js文件中引入
import Vue from 'vue';
import VueRouter from 'vue-router';
//主体
import App from './components/app.vue';
import Home from './components/home.vue'
//安装插件
Vue.use(VueRouter); //挂载属性
//创建路由对象并配置路由规则
let router = new VueRouter({
    routes: [
        //一个个对象
        { path: '/home', component: Home }
    ]
});
//new Vue 启动
new Vue({
    el: '#app',
    //让vue知道我们的路由规则
    router: router, //可以简写router
    render: c => c(App),
})
```

最后记得在在app.vue中“留坑”

```vue
//app.vue中
<template>
    <div>
        <!-- 留坑，非常重要 -->
        <router-view></router-view>
    </div>
</template>
<script>
    export default {
        data(){
            return {}
        }
    }
</script>
```



#### 4.1 基本使用步骤

1. #### **引入相关库文件**

   **注意：先引用Vue，再引用VueRouter**

   ```vue
   <script src="https://unpkg.com/vue/dist/vue.js"></script>
   <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
   ```

2. #### **添加路由链接**

   ```vue
   <router-link to="/user">User</router-link>
   <router-link to="/register">Register</router-link>
   ```

3. #### **添加路由填充位**

   ```vue
   <!-- 路由填充位（也叫做路由占位符） -->
   <!-- 将来通过路由规则匹配到的组件，将会被渲染到 router-view 所在位置 -->
   <router-view></router-view>
   ```

4. #### **定义路由组件**

   ```vue
   var User={
   	template:'<h1>User组件</h1>'
   }
   var Register={
   	template:'<h1>Register组件</h1>'
   }
   ```

5. #### **配置路由规则并创建路由实例**

   ```js
   var router=new VueRouter({
       //routes 是路由规则数组
       routes:[
           //每个路由规则都是一个配置对象，其中至少包含path和component两个属性：
           //path表示当前路由规则匹配的hash地址
           //component表示当前路由规则对应要展示的组件
           {path:'/user',component:User},
           {path:'/register',component:Register}
       ]
   })
   ```

6. #### **把路由挂载到Vue根实例中**

   ```js
   new Vue({
   	el:'#app',
       //为了能够让路由规则生效，必须把路由对象挂载到vue实例对象上
       router
   });
   ```

#### 4.2 路由重定向

路由重定向指的是：用户在访问地址A的时候，强制用户跳转到地址C，从而展示特定的组件页面；

通过路由规则的`redirect`属性，指定一个新的路由地址，可以很方便的设置路由的重定向：

```js
var router = new VueRouter({
    routes:[
        //其中，path表示需要被重定向的原地址，redirect表示将要被重定向的新地址
        {path:'/',redirect:'/user'},
        {path:'/user',component:User},
        {path:'register',component:Register}
    ]
})
```

#### 4.3 嵌套路由用法

##### 4.3.1 功能分析

- 点击父级路由链接显示模板内容
- 模板内容中又有子级路由链接
- 点击子级路由链接显示子级模板内容

##### 4.3.2 父路由组件模板

- 父级路由链接
- 父级路由填充位

```html
<p>
	<router-link to="/user">User</router-link>
	<router-link to="/register">Register</router-link>
</p>
<!-- 路由占位符 -->
<div>
<router-view></router-view>
</div>
```

##### 4.3.3 子级路由模板

- 子级路由链接
- 自己路由填充位

```html
const Register = {
	template:`<div>
        <h1>Register 组件</h1>
        <hr/>
        <router-link to="/register/tab1">Tab1</router-link>
        <router-link to="/register/tab2">Tab2</router-link>
        <!-- 子路由填充位 -->
        <router-view/>
	</div>`
}
```

##### 4.3.4 嵌套路由配置

- 父级路由通过`childern`属性配置子级路由

```js
const router = new VueRouter ({
	routes:[
        {path:'/user',component:User},
        {
            path:'/register',
            component:Register,
            //通过childern属性，为/register添加子路由规则
            childern:[
                {path:'/register/tab1',component:Tab1},
                {path:'/register/tab2',component:Tab2}
            ]
        }
	]
})
```

#### 4.4 动态匹配路由的基本用法

##### 4.4.1 基本使用

- **应用场景：通过动态路由参数的模式进行路由匹配**

```js
var router = new VueRouter({
	routes:[
		//动态路劲参数 以冒号开头
		{path:'/user/:id',component:User}
	]
})
```

```js
const User = {
    //路由组件中通过$route.params获取路由参数
    template:'<div>User {{$route.params.id}}</div>'
}
```

##### 4.4.2 路由组件传递参数

- **$route与对应路由形成高度耦合，不够灵活，所以可以使用props将组件和路由解耦**

###### 1. **props的值为布尔类型**

```js
const router = new VueRouter({
	routes:[
        //如果props被设置为true，route.params将被设置为组件属性
        {path:'/user/:id',component:User,props : true}
    ]
})
const User = {
    props:['id'],//使用props接收路由参数
    template:'<div>用户ID:{{id}}</div>' //使用路由参数
}
```

###### **2.props的值为对象类型**

- **该方法只能传静态参数**

```js
const router = new VueRouter({
	routes:[
        //如果props是一个对象，它会被按照原样设置为组件属性
        {path:'/user/:id',component:User,props : {uname:'lisi',age:12}}
    ]
})
const User = {
    props:['uname','age'],//使用props接收路由参数
    template:'<div>用户ID:{{$route.params.id}} 姓名：{{uname}} 年龄：{{age}}</div>' //使用路由参数
}
```

###### 3.props的值为函数类型

```js
const router = new VueRouter({
    routes:[
        //如果props是一个函数，则这个函数接收 route 对象为自己的参数
        {
            path:'/user/:id',
            components:User,
            props:route=>({uname:'zs',age:20,id:route.params.id})
        }
    ]
})
const User = {
    props:['uname','age','id'],//使用props接收路由参数
    template:'<div>用户ID:{{d}} 姓名：{{uname}} 年龄：{{age}}</div>' //使用路由参数
}
```

#### 4.5 vue-router编程式导航

##### 4.5.1 页面导航的两种方式

- **声明式导航**：通过<u>点击链接</u>实现导航的方式，叫做声明式导航

  例如：普通网页中的<a></a>链接后者vue中的<router-link></router-link>

- 编程式导航：通过调用Javascript形式的API实现导航的方式，叫做编程式导航

  例如：普通网页中的location.href

##### 4.5.2 编程式导航基本用法

常用的编程式导航API如下：

- **this.$router.push('hash地址')**

  参数规则：

  ```js
  //字符串（路径名称）
  router.push('/home')
  //对象
  router.push({path:'/home'})
  //命名的路由（传递参数）
  router.push({name:'/user',params:{userId:123}})
  //带查询参数，变成 /register?uname=lisi
  router.push({path:'/register',query:{uname:'lisi'}})
  ```

  

- **this.$router.go(n)**

```js
const User = {
    template:'<div><button @click="goRegister">跳转到注册页面</button></div>',
 	methods:{
        goRegister:function(){
            //用编程式导航控制路由跳转
            this.$router.push('/register');
        }
    }
}
```





#### 4.6vue-router命名路由

##### 4.6.1 命令路由的配置规则

为了更加方便的表示路由的路径，可以给路由规则起一个别名，即“命名路由”

```js
const router = new VueRouter({
    routes:[
        {
            path:'/user/:id',
            name:'user',
            component:User
        }
    ]
})
//使用命名路由实现页面的跳转
<router-link :to="{name:'user',params:{id:123}}">User</router-link>
router.push({name:'user',params:{id:123}})
```



### 五、 vue-router参数传递

声明式的导航`<router-link :to="...">`和编程式的导航`router.push(...)`都可以传参，本文主要介绍前者的传参方法，同样的规则也适用于编程式的导航。

#### 1.用name传递参数

在路由文件src/router/index.js里配置name属性

```bash
routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    }
]
```

模板里(src/App.vue)用`$route.name`来接收 比如：`<p>{{ $route.name}}</p>`

#### 2 通过`<router-link>` 标签中的to传参

这种传参方法的基本语法：

```ruby
<router-link :to="{name:xxx,params:{key:value}}">valueString</router-link>
```

比如先在src/App.vue文件中

```xml
<router-link :to="{name:'hi1',params:{username:'jspang',id:'555'}}">Hi页面1</router-link>
```

然后把src/router/index.js文件里给hi1配置的路由起个name,就叫hi1.

```css
{path:'/hi1',name:'hi1',component:Hi1}
```

最后在模板里(src/components/Hi1.vue)用`$route.params.username`进行接收.

```bash
{{$route.params.username}}-{{$route.params.id}}
```

#### 3 利用url传递参数----在配置文件里以冒号的形式设置参数。

我们在/src/router/index.js文件里配置路由

```css
{
    path:'/params/:newsId/:newsTitle',
    component:Params
}
```

我们需要传递参数是新闻ID（newsId）和新闻标题（newsTitle）.所以我们在路由配置文件里制定了这两个值。

在src/components目录下建立我们params.vue组件，也可以说是页面。我们在页面里输出了url传递的的新闻ID和新闻标题。

```html
<template>
    <div>
        <h2>{{ msg }}</h2>
        <p>新闻ID：{{ $route.params.newsId}}</p>
        <p>新闻标题：{{ $route.params.newsTitle}}</p>
    </div>
</template>
<script>
export default {
  name: 'params',
  data () {
    return {
      msg: 'params page'
    }
  }
}
</script>
```

在App.vue文件里加入我们的`<router-view>`标签。这时候我们可以直接利用url传值了

`<router-link to="/params/198/jspang website is very good">params</router-link>`

#### 4. 使用path来匹配路由，然后通过query来传递参数

```xml
<router-link :to="{ name:'Query',query: { queryId:  status }}" >
     router-link跳转Query
</router-link>
```

对应路由配置：

```css
   {
     path: '/query',
     name: 'Query',
     component: Query
   }
```

于是我们可以获取参数：

```kotlin
this.$route.query.queryId
```

### 六、vue-router配置子路由(二级路由)

实际生活中的应用界面，通常由多层嵌套的组件组合而成。同样地，URL中各段动态路径也按某种结构对应嵌套的各层组件，例如：

![img](https://upload-images.jianshu.io/upload_images/3174701-efce15514ae3acdb)

**如何实现下图效果(H1页面和H2页面嵌套在主页中)**？

![img](https://upload-images.jianshu.io/upload_images/3174701-1d309ac2e4ef990c)

1、首先用`<router-link>`标签增加了两个新的导航链接

```xml
<router-link :to="{name:'HelloWorld'}">主页</router-link>
<router-link :to="{name:'H1'}">H1页面</router-link>
<router-link :to="{name:'H2'}">H2页面</router-link>
```

2、在HelloWorld.vue加入`<router-view>`标签，给子模板提供插入位置

```xml
 <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <router-view></router-view>
  </div>
</template>
```

3、在components目录下新建两个组件模板 H1.vue 和 H2.vue
 两者内容类似，以下是H1.vue页面内容：

```xml
 <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        msg: 'I am H1 page,Welcome to H1'
      }
    }
  }
</script>
```

4、修改router/index.js代码，子路由的写法是在原有的路由配置下加入children字段。

```csharp
   routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld,
      children: [{path: '/h1', name: 'H1', component: H1},//子路由的<router-view>必须在HelloWorld.vue中出现
        {path: '/h2', name: 'H2', component: H2}
      ]
    }
  ]
```

### 七、单页面多路由区域操作

在一个页面里我们有两个以上`<router-view>`区域，我们通过配置路由的js文件，来操作这些区域的内容

1、App.vue文件，在`<router-view>`下面新写了两行`<router-view>`标签,并加入了些CSS样式

```xml
<template>
  <div id="app">
    <img src="./assets/logo.png">
       <router-link :to="{name:'HelloWorld'}"><h1>H1</h1></router-link>
       <router-link :to="{name:'H1'}"><h1>H2</h1></router-link>
    <router-view></router-view>
    <router-view name="left" style="float:left;width:50%;background-color:#ccc;height:300px;"/>
    <router-view name="right" style="float:right;width:50%;background-color:yellowgreen;height:300px;"/>
  </div>
</template>
```

2、需要在路由里配置这三个区域，配置主要是在components字段里进行

```css
export default new Router({
    routes: [
      {
        path: '/',
        name: 'HelloWorld',
        components: {default: HelloWorld,
          left:H1,//显示H1组件内容'I am H1 page,Welcome to H1'
          right:H2//显示H2组件内容'I am H2 page,Welcome to H2'
        }
      },
      {
        path: '/h1',
        name: 'H1',
        components: {default: HelloWorld,
          left:H2,//显示H2组件内容
          right:H1//显示H1组件内容
        }
      }
    ]
  })
```

上边的代码我们编写了两个路径，一个是默认的‘/’，另一个是‘/Hi’.在两个路径下的components里面，我们对三个区域都定义了显示内容。最后页面展示如下图：

![img](https://upload-images.jianshu.io/upload_images/3174701-f4f4f08651834c8e)

### 八.`$route` 和 `$router` 的区别

我们先将这两者console.log打印出来：

![img](https://upload-images.jianshu.io/upload_images/3174701-cb30e26e1485c06a.png)

![img](https://upload-images.jianshu.io/upload_images/3174701-f88eea882545a2e9.png)

**$route 是“路由信息对象”，包括 path，params，hash，query，fullPath，matched，name 等路由信息参数。**

**① `$route.path`**
 字符串，对应当前路由的路径，总是解析为绝对路径，如 "/order"。

**② `$route.params`**
 一个 key/value 对象，包含了 动态片段 和 全匹配片段，
 如果没有路由参数，就是一个空对象。

**③ `$route.query`**
 一个 key/value 对象，表示 URL 查询参数。
 例如，对于路径 /foo?user=1，则有 $route.query.user为1，
 如果没有查询参数，则是个空对象。

**④ `$route.hash`**
 当前路由的 hash 值 (不带 #) ，如果没有 hash 值，则为空字符串。

**⑤ `$route.fullPath`**
 完成解析后的 URL，包含查询参数和 hash 的完整路径。

**⑥ `$route.matched`**
 数组，包含当前匹配的路径中所包含的所有片段所对应的配置参数对象。

**⑦ `$route.name`   当前路径名字**

**$router 是“路由实例”对象，即使用 new VueRouter创建的实例，包括了路由的跳转方法，钩子函数等。**

**$router常见跳转方法:**

```kotlin
<button @click="goToMenu" class="btn btn-success">Let's order！</button>
.....
<script>
  export default{
    methods:{
      goToMenu(){
        this.$router.go(-1)//跳转到上一次浏览的页面
        this.$router.replace('/menu')//指定跳转的地址
        this.$router.replace({name:'menuLink'})//指定跳转路由的名字下
        this.$router.push('/menu')//通过push进行跳转
        this.$router.push({name:'menuLink'})//通过push进行跳转路由的名字下
      }
    }
  }
</script>
```

**`$router.push`和`$router.replace`的区别**：

- 使用push方法的跳转会向 history 栈添加一个新的记录，当我们点击浏览器的返回按钮时可以看到之前的页面。
- 使用replace方法不会向 history 添加新记录，而是替换掉当前的 history 记录，即当replace跳转到的网页后，‘后退’按钮不能查看之前的页面。

### 九、 如何设置404页面

用户会经常输错页面，当用户输错页面时，我们希望给他一个友好的提示页面，这个页面就是我们常说的404页面。vue-router也为我们提供了这样的机制。

1、设置我们的路由配置文件（/src/router/index.js）

```css
{
   path:'*',
   component:Error
}
```

这里的path:'*'就是输入地址不匹配时，自动显示出Error.vue的文件内容

2、在/src/components/文件夹下新建一个Error.vue的文件。简单输入一些有关错误页面的内容。

```xml
<template>
    <div>
        <h2>{{ msg }}</h2>
    </div>
</template>
<script>
export default {
  data () {
    return {
      msg: 'Error:404'
    }
  }
}
</script>
```

此时我们随意输入一个错误的地址时，便会自动跳转到404页面