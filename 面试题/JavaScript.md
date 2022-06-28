### JS中基础数据类型有那几种？了解包装对象吗？

**答：**基础数据类型有6种：

boolean
null
undefined
number
string
symbol

基础数据类型都是值，所以没有方法提供调用的 列如：`undefined.split('')`；那么为什么 `abc.split('')`类似这种调用可以被允许？原因是 js 中存在包装对象，会把字符串先包装成对象然后再调用对象下的一些方法，方法调用完成之后再销毁对象，这样就完成了基础数据类型的函数调用功能。

```js
function mySplit(str, method, arg) {
  let obj = new Object(str)
  return obj[method](arg)
}
let str = 'x t t'
mySplit(str, 'split', '')
```

**强调：** null 通过 typeof 看到的是 object 类型，但 null 并不是 object 类型，而是一个基础数据类型。是因为 JavaScript 在早期发展的时候，只能存在32位的操作系统，所以为了考虑性能问题，就把所有 000 开头的定义成对象，而 null 的定义全部都是 0，就被系统误认为是 object 类型。



### 如何判断this？箭头函数的this是什么？

**答：**可以分为三种场景来描述this

1、函数中直接调用的this。如下：

```js
function foo() {
  coonsole.log(this)
}
foo()
```

如上 this 会指向 window ，需要注意在严格模式下 this 会是 undefined 情况，同样也需要注意在 script 标签 `type="module"`下也会是 undefined。

2、在对象里调用的情况。如下：

```js
let obj = {
  myname: 'xtt',
  foo: function() {
    console.log(this)
  }
}
obj.foo() // this会指向调用的对象obj
```

3、在构造函数及类中 this 会指向实例化的对象。如下：

```js
function Person(name) {
  this.name = name
}
Person.prototype.foo = function() {
  console.log(this)
}
let cicada = new Person('xtt')
cicada.foo() // this指向实例化对象cicada
```

**箭头函数的this是什么？**

**答：**箭头函数没有自己的 this ，它会继承上一级作用域链的 this



### 什么是闭包？

**答：**函数和对其周围状态的引用捆绑在一起构造成**闭包**，简而言之就是一个函数可以访问到另一个函数里的变量。列如：

```js
function foo() {
	let a = 10
	return function() {
		console.log(a)
	}
}
let myFn = foo()
myFn() // 10
```

```js
for(var i=0; i<5; i++) {
  (function(i) {
    setTimeout(() => {
      console.log(i); // 1,2,3,4
    })
  })(i)
}
```



### 判断数据类型有几种方法

**答：** typeof、instanceof、constructor、Object.prototype.toString.call()

* typeof

  * 缺点：`typeof null`的值为`Object`，无法分辨是`null`还是`Object`

* instanceof

  * 缺点：只能判断对象是否存在于目标对象的原型链上

* `constructor`

* Object.prototype.toString.call()

  * 一种最好的基本类型检测方式 `Object.prototype.toString.call()` ;它可以区分 null 、 string 、boolean 、 number 、 undefined 、 array 、 function 、 object 、 date 、 math 数据类型。

  * 缺点：不能细分为谁谁的实例

    

​     



### 防抖debounce、节流throttle

```js
debounce(func, delay) {
  let timer = null;
  return function (...args) {
    if (timer) clearTimeout(timer);
    timer = setTimeout((args) => {
      func.apply(this);
    }, delay);
  }
}
```











