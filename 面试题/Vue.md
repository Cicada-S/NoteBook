

### 什么是MVVM模式？

M 是 model(模型层) 负责数据的存储和具体的业务逻辑

V 是 view(视图层) 负责数据的展示

VM 是 view model(视图模型层) 负责连接 model 跟 view 具有双向绑定 自动更新视图



### Vue 生命周期

```
beforeCreate
created

beforeMount
mounted

beforeUpdate
updated

beforeDestroy
destroyed

被 keep-alive 缓存的组件 激活 时调用。
activated
被 keep-alive 缓存的组件 失活 时调用。
deactivated
```





### Vue 组件间有哪些通信方式？

**答：** 有6种，分别是：

1. `props / $emit` 适用**于父子之间组件通信**这种方法是 Vue 组件的基础，相信同学们都耳闻能详，所以此处讲究不举例展开介绍。

   ```vue
   // 父传子
   <A user-name="xtt"></A>
   props: {
   	userName: String
   },
   
   // 子传父
   <button @click="emit">发射按钮</button>
   emit() {
   	this.$emit('myAccept', 17)
   }
   <A @myAccept="accept"></A>
   accept(age) {
   	console.log(age);
   },
   ```

2. `ref` 与 `$arent` / `$children` **适用于父子组件通信** `ref`：如果在普通的DOM元素上使用，引用指向的就是DOM元素：如果用在子组件上，引用就向组件示例 `$parent / $children`: 访问父 / 子实例

   ```vue
   <A @ref="Aref"></A>
   <button @click="getAref">点击</button>
   getAref() {
   	console.log(this.$refs.arent)
   	console.log(this.$children[0])
   }
   ```

3. `EventBur ($emit / $on)` **适用于父子、隔代、兄弟组件通信** 这种方法通过一个空的 Vue 示例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

   ```vue
   // 孙组件
   <button @click="handle">B按钮</button>
   import MyEvent from './MyEvent'
   handle() {
     MyEvent.$emit('cHandle', 'cicada')
   }
   
   // 祖组件
   import MyEvent from './MyEvent'
   created() {
     MyEvent.$on('cHandle', function(arg) {
       console.log(arg);
     })
   }
   ```

4. `$attrs / $ listeners` **适用于隔代组件通信** `$attrs`: 包含了父作用域中不被 prop 所识别（且获取）的特性绑定（class 和 style 除外）。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定（class 和 style 除外），并且可以通过 `v-binf="$attrs"` 传入内部组件。`$listeners`: 包含了父作用域中的（不含`.native`修饰符的）v-on事件监听器。它通过 `v-on="$listeners"` 传入内部组件。

   ```vue
   <A :height="'160cm'" :age="17"></A>
   
   <h2>{{ $attrs }}</h2>
   <B v-bind="$attrs"></B>
   ```

5. `provide / inject` **适用于隔代组件通信**祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 `inject` 来注入变量。`provide / inject` API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

   ```js
   provide: {
   	myName: 'Hello组件里的provide'
   },
   
   inject: ['myName'],
   ```

6. `Vuex`**适用于父子、隔代、兄弟组件通信** Vuex 是专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store (仓库)。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会得到高效更新。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。 这样使得我们可以方便地跟踪每一个状态的变化。

   
   
   
   
### vue 中 v-show 和 v-if 的区别是什么？

**答：**`v-show` 只是在 `display: none` 和 `display: block` 之间切换。无论初始条件是什么都会被渲染出来，后面字需要切换 CSS， DOM 还是一直保留着的。

`v-if` 的话就得说到 Vue 底层的编译了。当属性初始为 `false` 时，组件就不会被渲染，直到条件为 `true`，并且切换条件时会触发销毁 / 挂载组件，并且基于 `v-if`的这种惰性渲染机制，可以在必要的时候才去渲染组件，减少整个页面的初始渲染开销。

   

   

### keep-alive 组件有什么作用？

**答：** 如果你需要在组件切换的时候，保存一些组件的状态防止多次渲染，就可以使用 `keep-alive` 组件包裹需要保存的组件。

对于 `peek-alive` 组件来说，它拥有两个独有的生命周期钩子函数，分别为 `activated` 和 `deactiated`。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactiated` 钩子函数，命中缓存渲染后会执行 `actived` 钩子函数。



### 说一下Vue生命周期钩子函数？

**答：**

* beforeCreate 这个时期，this变量还不能使用，在data下的数据，和 methods 下的方法，watcher 中的事件不能获得到。
* created 这个时候可以操作 vue 实例中的数据和各种方法，但是还不能对 `dom` 节点进行操作。
* beforeMount 在挂载开始之前被调用：相关的 render 函数首次被调用
* mounted 挂载完毕，这时 `dom` 节点被渲染到文档内，一些需要 `dom` 的操作在此时才能正常进行
* beforeUpdate `data`中数据已经更新完毕，页面视图还未相应更改
* updated 数据和和试图都更新完毕
* beforeDestroy 销毁之前，实例上事件、指令等都可以使用，这里组件没有真正的销毁。
* destroyed 数据、指令、完全销毁



### vue中 computed 和 watch 区别?

**答：**`computed` 是计算属性，







