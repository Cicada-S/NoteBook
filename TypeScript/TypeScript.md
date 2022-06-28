## TypeScript



### TypeScript  增加了什么？

* 类型
* 支持ES新的特性
* 添加ES不具备的新特性
* 丰富的配置选项
* 强大的开发工具



### 1、TypeScript 开发环境搭建

1. 下载Node.js
2. 安装Node.js
3. 使用npm全局安装TypeScript
   1. 进入命令行
   2. 输入：`npm i -g typescript
4. 创建一个ts文件
5. 使用tsc对ts文件进行编译
   1. 进入命令行
   2. 进入ts文件所在的目录
   3. @执行命令：tsc xxx.ts





### 2、基本类型

#### 类型声明

* 类型声明是TS非常重要的一个特点

* 通过类型声明可以指定TS中变量（参数、新参）的类型

* 指定类型后，当为变量赋值时，TS编译器会自动检查==值是否符合类型声明==，符合则赋值，否则报错

* 语法：

  ```typescript
  let 变量: 类型
  let 变量: 类型 = 值
  
  function fn(参数: 类型, 参数: 类型): 类型 {
    ...
  }
  ```



#### 自动类型判断

* TS拥有自动的类型判断机制
* 当对变量的声明和赋值是同时进行的，TS编译器会自动判断变量的类型
* 所有如果你的变量的声明和赋值同时进行的，可以省略掉类型声明



#### 类型

| 类型    | 例子            | 描述                         |
| ------- | --------------- | ---------------------------- |
| number  | 1,-33,2.5       | 任意数字                     |
| string  | 'hi',"hi",`hi`  | 任意字符串                  |
| boolean | true、false     | 布尔值true或false            |
| 字面量  | 其本身          | 限制变量的值就是该字面量的值 |
| any     | *               | 任意类型                     |
| unknown | *               | 类型安全的any                |
| void    | 空值(undefined) | 没有值(或undefined)          |
| never   | 没有值          | 不能是任何值                 |
| object  | {name:'孙悟空'} | 任意的JS对象                 |
| array | [1,2,3] | 任意JS对象 |
| tuple | [4,5] | 元素，TS新增类型，固定长度数组 |
| enum | enum{A,B} | 枚举，TS中新增类型 |

#### number

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```

#### string

```typescript
let color: string = 'blue'
color = 'red'
```

#### boolean

```typescript
let isDone: boolean = false
```

#### 字面量


* 也可以使用字面量去指定变量的类型，通过字面量可以确定变量的取值范围

```typescript
// | 表示或
let color: 'red' | 'blue' | 'black'
let num: 1 | 2 | 3 | 4 | 5
```

#### any

```typescript
// any 表示的是任意类型，一个变量设置类型为any后相当于对该变量关闭了TS的类型检测
// 声明变量如果不指定类型，则TS解析器会自动判断变量的类型为any (隐式的any)
let d: any = 4
d = 'hello'
d = true

// d的类型是any, 它可以赋值给任意变量
let s: string
s = d
```

#### unknown

```typescript
// unknown 表示未知类型的值  实际上是一个类型安全的any 
let notSure: unknown = 4
notSure = 'hello'

// unknown 类型的变量, 不能直接赋值给其他变量
let e: unknown
let s: string
if(typeof e === 'string') {
  s = e
}
```

#### void

````typescript
// void 用来表示空, 以函数为例, 就表示没有返回值的函数
function fn(num): void{}

let unusable: void = undefined
````

#### never

```typescript
// never 表示永远不会返回结果
function error(message: string): never {
  throw new Error(message)
}
```

#### object

```typescript
// object 表示一个js对象
let a: object
a = {};
a = function() {}

// {} 用来指定对象中可以包含哪些属性
// 语法：{属性名: 属性值, 属性名: 属性值}
// 在属性名后边加上?, 表示属性是可选的
let b: {name: string, age?: number}
b = {name: 'xtt', age: 17}

// [propName: string]: any 表示任意类型的属性
let c: {name: string, [propName: string]: any}
c = {name: 'xtt', age: 17, gender: '女'}

/**
 * 设置函数机构的类型声明：
 *      语法：（形参：类型，形参：类型 ...） => 返回值
 */
let d: (a: number, b: number) => number
```

#### array

```typescript
/**
 * 数组的类型声明:
 *      类型[]
 *      Array<类型>
 */
// string[] 表示字符串数组
let e: string[]
e = ['a', 'b', 'c']

// number[] 表示数值数组
let f: number[]

let g: Array<number>
g = [1, 2, 3]
```

#### tuple

```js
/**
 * tuple 元组， 元组就固定长度的数组
 *       		语法：[类型，类型，类型]
 */
let h: [string, number]
h = ['xtt', 17]
```

#### enum

```typescript
enum Gender {
  male = 1,
  Female = 0
}

let i: {name: string, gender: Gender}
i = {
  name: 'xtt',
  gender: Gender.Female 
}

// & 表示同时
let j: { name: string } & { age: number }
j = {name: 'xtt', age: 17}
```


#### 类型别名

```typescript
type myType = 1 | 2 | 3 | 4 | 5
let k: myType
let l: myType

k = 2
```


#### 类型断言 

