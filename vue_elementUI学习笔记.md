# HTML

## label

### 定义和用法

<label> 标签为 input 元素定义标注（标记）。

label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

<label> 标签的 for 属性应当与相关元素的 id 属性相同。

### label的`for`属性

<label>是专门为<input>元素服务的，为其定义标记。给 label 加了 for 属性绑定了input控件后，可以提高鼠标用户的用户体检。如果在label 元素内点击文本，就会触发此控件，也就是说，当用户渲染该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

### label 和表单控件绑定

#### 方法一：隐式绑定

将表单控件作为label的内容，此时不需要for属性，绑定的控件也不需要id属性。

```html
隐式绑定：
<label>Date of Birth: <input type="text" name="DofB" /></label>
```

#### 方法二：显示绑定

为label标签下的for属性命名一个目标表单的id

```html
显式绑定：
<label for="SSN">Social Security Number:</label>
<input type="text" name="SocSecNum" id="SSN" />
```



# Vue笔记

## 指令

### [v-on](https://cn.vuejs.org/v2/api/#v-on)

#### **缩写：**`@`

#### **参数**：`event`

#### **修饰符：**

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

#### **用法：**

绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。

用在普通元素上时，只能监听[**原生 DOM 事件**](https://developer.mozilla.org/zh-CN/docs/Web/Events)。用在自定义元素组件上时，也可以监听子组件触发的**自定义事件**。

在监听原生 DOM 事件时，方法以事件为唯一的参数。如果使用内联语句，语句可以访问一个 `$event` property：`v-on:click="handle('ok', $event)"`。

从 `2.4.0` 开始，`v-on` 同样支持不带参数绑定一个事件/监听器键值对的对象。注意当使用对象语法时，是不支持任何修饰器的。

#### **示例**：

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

#### **参考**：

- [事件处理器](https://cn.vuejs.org/v2/guide/events.html)
- [组件 - 自定义事件](https://cn.vuejs.org/v2/guide/components.html#监听子组件事件)

### [v-bind](https://cn.vuejs.org/v2/api/#v-bind)

#### **缩写**：

`:`

#### **参数**：

`attrOrProp (optional)`

#### **修饰符**：

- `.prop` - 作为一个 DOM property 绑定而不是作为 attribute 绑定。([差别在哪里？](https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html#answer-6004028))
- `.camel` - (2.1.0+) 将 kebab-case attribute 名转换为 camelCase。(从 2.1.0 开始支持)
- `.sync` (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 `v-on` 侦听器。

#### **用法**：

动态地绑定一个或多个 attribute，或一个组件 prop 到表达式。

在绑定 `class` 或 `style` attribute 时，支持其它类型的值，如数组或对象。可以通过下面的教程链接查看详情。

在绑定 prop 时，prop 必须在子组件中声明。可以用修饰符指定不同的绑定类型。

没有参数时，可以绑定到一个包含键值对的对象。注意此时 `class` 和 `style` 绑定不支持数组和对象。

#### **示例**：

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

#### 详细使用

##### **一、绑定HTML Class**

1. ###### 对象语法

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

2. ######  数组语法

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
   
   对于多个class,可以这么写：
   
   ```html
   <div v-bind:class="[classA, { classB: isB, classC: isC }]">
   ```
   
   

##### **二、绑定内联样式**

1. ###### 对象语法

   v-bind:style 的对象语法十分直观--非常像CSS，其实它是一个Javascript对象，**CSS属性名必须用驼峰命名法**（官方文档写的是既可以用驼峰也可以用 短横分隔命名法），但是用短横分隔是会报错的

   ```html
   <!-- 错误写法 -->
   <div id="box" :style="{color:activeColor, font-size:size}">红嘴绿鹦哥</div> <!--font-size会报错-->
   <!-- 正确写法 -->
   <div id="box" :style="{color:activeColor, fontSize:size, textShadow:shadow}">红嘴绿鹦哥</div>
   var vm= new Vue({
       el:‘#box‘,
       data:{
           activeColor:‘#f00‘,
           size:‘30px‘,
           shadow:‘5px 2px 6px #000‘
       }
   })
   ```

   **也可以直接绑定到一个样式对象，这样更好，让模板更清晰：**

   ```html
   <div id="box" :style="styleObject">红嘴绿鹦哥</div>
   var vm= new Vue({
       el:‘#box‘,
       data:{
           styleObject:{
               color:‘red‘,
               fontSize:‘30px‘
           }
       }
   })
   ```

2. ###### 数组语法

   可将多个样式对象应用到一个元素上

   ```html
   <div class="box" :style="[styleObjectA, styleObjectB]">好好学习，天天向上</div>
   var vm2= new Vue({
       el:‘.box‘,
       data:{
           styleObjectA:{
               fontSize:‘36px‘,
               color:‘blue‘
           },
           styleObjectB:{
               textDecoration:‘underline‘
           }
       }
   })
   ```

#### **参考**：

- [Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html)
- [组件 - Props](https://cn.vuejs.org/v2/guide/components.html#通过-Prop-向子组件传递数据)
- [组件 - `.sync` 修饰符](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符)

### [v-model](https://cn.vuejs.org/v2/api/#v-model)

#### 使用说明

实现这些标签数据的双向绑定。

#### 限制

- `<input>`
- `<select>`
- `<textarea>`
- `components`

#### 本质

 v-model本质上是一个语法糖。

```js
<input v-model="test">
//等同于
<input :value="test" @input="test = $event.target.value">
```

#### 修饰符

##### .lazy

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了输入法组合文字时)。你可以添加 `lazy` 修饰符，从而转变为使用 on`change` 事件进行同步，当在输入框输入数据时，数据并不会立即改变，当光标离开输入框以后，数据才会实现同步改变。

##### .number

如果想自动将用户的输入值转为数值类型，把type定义为number类型，给 `v-model` 添加 `number` 修饰符，当用户输入数值类型的数据时，v-model.number会自动把输入的数据转换为数值类型，注意如果用户输入特殊字母e，number属性不能识别

##### .trim

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符，在输入框起始时候多添加几个空格，当光标离开之后，trim属性会自动过滤首尾空格。

#### 参考

- [表单控件绑定](https://cn.vuejs.org/v2/guide/forms.html)
- [组件 - 在输入组件上使用自定义事件](https://cn.vuejs.org/v2/guide/components-custom-events.html#将原生事件绑定到组件)

### [v-text](https://cn.vuejs.org/v2/api/#v-text)

#### 使用说明

将数据对象的值显示在网页上。该指令只是单向的绑定。`v-text`可以简写为`{{}}`,并且支持逻辑运算。

插值表达式和v-text指令被直接解析为了字符串元素

#### 示例

```html
<span v-text="msg"></span>
<!-- 和下面的一样 -->
<span>{{msg}}</span>
```

#### 参考：

[数据绑定语法 - 插值](https://cn.vuejs.org/v2/guide/syntax.html#插值)

### [v-html](https://cn.vuejs.org/v2/api/#v-html)

#### 使用说明

更新元素的 `innerHTML`。即可以接收`html`，并解析html后进行显示。

#### 示例

```html
<div v-html="html"></div>
```

#### 参考

[数据绑定语法 - 插值](https://cn.vuejs.org/v2/guide/syntax.html#纯-HTML)

### [v-pre](https://cn.vuejs.org/v2/api/#v-pre)

#### 用法

跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

#### 示例

```html
<span v-pre>{{ this will not be compiled }}</span>
```

### [v-cloak](https://cn.vuejs.org/v2/api/#v-cloak)

#### 用法

这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

#### 示例

```css
[v-cloak] {
  display: none;
}
```

```html
<div v-cloak>
  {{ message }}
</div>
```

### [v-once](https://cn.vuejs.org/v2/api/#v-once)

#### 用法

只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

#### 示例

```html
<!-- 单个元素 -->
<span v-once>This will never change: {{msg}}</span>
<!-- 有子元素 -->
<div v-once>
  <h1>comment</h1>
  <p>{{msg}}</p>
</div>
<!-- 组件 -->
<my-component v-once :comment="msg"></my-component>
<!-- `v-for` 指令-->
<ul>
  <li v-for="i in list" v-once>{{i}}</li>
</ul>
```

#### 参考

- [数据绑定语法- 插值](https://cn.vuejs.org/v2/guide/syntax.html#插值)
- [组件 - 对低开销的静态组件使用 `v-once`](https://cn.vuejs.org/v2/guide/components-edge-cases.html#通过-v-once-创建低开销的静态组件)

### [v-if](https://cn.vuejs.org/v2/api/#v-if)

#### 用法

根据表达式的值的 [truthiness](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy) （真值）来有条件地渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建。如果元素是 `<template>`，将提出它的内容作为条件块。当条件变化时该指令触发过渡效果。

#### 注意

当和 `v-if` 一起使用时，`v-for` 的优先级比 `v-if` 更高。详见[列表渲染教程](https://cn.vuejs.org/v2/guide/list.html#v-for-with-v-if)

#### 参考

[条件渲染 - v-if](https://cn.vuejs.org/v2/guide/conditional.html)

### [v-else](https://cn.vuejs.org/v2/api/#v-else)

#### 限制

前一兄弟元素必须有 `v-if` 或 `v-else-if`。

#### 用法

为 `v-if` 或者 `v-else-if` 添加“else 块”。

#### 示例

```html
<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
```

#### 参考

[条件渲染 - v-else](https://cn.vuejs.org/v2/guide/conditional.html#v-else)

### [v-else-if](https://cn.vuejs.org/v2/api/#v-else-if)

#### 限制

前一兄弟元素必须有 `v-if` 或 `v-else-if`。

#### 用法

表示 `v-if` 的“else if 块”。可以链式调用。

```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

#### 参考

[条件渲染 - v-else-if](https://cn.vuejs.org/v2/guide/conditional.html#v-else-if)

### [v-show](https://cn.vuejs.org/v2/api/#v-show)

#### 用法

根据表达式之真假值，切换元素的 `display` CSS property。

当条件变化时该指令触发过渡效果。

#### 参考

[条件渲染 - v-show](https://cn.vuejs.org/v2/guide/conditional.html#v-show)

### [v-for](https://cn.vuejs.org/v2/api/#v-for)

#### 用法

基于源数据多次渲染元素或模板块。此指令之值，必须使用特定语法 `alias in expression`，为当前遍历的元素提供别名：

```html
<div v-for="item in items">
  {{ item.text }}
</div>
```

另外也可以为数组索引指定别名 (或者用于对象的键)：

```html
<div v-for="(item, index) in items"></div>
<div v-for="(val, key) in object"></div>
<div v-for="(val, name, index) in object"></div>
```

`v-for` 的默认行为会尝试原地修改元素而不是移动它们。要强制其重新排序元素，你需要用特殊 attribute `key` 来提供一个排序提示：

```html
<div v-for="item in items" :key="item.id">
  {{ item.text }}
</div>
```

从 2.6 起，`v-for` 也可以在实现了[可迭代协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols#可迭代协议)的值上使用，包括原生的 `Map` 和 `Set`。不过应该注意的是 Vue 2.x 目前并不支持可响应的 `Map` 和 `Set` 值，所以无法自动探测变更。

当和 `v-if` 一起使用时，`v-for` 的优先级比 `v-if` 更高。详见[列表渲染教程](https://cn.vuejs.org/v2/guide/list.html#v-for-with-v-if)

`v-for` 的详细用法可以通过以下链接查看教程详细说明。

#### 参考

- [列表渲染](https://cn.vuejs.org/v2/guide/list.html)
- [key](https://cn.vuejs.org/v2/guide/list.html#key)

### [v-slot](https://cn.vuejs.org/v2/api/#v-slot)

#### 缩写

`#`

#### 预期

可放置在函数参数位置的 JavaScript 表达式 (在[支持的环境下](https://cn.vuejs.org/v2/guide/components-slots.html#解构插槽-Props)可使用解构)。可选，即只需要在为插槽传入 prop 的时候使用。

#### 参数

插槽名 (可选，默认值是 `default`)

#### 限制

- `<template>`
- [组件](https://cn.vuejs.org/v2/guide/components-slots.html#独占默认插槽的缩写语法) (对于一个单独的带 prop 的默认插槽)

#### 用法

提供具名插槽或需要接收 prop 的插槽。

#### 示例

```html
<!-- 具名插槽 -->
<base-layout>
  <template v-slot:header>
    Header content
  </template>

  Default slot content

  <template v-slot:footer>
    Footer content
  </template>
</base-layout>

<!-- 接收 prop 的具名插槽 -->
<infinite-scroll>
  <template v-slot:item="slotProps">
    <div class="item">
      {{ slotProps.item.text }}
    </div>
  </template>
</infinite-scroll>

<!-- 接收 prop 的默认插槽，使用了解构 -->
<mouse-position v-slot="{ x, y }">
  Mouse position: {{ x }}, {{ y }}
</mouse-position>
```

#### 参考

- [组件 - 插槽](https://cn.vuejs.org/v2/guide/components-slots.html)
- [RFC-0001](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0001-new-slot-syntax.md)

## 组件

### 组件注册

```vue + js + html
Vue.component('组件名称'),{
	data:组件数据,
	template:组件模板内容
})
```

#### 示例

```html
<div id="app">
    <button-counter></button-counter>
</div>
<script>
    <!--注册一个名为buttom-counter的组件-->
    Vue.component('button-counter',{
        data:function(){
            return{
                count:0
            }
        },
        template:'<button> @click="count++">点击了{{count}}次。</button>'
    })
    new Vue({
        el:'#app'
    })
</script>
```

#### 注意事项

- 组件参数的data值必须是函数同时这个函数要求返回一个对象 

- 组件模板的内容必须是单个根元素

- 组件模板的内容可以是模板字符串

- 如果使用驼峰式命名组件，那么在使用组件的时候，只能在字符串模板中用驼峰的方式使用组件，但是在普通的标签模板中，必须使用短横线的方式使用组件

  ```html
    <div id="app">
       <!-- 
  		4.组件可以重复使用多次 
  	      因为data中返回的是一个对象所以每个组件中的数据是私有的
  		  即每个实例可以维护一份被返回对象的独立的拷贝   
  	--> 
      <button-counter></button-counter>
      <button-counter></button-counter>
      <button-counter></button-counter>
        <!-- 8.必须使用短横线的方式使用组件 -->
       <hello-world></hello-world>
    </div>
  
  <script type="text/javascript">
  	//5.如果使用驼峰式命名组件，那么在使用组件的时候，只能在字符串模板中用驼峰的方式使用组件，但是在普通的标签模板中，必须使用短横线的方式使用组件
       Vue.component('HelloWorld', {
        data: function(){
          return {
            msg: 'HelloWorld'
          }
        },
        template: '<div>{{msg}}</div>'
      });
      
      Vue.component('button-counter', {
        // 1.组件参数的data值必须是函数 
        //   同时这个函数要求返回一个对象  
        data: function(){
          return {
            count: 0
          }
        },
        //  2.组件模板必须是单个根元素
        //  3.组件模板的内容可以是模板字符串  
        template: `
          <div>
            <button @click="handle">点击了{{count}}次</button>
            <button>测试123</button>
  			#6.在字符串模板中可以使用驼峰的方式使用组件	
  		   <HelloWorld></HelloWorld>
          </div>
        `,
        methods: {
          handle: function(){
            this.count += 2;
          }
        }
      })
      var vm = new Vue({
        el: '#app',
        data: {
          
        }
      });
    </script>
  ```

#### 组件命名方式

- 短横线方式

  ```html
  Vue.compoent('my-component,/>',{/*.../*})
  ```

- 驼峰方式

  ```vue
  Vue.compoent('MyComponent,/>',{/*.../*})
  ```

#### 局部组件注册

- 只能在当前注册它的vue实例中使用

```html
<div id="app">
    <my-component></my-component>
</div>
<script>
// 定义组件的模板
var ComponentA={template:'<div>A custom component!</div>'}
new Vue({
	el:'#app'
    //局部注册组件  
	components:{
    // <my-component> 将只在父模板可用  一定要在实例上注册了才能在html文件中使用
		'my-component':ComponentA,
	}
})
 </script>
```

### Vue组件之间传值

#### 父组件向子组件传值 

- 父组件发送的形式是以属性的形式绑定值到子组件身上。

- 然后子组件用属性props接收

- 在props中使用驼峰形式，模板中需要使用短横线的形式，字符串形式的模板中没有这个限制

  ```html
    <div id="app">
      <div>{{pmsg}}</div>
       <!--1.menu-item  在 APP中嵌套着 故 menu-item 为  子组件      -->
       <!-- 给子组件传入一个静态的值 -->
      <menu-item title='来自父组件的值'></menu-item>
      <!-- 2.需要动态的数据的时候 需要属性绑定的形式设置 此时 ptitle  来自父组件data 中的数据 . 
  		  传的值可以是数字、对象、数组等等-->
      <menu-item :title='ptitle' content='hello'></menu-item>
    </div>
  
    <script type="text/javascript">
      Vue.component('menu-item', {
        // 3.子组件用属性props接收父组件传递过来的数据  
        props: ['title', 'content'],
        data: function() {
          return {
            msg: '子组件本身的数据'
          }
        },
        template: '<div>{{msg + "----" + title + "-----" + content}}</div>'
      });
      var vm = new Vue({
        el: '#app',
        data: {
          pmsg: '父组件中内容',
          ptitle: '动态绑定属性'
        }
      });
    </script>
  ```

#### 子组件向父组件传值

- 子组件用`$emit()`触发事件

- `$emit()`  第一个参数为 自定义的事件名称     第二个参数为需要传递的数据

- 父组件用`v-on` 监听子组件的事件

  ```html
   <div id="app">
      <div :style='{fontSize: fontSize + "px"}'>{{pmsg}}</div>
      <!--2.父组件用v-on 监听子组件的事件 这里 enlarge-text  是从 $emit 中的第一个参数对应   handle 为对应的事件处理函数-->	
      <menu-item :parr='parr' @enlarge-text='handle($event)'></menu-item>
    </div>
    <script type="text/javascript" src="js/vue.js"></script>
    <script type="text/javascript">
      /*子组件向父组件传值-携带参数*/
      Vue.component('menu-item', {
        props: ['parr'],
        template: `
          <div>
            <ul>
              <li :key='index' v-for='(item,index) in parr'>{{item}}</li>
            </ul>
  			### 1.子组件用$emit()触发事件
  			### 第一个参数为 自定义的事件名称   第二个参数为需要传递的数据  
            <button @click='$emit("enlarge-text", 5)'>扩大父组件中字体大小</button>
            <button @click='$emit("enlarge-text", 10)'>扩大父组件中字体大小</button>
          </div>
        `
      });
      var vm = new Vue({
        el: '#app',
        data: {
          pmsg: '父组件中内容',
          parr: ['apple','orange','banana'],
          fontSize: 10
        },
        methods: {
          handle: function(val){
            // 扩大字体大小
            this.fontSize += val;
          }
        }
      });
    </script>
  
  ```

#### 兄弟之间的传递

- 兄弟之间传递数据需要借助于事件中心，通过事件中心传递数据   

  - 提供事件中心    var hub = new Vue()

- 传递数据方，通过一个事件触发hub.$emit(方法名，传递的数据)

- 接收数据方，通过mounted(){} 钩子中  触发hub.$on()方法名

- 销毁事件 通过hub.$off()方法名销毁之后无法进行传递数据

  ```html
   <div id="app">
      <div>父组件</div>
      <div>
        <button @click='handle'>销毁事件</button>
      </div>
      <test-tom></test-tom>
      <test-jerry></test-jerry>
   </div>
   <script type="text/javascript" src="js/vue.js"></script>
   <script type="text/javascript">
      /*兄弟组件之间数据传递*/
      //1.提供事件中心
      var hub = new Vue();
      Vue.component('test-tom', {
        data: function(){
          return {
            num: 0
          }
        },
        template: `
          <div>
            <div>TOM:{{num}}</div>
            <div>
              <button @click='handle'>点击</button>
            </div>
          </div>
        `,
        methods: {
          handle: function(){
            //2.传递数据方，通过一个事件触发hub.$emit(方法名，传递的数据)   触发兄弟组件的事件
            hub.$emit('jerry-event',2);
          }
        },
        mounted: function() {
         // 3.接收数据方，通过mounted(){} 钩子中  触发hub.$on(方法名
          hub.$on('tom-event', (val) => {
            this.num += val;
          });
        }
      });
      Vue.component('test-jerry', {
        data: function(){
          return {
            num: 0
          }
        },
        template: `
          <div>
            <div>JERRY:{{num}}</div>
            <div>
              <button @click='handle'>点击</button>
            </div>
          </div>
        `,
        methods: {
          handle: function(){
            //2、传递数据方，通过一个事件触发hub.$emit(方法名，传递的数据)   触发兄弟组件的事件
            hub.$emit('tom-event', 1);
          }
        },
        mounted: function() {
          // 3、接收数据方，通过mounted(){} 钩子中  触发hub.$on()方法名
          hub.$on('jerry-event', (val) => {
            this.num += val;
          });
        }
      });
      var vm = new Vue({
        el: '#app',
        data: {
          
        },
        methods: {
          handle: function(){
            //4、销毁事件 通过hub.$off()方法名销毁之后无法进行传递数据  
            hub.$off('tom-event');
            hub.$off('jerry-event');
          }
        }
      });
    </script>
  ```

### 组件插槽

- 组件的最大特性就是复用性，而用好插槽能大大提高组件的可复用能力

#### 匿名插槽

```html
  <div id="app">
    <!-- 这里的所有组件标签中嵌套的内容会替换掉slot  如果不传值 则使用 slot 中的默认值  -->  
    <alert-box>有bug发生</alert-box>
    <alert-box>有一个警告</alert-box>
    <alert-box></alert-box>
  </div>

  <script type="text/javascript">
    /*组件插槽：父组件向子组件传递内容*/
    Vue.component('alert-box', {
      template: `
        <div>
          <strong>ERROR:</strong>
		# 当组件渲染的时候，这个 <slot> 元素将会被替换为“组件标签中嵌套的内容”。
		# 插槽内可以包含任何模板代码，包括 HTML
          <slot>默认内容</slot>
        </div>
      `
    });
    var vm = new Vue({
      el: '#app',
      data: {
        
      }
    });
  </script>
</body>
</html>

```

#### 具名插槽

- 具有名字的插槽 
- 使用 <slot> 中的 "name" 属性绑定元素

```html
 <div id="app">
    <base-layout>
       <!-- 2、 通过slot属性来指定, 这个slot的值必须和下面slot组件得name值对应上
				如果没有匹配到 则放到匿名的插槽中   --> 
      <p slot='header'>标题信息</p>
      <p>主要内容1</p>
      <p>主要内容2</p>
      <p slot='footer'>底部信息信息</p>
    </base-layout>

    <base-layout>
      <!-- 注意点：template临时的包裹标签最终不会渲染到页面上  -->  
      <template slot='header'>
        <p>标题信息1</p>
        <p>标题信息2</p>
      </template>
      <p>主要内容1</p>
      <p>主要内容2</p>
      <template slot='footer'>
        <p>底部信息信息1</p>
        <p>底部信息信息2</p>
      </template>
    </base-layout>
  </div>
  <script type="text/javascript" src="js/vue.js"></script>
  <script type="text/javascript">
    /*
      具名插槽
    */
    Vue.component('base-layout', {
      template: `
        <div>
          <header>
			###	1.使用 <slot> 中的 "name" 属性绑定元素 指定当前插槽的名字
            <slot name='header'></slot>
          </header>
          <main>
            <slot></slot>
          </main>
          <footer>
			###  注意点： 
			###  具名插槽的渲染顺序，完全取决于模板，而不是取决于父组件中元素的顺序
            <slot name='footer'></slot>
          </footer>
        </div>
      `
    });
    var vm = new Vue({
      el: '#app',
      data: {
        
      }
    });
  </script>
</body>
</html>

```

#### 作用域插槽

- 父组件对子组件加工处理
- 既可以复用子组件的slot，又可以使slot内容不一致

```html
  <div id="app">
    <!-- 
		1、当我们希望li 的样式由外部使用组件的地方定义，因为可能有多种地方要使用该组件，
		但样式希望不一样 这个时候我们需要使用作用域插槽 
		
	-->  
    <fruit-list :list='list'>
       <!-- 2、 父组件中使用了<template>元素,而且包含scope="slotProps",
			slotProps在这里只是临时变量   
		---> 	
      <template slot-scope='slotProps'>
        <strong v-if='slotProps.info.id==3' class="current">
            {{slotProps.info.name}}		         
         </strong>
        <span v-else>{{slotProps.info.name}}</span>
      </template>
    </fruit-list>
  </div>
  <script type="text/javascript" src="js/vue.js"></script>
  <script type="text/javascript">
    /*
      作用域插槽
    */
    Vue.component('fruit-list', {
      props: ['list'],
      template: `
        <div>
          <li :key='item.id' v-for='item in list'>
			###  3、 在子组件模板中,<slot>元素上有一个类似props传递数据给组件的写法msg="xxx",
			###   插槽可以提供一个默认内容，如果如果父组件没有为这个插槽提供了内容，会显示默认的内容。
					如果父组件为这个插槽提供了内容，则默认的内容会被替换掉
            <slot :info='item'>{{item.name}}</slot>
          </li>
        </div>
      `
    });
    var vm = new Vue({
      el: '#app',
      data: {
        list: [{
          id: 1,
          name: 'apple'
        },{
          id: 2,
          name: 'orange'
        },{
          id: 3,
          name: 'banana'
        }]
      }
    });
  </script>
</body>
</html>
```

## vue接口请求与调用

### 接口调用方式

- 原生ajax
- 基于jQuery的ajax
- fetch
- axios

### 异步

- JavaScript的执行环境是「单线程」
- 所谓单线程，是指JS引擎中负责解释和执行JavaScript代码的线程只有一个，也就是一次只能完成一项任务，这个任务执行完后才能执行下一个，它会「阻塞」其他任务。这个任务可称为主线程
- 异步模式可以一起执行**多个任务**
- JS中常见的异步调用
  - 定时任何
  - ajax
  - 事件函数

### promise

- 主要解决异步深层嵌套的问题
- promise 提供了简洁的API  使得异步操作更加容易

```html
   <script type="text/javascript">
    /*
     1. Promise基本使用
           我们使用new来构建一个Promise  Promise的构造函数接收一个参数，是函数，并且传入两个参数： resolve，reject， 分别表示异步操作执行成功后的回调函数和异步操作执行失败后的回调函数
    */


    var p = new Promise(function(resolve, reject){
      //2. 这里用于实现异步任务  setTimeout
      setTimeout(function(){
        var flag = false;
        if(flag) {
          //3. 正常情况
          resolve('hello');
        }else{
          //4. 异常情况
          reject('出错了');
        }
      }, 100);
    });
    //  5.Promise实例生成以后，可以用then方法指定resolved状态和reject状态的回调函数 
    //  在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了  
    p.then(function(data){
      console.log(data)
    },function(info){
      console.log(info)
    });
  </script>
```

### 基于Promise发送Ajax请求

```html
  <script type="text/javascript">
    /*
      基于Promise发送Ajax请求
    */
    function queryData(url) {
     #   1.1 创建一个Promise实例
      var p = new Promise(function(resolve, reject){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
          if(xhr.readyState != 4) return;
          if(xhr.readyState == 4 && xhr.status == 200) {
            # 1.2 处理正常的情况
            resolve(xhr.responseText);
          }else{
            # 1.3 处理异常情况
            reject('服务器错误');
          }
        };
        xhr.open('get', url);
        xhr.send(null);
      });
      return p;
    }
	# 注意：  这里需要开启一个服务 
    # 在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了
    queryData('http://localhost:3000/data')
      .then(function(data){
        console.log(data)
        #  1.4 想要继续链式编程下去 需要 return  
        return queryData('http://localhost:3000/data1');
      })
      .then(function(data){
        console.log(data);
        return queryData('http://localhost:3000/data2');
      })
      .then(function(data){
        console.log(data)
      });
  </script>
```

### Promise  基本API

#### 实例方法

##### .then()

- 得到异步任务正确的结果

##### .catch()

- 获取异常信息

##### .finally()

- 成功与否都会执行（不是正式标准） 

```html
  <script type="text/javascript">
    /*
      Promise常用API-实例方法
    */
    // console.dir(Promise);
    function foo() {
      return new Promise(function(resolve, reject){
        setTimeout(function(){
          // resolve(123);
          reject('error');
        }, 100);
      })
    }
    // foo()
    //   .then(function(data){
    //     console.log(data)
    //   })
    //   .catch(function(data){
    //     console.log(data)
    //   })
    //   .finally(function(){
    //     console.log('finished')
    //   });

    // --------------------------
    // 两种写法是等效的
    foo()
      .then(function(data){
        # 得到异步任务正确的结果
        console.log(data)
      },function(data){
        # 获取异常信息
        console.log(data)
      })
      # 成功与否都会执行（不是正式标准） 
      .finally(function(){
        console.log('finished')
      });
  </script>
```

#### 静态方法

#####  .all()

- `Promise.all`方法接受一个数组作参数，数组中的对象（p1、p2、p3）均为promise实例（如果不是一个promise，该项会被用`Promise.resolve`转换为一个promise)。它的状态由这三个promise实例决定

#####  .race()

- `Promise.race`方法同样接受一个数组作参数。当p1, p2, p3中有一个实例的状态发生改变（变为`fulfilled`或`rejected`），p的状态就跟着改变。并把第一个改变状态的promise的返回值，传给p的回调函数

```html
  <script type="text/javascript">
    /*
      Promise常用API-对象方法
    */
    // console.dir(Promise)
    function queryData(url) {
      return new Promise(function(resolve, reject){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
          if(xhr.readyState != 4) return;
          if(xhr.readyState == 4 && xhr.status == 200) {
            // 处理正常的情况
            resolve(xhr.responseText);
          }else{
            // 处理异常情况
            reject('服务器错误');
          }
        };
        xhr.open('get', url);
        xhr.send(null);
      });
    }

    var p1 = queryData('http://localhost:3000/a1');
    var p2 = queryData('http://localhost:3000/a2');
    var p3 = queryData('http://localhost:3000/a3');
     Promise.all([p1,p2,p3]).then(function(result){
       //   all 中的参数  [p1,p2,p3]   和 返回的结果一 一对应["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
       console.log(result) //["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
     })
    Promise.race([p1,p2,p3]).then(function(result){
      // 由于p1执行较快，Promise的then()将获得结果'P1'。p2,p3仍在继续执行，但执行结果将被丢弃。
      console.log(result) // "HELLO TOM"
    })
  </script>
```

### fetch

- Fetch API是新的ajax解决方案 Fetch会返回Promise
- **fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象**。
- fetch(url, options).then(）

```html
  <script type="text/javascript">
    /*
      Fetch API 基本用法
      	fetch(url).then()
     	第一个参数请求的路径   Fetch会返回Promise   所以我们可以使用then 拿到请求成功的结果 
    */
    fetch('http://localhost:3000/fdata').then(function(data){
      // text()方法属于fetchAPI的一部分，它返回一个Promise实例对象，用于获取后台返回的数据
      return data.text();
    }).then(function(data){
      //   在这个then里面我们能拿到最终的数据  
      console.log(data);
    })
  </script>
```

#### fetch API  中的 HTTP  请求

- fetch(url, options).then(）
- HTTP协议，它给我们提供了很多的方法，如POST，GET，DELETE，UPDATE，PATCH和PUT
  - 默认的是 GET 请求
  - 需要在 options 对象中 指定对应的 method       method:请求使用的方法 
  - post 和 普通 请求的时候 需要在options 中 设置  请求头 headers   和  body

```html
   <script type="text/javascript">
        /*
              Fetch API 调用接口传递参数
        */
       #1.1 GET参数传递 - 传统URL  通过url  ？ 的形式传参 
        fetch('http://localhost:3000/books?id=123', {
            	# get 请求可以省略不写 默认的是GET 
                method: 'get'
            })
            .then(function(data) {
            	# 它返回一个Promise实例对象，用于获取后台返回的数据
                return data.text();
            }).then(function(data) {
            	# 在这个then里面我们能拿到最终的数据  
                console.log(data)
            });

      #1.2  GET参数传递  restful形式的URL  通过/ 的形式传递参数  即  id = 456 和id后台的配置有关   
        fetch('http://localhost:3000/books/456', {
            	# get 请求可以省略不写 默认的是GET 
                method: 'get'
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       #2.1  DELETE请求方式参数传递      删除id  是  id=789
        fetch('http://localhost:3000/books/789', {
                method: 'delete'
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       #3 POST请求传参
        fetch('http://localhost:3000/books', {
                method: 'post',
            	# 3.1  传递数据 
                body: 'uname=lisi&pwd=123',
            	#  3.2  设置请求头 
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       # POST请求传参
        fetch('http://localhost:3000/books', {
                method: 'post',
                body: JSON.stringify({
                    uname: '张三',
                    pwd: '456'
                }),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

        # PUT请求传参     修改id 是 123 的 
        fetch('http://localhost:3000/books/123', {
                method: 'put',
                body: JSON.stringify({
                    uname: '张三',
                    pwd: '789'
                }),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });
    </script>
```

#### fetchAPI 中 响应格式

- 用fetch来获取数据，如果响应正常返回，我们首先看到的是一个response对象，其中包括返回的一堆原始字节，这些字节需要在收到后，需要我们通过调用方法将其转换为相应格式的数据，比如`JSON`，`BLOB`或者`TEXT`等等

```js
    /*
      Fetch响应结果的数据格式
    */
    fetch('http://localhost:3000/json').then(function(data){
      // return data.json();   //  将获取到的数据使用 json 转换对象
      return data.text(); //  //  将获取到的数据 转换成字符串 
    }).then(function(data){
      // console.log(data.uname)
      // console.log(typeof data)
      var obj = JSON.parse(data);
      console.log(obj.uname,obj.age,obj.gender)
    })
```

### axios

- 基于promise用于浏览器和node.js的http客户端
- 支持浏览器和node.js
- 支持promise
- 能拦截请求和响应
- 自动转换JSON数据
- 能转换请求和响应数据

#### axios基础用法

- get和 delete请求传递参数
  - 通过传统的url  以 ? 的形式传递参数
  - restful 形式传递参数 
  - 通过params  形式传递参数 
- post  和 put  请求传递参数
  - 通过选项传递参数
  - 通过 URLSearchParams  传递参数 

```json
    # 1. 发送get 请求 
	axios.get('http://localhost:3000/adata').then(function(ret){ 
      #  拿到 ret 是一个对象  所有的对象都存在 ret 的data 属性里面
      // 注意data属性是固定的用法，用于获取后台的实际数据
      // console.log(ret.data)
      console.log(ret)
    })
	# 2.  get 请求传递参数
    # 2.1  通过传统的url  以 ? 的形式传递参数
	axios.get('http://localhost:3000/axios?id=123').then(function(ret){
      console.log(ret.data)
    })
    # 2.2  restful 形式传递参数 
    axios.get('http://localhost:3000/axios/123').then(function(ret){
      console.log(ret.data)
    })
	# 2.3  通过params  形式传递参数 
    axios.get('http://localhost:3000/axios', {
      params: {
        id: 789
      }
    }).then(function(ret){
      console.log(ret.data)
    })
	#3 axios delete 请求传参     传参的形式和 get 请求一样
    axios.delete('http://localhost:3000/axios', {
      params: {
        id: 111
      }
    }).then(function(ret){
      console.log(ret.data)
    })

	# 4  axios 的 post 请求
    # 4.1  通过选项传递参数
    axios.post('http://localhost:3000/axios', {
      uname: 'lisi',
      pwd: 123
    }).then(function(ret){
      console.log(ret.data)
    })
	# 4.2  通过 URLSearchParams  传递参数 
    var params = new URLSearchParams();
    params.append('uname', 'zhangsan');
    params.append('pwd', '111');
    axios.post('http://localhost:3000/axios', params).then(function(ret){
      console.log(ret.data)
    })

 	#5  axios put 请求传参   和 post 请求一样 
    axios.put('http://localhost:3000/axios/123', {
      uname: 'lisi',
      pwd: 123
    }).then(function(ret){
      console.log(ret.data)
    })

```

#### axios 全局配置

```js
#  配置公共的请求头 
axios.defaults.baseURL = 'https://api.example.com';
#  配置 超时时间
axios.defaults.timeout = 2500;
#  配置公共的请求头
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
# 配置公共的 post 的 Content-Type
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

#### axios 拦截器

- 请求拦截器
  - 请求拦截器的作用是在请求发送前进行一些操作
    - 例如在每个请求体里加上token，统一做了处理如果以后要改也非常容易
- 响应拦截器
  - 响应拦截器的作用是在接收到响应后进行一些操作
    - 例如在服务器返回登录状态失效，需要重新登录的时候，跳转到登录页

```js
	# 1. 请求拦截器 
	axios.interceptors.request.use(function(config) {
      console.log(config.url)
      # 1.1  任何请求都会经过这一步   在发送请求之前做些什么   
      config.headers.mytoken = 'nihao';
      # 1.2  这里一定要return   否则配置不成功  
      return config;
    }, function(err){
       #1.3 对请求错误做点什么    
      console.log(err)
    })
	#2. 响应拦截器 
    axios.interceptors.response.use(function(res) {
      #2.1  在接收响应做些什么  
      var data = res.data;
      return data;
    }, function(err){
      #2.2 对响应错误做点什么  
      console.log(err)
    })
```

### async  和 await

- async作为一个关键字放到函数前面
  - 任何一个`async`函数都会隐式返回一个`promise`
- `await`关键字只能在使用`async`定义的函数中使用
  - ​    await后面可以直接跟一个 Promise实例对象
  - ​     await函数不能单独使用
- **async/await 让异步代码看起来、表现起来更像同步代码**

```js
 	# 1.  async 基础用法
    # 1.1 async作为一个关键字放到函数前面
	async function queryData() {
      # 1.2 await关键字只能在使用async定义的函数中使用      await后面可以直接跟一个 Promise实例对象
      var ret = await new Promise(function(resolve, reject){
        setTimeout(function(){
          resolve('nihao')
        },1000);
      })
      // console.log(ret.data)
      return ret;
    }
	# 1.3 任何一个async函数都会隐式返回一个promise   我们可以使用then 进行链式编程
    queryData().then(function(data){
      console.log(data)
    })

	#2.  async    函数处理多个异步函数
    axios.defaults.baseURL = 'http://localhost:3000';

    async function queryData() {
      # 2.1  添加await之后 当前的await 返回结果之后才会执行后面的代码   
      
      var info = await axios.get('async1');
      #2.2  让异步代码看起来、表现起来更像同步代码
      var ret = await axios.get('async2?info=' + info.data);
      return ret.data;
    }

    queryData().then(function(data){
      console.log(data)
    })
```

# Vue踩坑

## v-if 与 v-for 一起使用

当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级，这意味着 `v-if` 将分别重复运行于每个 `v-for` 循环中，即每次`v-for`的循环中都会执行`v-if`的判断，因此会影响性能。所以，不推荐v-if和v-for同时使用

## 代替的方法

### 方法一、不用v-if或者分开使用

### 方法二、使用computed进行预过滤

## 参考：[v-if和v-for一起使用的几个方法](https://www.cnblogs.com/mmzuo-798/p/11943448.html)



# Vue实际开发案例

## 实现列表滚动

### 要求

在页面实现列表的循环滚动，当鼠标移入后停止滚动，点击相关条目可以实现跳转。

### 实现思路

- 使用`jQuery`的`scrollTop()`方法实现列表的滚动
- 使用`setInterval`来对列表的滚动速度进行控制
- 当鼠标移入后，触发相应的事件执行`clearInterval`，从而停止滚动
- 当鼠标移出后，触发相应的事件执行`setInterval`，继续滚动

### 具体代码

```vue
<template>

    <div style="position: relative;">
      <div ref="message" class="messages">
        <div ref="infobord1" class="content-issue">
            <p v-if="showFlag" @click="clickItem(index)"   v-for="(item,index) in messages">
            <span class="gdTitle"> {{item.gdtitle}}</span>
            <span class="icon"> <i v-bind:class="getStatus(item.gdstatus)"></i> </span>
            <span v-bind:class="getInfoClass(item.gdstatus)">{{item.gdstatusname}}</span>
          </p>
        </div>
      </div>
    </div>

</template>
<script>
export default {
    data () {
        return {
            showFlag: true,
            //构造数据
            messages:[
                {
                  gdid:"1122",
                  gdstatus:"DOING",
                  gdstatusname:"待审批",
                  gdtitle:"陆传荣我的工单申请"
                },
                {
                  gdid:"1122",
                  gdstatus:"CLOSE",
                  gdstatusname:"已通过",
                  gdtitle:"我的工单申请"
                },
                {
                  gdid:"1122",
                  gdstatus:"REJECT",
                  gdstatusname:"已驳回",
                  gdtitle:"我的工单申请1"
                },
                {
                  gdid:"1122",
                  gdstatus:"DOING",
                  gdstatusname:"待审批",
                  gdtitle:"陆传荣我的工单申请"
                },
                {
                  gdid:"1122",
                  gdstatus:"CLOSE",
                  gdstatusname:"已通过",
                  gdtitle:"我的工单申请"
                },
                {
                  gdid:"1122",
                  gdstatus:"REJECT",
                  gdstatusname:"已驳回",
                  gdtitle:"我的工单申请1"
                }
            ]
        };
    },
    methods: {
        //点击事件
        clickItem(i) {
          console.log(this.messages[i].gdtitle);
        },
        getInfoClass:function(gdstatus) {
          if (gdstatus === "DOING") {
            return "doing";
          } else if (gdstatus === "CLOSE") {
            return "pass";
          } else if (gdstatus === "REJECT") {
            return "reject";
          }
        },
        getStatus: function(gdstatus) {
          if (gdstatus === "DOING") {
            return "el-icon-warning";
          } else if (gdstatus === "CLOSE") {
            return "el-icon-success";
          } else if (gdstatus === "REJECT") {
            return "el-icon-error";
          }
        },
        rollText: function() {
          var speed = 50;
          var that = this;
          function Marquee() {
            // console.log(that.message.scrollHeight)
              if (that.message.scrollHeight -that.message.scrollTop  == that.message.clientHeight) {
                that.message.scrollTop = 0;
            } else {
              that.message.scrollTop++;
            }
          }
          var MyMar = setInterval(Marquee, speed); //设置定时器
          //鼠标移上时清除定时器达到滚动停止的目的
          this.message.addEventListener("mouseover", function() {
            clearInterval(MyMar);
          });
          //鼠标移开时重设定时器
          this.message.addEventListener("mouseout", function() {
            MyMar = setInterval(Marquee, speed);
          });
        }
    },
    mounted() {
        this.message = this.$refs.message;
   	 	this.infobord1 = this.$refs.infobord1;
    	this.rollText();
    } 
}
</script>
<style scoped>
.gdTitle{
  width: 186px;
  text-align: left;
}
.content-issue {
  width: 100%;
  margin-bottom: 82px;
  margin-top: 82px;
}
.content-issue p {
  color: white;
  width: 100%;
  font-size: 14px;
  cursor: pointer;
  display: flex;
  justify-content: flex-start;
  background: white;
  position: relative;
  white-space: nowrap;
  height: 20px;
  line-height: 20px;
  margin-block-start: 10px;
  margin-block-end: 10px;
}
.icon {
  /*color: #F04134;*/
  font-size:14px;
  /*width:15px;*/
  height: 20px;
  /*width: 95%;*/
}
/*鼠标选中后的样式*/
.content-issue p:hover {
  background: #6FB7F9;
}
.content-issue span {
  color: #354052;
}
.content-issue i.el-icon-warning {
  color: #ABCEF2;
}
.content-issue i.el-icon-success {
  color: #2CBF4B;
}
.content-issue i.el-icon-error {
  color: #F04134;
}
.content-issue span.doing {
  color: #ABCEF2;
  margin-left: 8px;
}
.content-issue span.pass {
  color: #2CBF4B;
  margin-left: 8px;
}
.content-issue span.reject {
  color: #F04134;
  margin-left: 8px;
}
.messages {
  position: relative;
  width: 254px;
  height: 82px;
  overflow: hidden;
}
</style>
```



# VUE Router

## 一、vue-router是什么

这里的路由并不是指我们平时所说的硬件路由器，**这里的路由就是SPA（单页应用）的路径管理器**。再通俗的说，vue-router就是WebApp的链接路径管理系统。
 vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。传统的页面应用，是用一些超链接来实现页面切换和跳转的。在vue-router单页面应用中，则是路径之间的切换，也就是组件的切换。**路由模块的本质 就是建立起url和页面之间的映射关系**。

至于我们为啥不能用a标签，这是因为用Vue做的都是单页应用（**当你的项目准备打包时，运行`npm run build`时，就会生成dist文件夹，这里面只有静态资源和一个index.html页面**），所以你写的<a></a>标签是不起作用的，你必须使用vue-router来进行管理。

## 二、vue-router实现原理

SPA(single page application):单一页面应用程序，只有一个完整的页面；它在加载页面时，不会加载整个页面，而是只更新某个指定的容器中内容。**单页面应用(SPA)的核心之一是: 更新视图而不重新请求页面**;vue-router在实现单页面前端路由时，提供了两种方式：Hash模式和History模式；根据mode参数来决定采用哪一种方式。

### 1、Hash模式：

**vue-router 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。** hash（#）是URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说**hash 出现在 URL 中，但不会被包含在 http 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面**；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说**Hash模式通过锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据。hash 模式的原理是 onhashchange 事件(监测hash值变化)，可以在 window 对象上监听这个事件**。

### 2、History模式：

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

## 三、使用路由模块来实现页面跳转的方式

- 方式1：直接修改地址栏
- 方式2：this.$router.push(‘路由地址’)
- 方式3：`<router-link to="路由地址"></router-link>`

## 四、vue-router的基本使用

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



### 4.1 基本使用步骤

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

### 4.2 路由重定向

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

### 4.3 嵌套路由用法

#### 4.3.1 功能分析

- 点击父级路由链接显示模板内容
- 模板内容中又有子级路由链接
- 点击子级路由链接显示子级模板内容

#### 4.3.2 父路由组件模板

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

#### 4.3.3 子级路由模板

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

#### 4.3.4 嵌套路由配置

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

### 4.4 动态匹配路由的基本用法

#### 4.4.1 基本使用

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

#### 4.4.2 路由组件传递参数

- **$route与对应路由形成高度耦合，不够灵活，所以可以使用props将组件和路由解耦**

##### 1. **props的值为布尔类型**

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

##### **2.props的值为对象类型**

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

##### 3.props的值为函数类型

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

### 4.5 vue-router编程式导航

#### 4.5.1 页面导航的两种方式

- **声明式导航**：通过<u>点击链接</u>实现导航的方式，叫做声明式导航

  例如：普通网页中的<a></a>链接后者vue中的<router-link></router-link>

- 编程式导航：通过调用Javascript形式的API实现导航的方式，叫做编程式导航

  例如：普通网页中的location.href

#### 4.5.2 编程式导航基本用法

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

### 4.6vue-router命名路由

#### 4.6.1 命令路由的配置规则

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

## 五、 vue-router参数传递

声明式的导航`<router-link :to="...">`和编程式的导航`router.push(...)`都可以传参，本文主要介绍前者的传参方法，同样的规则也适用于编程式的导航。

### 1.用name传递参数

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

### 2 .通过`<router-link>` 标签中的to传参

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

### 3.利用url传递参数----在配置文件里以冒号的形式设置参数。

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

### 4. 使用path来匹配路由，然后通过query来传递参数

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

## 六、vue-router配置子路由(二级路由)

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

## 七、单页面多路由区域操作

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

## 八.`$route` 和 `$router` 的区别

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

## 九、 如何设置404页面

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

##### Form 属性

| 属性名                    | 说明                                                         | 类型    | 可选值                | 默认值 |
| ------------------------- | ------------------------------------------------------------ | ------- | --------------------- | ------ |
| `model`                   | 表单数据对象                                                 | object  | ——                    | ——     |
| `rules`                   | 表单验证规则                                                 | object  | ——                    | ——     |
| `inline`                  | 行内表单模式                                                 | boolean | ——                    | false  |
| `label-position`          | 表单域标签的位置，如果值为 left 或者 right 时，则需要设置 `label-width` | string  | right/left/top        | right  |
| `label-width`             | 表单域标签的宽度，例如 '50px'。作为 Form 直接子元素的 form-item 会继承该值。支持 `auto`。 | string  | ——                    | ——     |
| `label-suffix`            | 表单域标签的后缀                                             | string  | ——                    | ——     |
| `hide-required-asterisk`  | 是否显示必填字段的标签旁边的红色星号                         | boolean | ——                    | false  |
| `show-message`            | 是否显示校验错误信息                                         | boolean | ——                    | true   |
| `inline-message`          | 是否以行内形式展示校验信息                                   | boolean | ——                    | false  |
| `status-icon`             | 是否在输入框中显示校验结果反馈图标                           | boolean | ——                    | false  |
| `validate-on-rule-change` | 是否在 `rules` 属性改变后立即触发一次验证                    | boolean | ——                    | true   |
| `size`                    | 用于控制该表单内组件的尺寸                                   | string  | medium / small / mini | ——     |
| `disabled`                | 是否禁用该表单内的所有组件。若设置为 true，则表单内组件上的 disabled 属性不再生效 | boolean | ——                    | false  |

- **model**的绑定要使用`:model="fromData"`，不能使用`v-model="fromData"`
- 在`<el-from>`中绑定**rules**时，使用`:rules="ruleFrom"`进行绑定 ，在`<el-from-item>`中定义prop，prop的名称要与ruleFrom中对象键值对应
- **data中的form要和rules结构完全一样，一一对应，在prop中要定义的和v-model的一样**
- `:inline="true"`：设置为行内显示
- `:model='formData'`：对表单进行数据绑定
- `:rules='rules'`：进行规则绑定，`'rules'`为data中的对象，在`<el-form-item>`的`prop`属性中写入对应的键名称。
- `rules`中单个表单域校验规则可以包含多个数组，每个数组即是一条校验规则
- `rules`数组中的单个检验规则对象中包含多个参数

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

##### `rules`规则的参数：

###### type：

表明要使用验证器的类型，类似数据格式检验，其中还有email、url、regexp、method等特定格式字段的验证。

使用这个，我们就可以对一些特定的字段进行校验，而不用再像以前一样写正则，做判断。

比如只需要配置 type:'email' 的规则就可以验证email了，验证器都已经封装好了这些功能，你只需调用就可以了。可识别的类型值有：

- `string`: 字符串类型（默认值）
- `number`: 数字类型
- `boolean`:布尔类型
- `method`: 函数类型
- `regexp`:正则表达式
- `integer`: 整型
- `float`: 双精度浮点型数字
- `array`: 数组类型
- `object`: 对象类型
- `enum`: 枚举值
- `date`: 日期格式
- `url`: 网址格式
- `hex`: 16进制数字
- `email`: 电子邮箱格式
- `any`: 任意类型

验证电子邮箱的完整示例代码：

```js
email = [
    {
        type: "string",
    	required: true,
    	message: '请输入邮箱地址',
    	trigger: 'blur'
    },
    {
        type: 'email',
    	message: '请输入正确的邮箱地址',
    	trigger: ['blur', 'change']
    }
]
```

###### required：

必填字段，即非空验证。如上面实例中的的非空验证，以及邮箱前边的必填符号*，就是这个参数的功劳。

###### pattern

正则表达式，如果需要验证手机号码之类，可以直接编写正则表达式配置到校验规则中，那么就不需要自己去校验了，由校验器自动校验。

```js
{ type : "string" , required: true , pattern : /^[a-z]+$/ }
```

###### min/max

判断数据大小范围，通常对数字大小范围做校验。对于字符串和数组类型，将根据长度进行比较。

```js
{ required: true, message: '请输入活动名称', trigger: 'blur' },
{ min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
```

###### len

长度验证，如11位手机号码。

```js
roles: {type: "array", required: true, len: 3 }
```

###### enum

枚举值验证，示例代码如下：

```js
role: {type: "enum", enum: ['admin', 'user', 'guest']}
```

###### whitespace

验证是否只有空格(如果没有该配置，则全空格的输入值也是有效的）。

```js
whitespace: [{
    type: "string",
    message: '只存在空格',
    whitespace:true,
    trigger: ['change', 'blur']
}]
```

###### transform

有时有必要在验证之前转换值，以强制或以某种方式对其进行清理。为此 `transform` ，向验证规则添加一个功能。在验证之前，先转换属性，然后将其重新分配给源对象，以更改该属性的值。貌似这个只能辅助校验，并**不能改变组件绑定变量本身的值**

```js
// 校验
transform: [
 {
    type: 'enum',
    enum: [2,4,6], 
    message: `结果不存在`, 
    trigger: ['change', 'blur'],
    transform(value) {
      return Number(value * 2)
    }
  }
]
```

###### fields

深层规则，可以通过将嵌套规则分配给规则的属性来验证`object`或`array`类型的验证规则，如地址对象的省市区的规则验证：

- object类型：

  ```js
  address: {
      type: "object", required: true,
      fields: {
        street: {type: "string", required: true},
        city: {type: "string", required: true},
        zip: {type: "string", required: true, len: 8, message: "invalid zip"}
      }
    }
  ```

- array类型：

  ```js
  roles: {
      type: "array", required: true, len: 3,
      fields: {
        0: {type: "string", required: true},
        1: {type: "string", required: true},
        2: {type: "string", required: true}
      }
    }
  ```

###### messages

未通过校验的提示信息：

```js
{name:{type: "string", required: true, message: "Name is required"}}
```

- 支持html:

  ```js
  {name:{type: "string", required: true, message: "<b>Name is required</b>"}}
  ```

- 支持vue-i18n:

  ```js
  {name:{type: "string", required: true, message: () => this.$t( 'name is required' )}}
  ```

###### validator

可以为指定字段自定义验证函数——这就相当于把前边配置的东西用js按照以前的方式编写验证逻辑了。虽然麻烦点，但是能实现比较复杂的业务逻辑判断。
**简单的用法：**

```js
field: {
    validator(rule, value, callback) {
      return value === 'test';
    },
    message: 'Value is not equal to "test".',
  }
```

**复杂的用法：**

```js
......    
	data() {
    	const checkAge = (rule, value, callback) => {
            if (!value) {
              return callback(new Error('年龄不能为空'));
            }
            setTimeout(() => {
              if (!Number.isInteger(value)) {
                callback(new Error('请输入数字值'));
              } else {
                if (value < 18) {
                  callback(new Error('必须年满18岁'));
                } else {
                  callback();
                }
              }
            }, 1000);
        };
      	return {
        ruleForm: {
          age: 11
        },
        rules: {          
          age: [{
            type: 'number',
            required: true,
            validator: checkAge,
            trigger: ['blur', 'change']
          }]
        }
      };
}
......
```

##### Form方法

| 方法名          | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| `validate`      | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise |
| `validateField` | 对部分表单字段进行校验的方法                                 |
| `resetFields`   | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果   |
| `clearValidate` | 移除表单项的校验结果。传入待移除的表单项的 prop 属性或者 prop 组成的数组，如不传则移除整个表单的校验结果 |

##### Form-Item 属性

| 参数             | 说明                                                         | 类型    | 默认值 |
| ---------------- | ------------------------------------------------------------ | ------- | ------ |
| `prop`           | 表单域 model 字段，在使用 validate、resetFields 方法的情况下，该属性是必填的 | string  | ——     |
| `label`          | 标签文本                                                     | string  | ——     |
| `label`-width    | 表单域标签的的宽度，例如 '50px'。支持 `auto`。               | string  | ——     |
| `required`       | 是否必填，如不设置，则会根据校验规则自动生成                 | boolean | false  |
| `rules`          | 表单验证规则                                                 | object  | ——     |
| `error`          | 表单域验证错误信息, 设置该值会使表单验证状态变为`error`，并显示该错误信息 | string  | ——     |
| `show-message`   | 是否显示校验错误信息                                         | boolean | true   |
| `inline-message` | 以行内形式展示校验信息                                       | boolean | false  |
| `size`           | 用于控制该表单域下组件的尺寸                                 | string  | ——     |



### Data



### Notice



### Navigation



### Others





# 正则表达式

## **元字符(metacharacter)**

### `\b`

代表着单词的开头或结尾，也就是单词的分界处。虽然通常英文的单词是由空格，标点符号或者换行来分隔的，但是\b并不匹配这些单词分隔字符中的任何一个，它**只匹配一个位置**。

例如要查找单词`hi`,为避免匹配*him*,*history*,*high*等等，使用`\b`来限定：

```
\bhi\b
```



### `.`



Token

# 开发案例

## 登录与退出

### 登录业务相关技术点

- http是无状态的
- 通过cookie在客户端记录状态
- 通过session在服务端记录状态
- 通过token方式维持状态

注意：在前后端**不存在跨域问题**时，推荐使用`cookie`和`session`来记录登录状态；反之，**存在跨域问题时**，要用token来记录。

#### token原理

![image-20201220213752052](C:\Users\lcr\Desktop\img\image-20201220213752052.png)



- 其他





# git命令

`git checkout -b login`：创建一个login子分支，并通过checkout命令切换到该子分支

`git branch`：查看当前项目中的所有分支

`git add`

`git push`

`git status`

`git commit -m "add files"`

`git add .`





# vscode备份插件

## 安装Settings Sync

vscode插件中心直接搜索安装即可。

[![UTOOLS1587289082727.png](https://user-gold-cdn.xitu.io/2020/4/19/17191cd4d34a6ce4?w=1295&h=643&f=png&s=134258)](https://user-gold-cdn.xitu.io/2020/4/19/17191cd4d34a6ce4?w=1295&h=643&f=png&s=134258)

## github生成token和gistid

### token获取步骤：

**网址**：github：https://github.com/
**路径**：Settings -> Developer settings -> Personal access tokens
**操作**：点击按钮 Generate new token 新增一个token，选择gistid即可。
**记住生成的token值**

### gistid获取步骤

**网址**：github：https://github.com/

**路径**： 点击右上角+号 New gist

**操作**： 任意填写gist描述 -> 点击生成私钥(英文的) ->记录下来

## 配置本设备gistId和token

- Ctrl + P / F1，弹出命令窗口
- 输入`> sync`
- 选择`Advaced Options`

[![批注 2020-04-19 174414.jpg](https://user-gold-cdn.xitu.io/2020/4/19/17191d34fd493129?w=1276&h=615&f=jpeg&s=77754)](https://user-gold-cdn.xitu.io/2020/4/19/17191d34fd493129?w=1276&h=615&f=jpeg&s=77754)

填写gistid和token即可

## 同步、下载

### 上载设定

**按Shift + Alt + U**（macOS：Shift + Option + U）

> 在命令面板中键入“>同步”，以顺序下载/上传

首次下载或上传时，欢迎页面将自动打开，您可以在其中配置“设置同步”。

选择上传后，上传设置后。您将看到“摘要”详细信息以及每个上传的文件和扩展名的列表。

### 下载您的设置

**按Shift + Alt + D**（macOS：Shift + Option + D）

> 在命令面板中键入“>同步”，以顺序下载/上传

首次下载或上传时，欢迎页面将自动打开，您可以在其中配置“设置同步”。

选择下载后，下载后。设置同步将向您显示摘要，其中包含要下载的每个文件和扩展名的列表。

将打开新的弹出窗口，使您可以重新启动代码以应用设置。

## 恢复备份

1. 在需要同步的电脑打开VSCode,安装相同的插件。
2. 按快捷键 shift+alt+d 或 ctrl+p 输入>sync点击Download Settings
3. 把GITHUB GIST的access token 和gist id粘贴然后回车。(可能需要重新到github生成token)



# CSS笔记

## div居中

### 1.水平居中

方法一：直接加上`<center>`标签即可，或者设置`margin:auto;`

方法二：`div`使用绝对布局，`left`设置为50%，`transform`向左平移自己宽度的50%

```css
position: absolute;
left: 50%;
transform: translate(-50%);
```

### 2.垂直居中

## [CSS实现垂直居中的常用方法](https://www.cnblogs.com/yugege/p/5246652.html)

　在前端开发过程中，盒子居中是常常用到的。其中 ，居中又可以分为水平居中和垂直居中。水平居中是比较容易的，直接设置元素的margin: 0 auto就可以实现。但是垂直居中相对来说是比较复杂一些的。下面我们一起来讨论一下实现垂直居中的方法。

​	已经实现水平居中了！接下来该打大boss了——实现垂直居中。不过，在这之前，我们先要设置div元素的祖先元素html和body的高度为100%（因为他们默认是为0的），并且清除默认样式，即把margin和padding设置为0（如果不清除默认样式的话，浏览器就会出现滚动条，聪明的亲，自己想想问什么）。

 	接下来，需要做的事情就是要让div往下移动了。我们都知道top属性可以使得元素向下偏移的。但是，由于默认情况下，由于position的值为static（静止的、不可以移动的），元素在文档流里是从上往下、从左到右紧密的布局的，我们不可以直接通过top、left等属性改变它的偏移。所以，想要移动元素的位置，就要把position设置为不是static的其他值，如relative,absolute,fixed等。然后，就可以通过top、bottom、right、left等属性使它在文档中发生位置偏移（注意，relative是不会使元素脱离文档流的，absolute和fixed则会！也就是说，relative会占据着移动之前的位置，但是absolute和fixed就不会）。

​	我们刷新一下页面，发现跟之前是没有任何变化的，因为，我们仅仅是使设置了元素的position=relative而已，但是还没开始移动他的垂直偏移。好，下面我们就让它偏移吧！垂直偏移需要用到top属性，它的值可以是具体的像素，也可以是百分数。因为我们现在不知道父元素（即body）的具体高度，所以，是不可以通过具体像素来偏移的，而应该用百分数。既然是要让它居中嘛！好，那么我们就让它的值为50%不就行了吗？问题真的那么简单，我们来试一下，就设置50%试一下。

通过观察上图，只要让div的中心移动到红线的位置，那么整个div就居中了。那怎么让它中心移动到红线处呢？从图中可以观察到，从div的中心到红线的距离是div自身高度的一半。这时候，我们可以使用通过margin-top属性来设置，因为div的自身高度是300，所以，需要设置他的margin-top值为-150。为什么是要设置成负数的呢？因为正数是向下偏移，我们是希望div向上偏移，所以应该是负数。

确实已经居中了。

除了可以使用margin-top把div往上偏移之外，CSS3的transform属性也可以实现这个功能，通过设置div的transform: translateY(-50%)，意思是使得div向上平移（translate）自身高度的一半(50%)。

 上面的两种方法，我们都是基于设置div的top值为50%之后，再进行调整垂偏移量来实现居中的。如果使用CSS3的弹性布局（flex）的话，问题就会变得容易多了。使用CSS3的弹性布局很简单，只要设置父元素（这里是指body）的display的值为flex即可。





方法一：`div`使用绝对布局，`top`设置为50%，`transform`向上平移自己高度的50%

```css
position: absolute;
top: 50%;
transform: translate(0,-50%);
```

### 3.水平垂直都居中

```css
position: absolute;
top: 50%;
left:50%;
transform: translate(-50%,-50%);
```