* 有些情况下，变量的类型对于我们来说是很明确，但是TS编译器却并不清楚，此时，可以通过类型断言来告诉编译器变量的类型，断言有两种情况形式：

  * 第一种:

    ```typescript
    /**
     * 语法:
     *    变量 as 类型
     *    <类型>变量
     */
    let someValue: unknown = 'this is a string'
    let strLength: number = (someValue as string).length
    ```

  * 第二种

    ```typescript
    let someValue: unknown = 'this is a string'
    let strLength: number = (<string>someValue).length
    ```





### 3、编译选项

#### 3.1 自动编译文件

* 编译文件时，使用 -w 指令后，TS编译器会自动监视文件的变化，并在文件发生变化时对文件进行重新编译.

* 实例：

  ```终端
  tsc xxx.ts -w
  ```



#### 3.2 自动编译整个项目

* 如果直接便用tsc指令，则可以自动将当前项目下的所有ts文件编译为js文件。

* 但是能直接使用tsc命令的前提时，要先在项目根目录下创建一个ts的配置文件 tsconfig.json

* tsconfig.json是一个SON文件，添加配置文件后，只需只需 tsc 命令即可完成对整个项目的编译

* 配置选项：

  include

  * 定义希望被编译的文件所在的目录

  * 默认值： ["**/*"]

  * 示例

    ```tsconfig.json
    "include":["src/**/*", "tests/**/*"]
    ```

    上述示例中，所有src目录和tests目录下的文件都会被编译

    

  exclude

  * 定义需要排除在外的目录

  * 默认值： ["node_modules", "bower_components", "jspm_packages"]

  * 示例：

    ```tsconfig.json
    "exclude": ["./src/hello/**/*"]
    ```

    上述示例中，src下hello目录下的文件都不会被编译

  

  extends

  * 定义被继承的配置文件

  * 示例:

    ```tsconfig.json
    "extends": "./configs/base"
    ```

    上述示例中，当前配置中间中会自动包含config目录下base.json中的所有配置信息

  

  files

  * 指定被编译文件的列表，只有需要编译的文件少时才会用到

  * 示例:

    ```tsconfig.json
    "files": [
    	"core.ts",
    	"sys.ts",
    	"types.ts",
    	"scanner.ts",
    	"utilities.ts",
    	"binder.ts",
    	"checker.ts"
    	"tsc.ts"
    ]
    ```

    列表中的文件都会被TS编译器所编译

  

  compilerOptions

  * 编译选择是配置文件中非常重要也比较复杂的配置选项

  * 在compilerOptions中包含多个子选项，用来完成对编译的配置

  * 项目选项

    target

    * 设置ts代码编译的目标版本

    * 可选值：

      ES3（默认）、ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext

      ```tsconfig.json
      "compilerOptions": {
      	"target": "ES6"
      }
      ```

      如上设置我们所编写的ts代码将会被编译为ES6版本的js代码

    

    lib

    * 指定代码运行时所包含的库（宿主环境）

    * 可选值：

      ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext、DOM、WebWorker、ScriptHost ...

      ```tsconfig.json
      "compilerOptions": {
      	"target": "ES6",
      	"lib": ["ES6", "DOM"],
      	"outDir": "dist",
      	"outFile": "dist/aa.js"
      }
      ```

    

    module

    * 设置编译后代码使用的模块化系统

    * 可选值:

      CommonJS、UMD、AMD、System、ES2020、ESNext、None

      ```tsconfig.json
      "compilerOptions": {
      	"module": "CommonJS"
      }
      ```

    

    outDir

    * 编译后文件的所在目录
    * 默认情况下，编译后的js文件会和ts文件位于相同的目录，设置outDir后可以改变编译后的文件位置
    * 





### 4、webpack

* 通常情况下，实际开发中 我们都需要使用构建工具对代码进行打包，TS同样也可以结合构造工具一起使用，下边以webpack为例介绍一下如何结合构造工具使用TS。

* 步骤：

  1. 初始化项目

     * 进入项目根目录，执行命令 `npm init -y`
     * 主要作用：创建package.json文件

  2. 下载构建工具

     * `npm i -D webpack webpack-cli typescript ts-loader`
     * `webpack` 构建工具webpack
     * `webpack-cli` webpack的命令工具
     * `typescript`  ts编译器
     * `ts-loader` ts加载器，用于子啊webpack中编译ts文件

  3. 根目录下创建webpack的配置文件`webpack.config.js`

     ```js
     // 引入一个包
     const path = require('path')
     
     // webpack 中所有的配置信息都应该写在module.exports中
     module.exports = {
       // 指定入口文件
       entry: './src/index.ts',
     
       // 指定打包文件所在目录
       output: {
         // 指定打包文件的目录
         path: path.resolve(__dirname, 'dist'),
         // 打包后的文件
         filename: 'bundle.js'
       },
     
       // 指定webpack打包时要使用模块
       module: {
         // 指定要加载的规则
         rules: [
           {
             // test指定的是规则生效的文件
             test: /\.ts$/,
             // 要使用的loader
             use: 'ts-loader',
             // 要排除的文件
             exclude: /node_modules/
           }
         ]
       }
     }
     ```
     
  4.    根目录下创建ts的配置文件`tsconfig.js`

     ```json
     {
       "compilerOptions": {
         "module": "ES2015",
         "target": "ES6",
         "strict": true
       } 
     }
     ```
  
     
  









