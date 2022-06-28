## Node.js



### 1. 初识Node.js

#### 1.1 回顾与思考

>1. **已经掌握了那些技术**



>2. **浏览器中的 JavaScript 的组成部分**

​						**浏览器中的 JavaScript**

| js 核心语法        | WebAPI                           |
| ------------------ | -------------------------------- |
| 变量、数据类型     | DOM 操作                         |
| 循环、分支、判断   | BOM 操作                         |
| 函数、作用域、this | 基于 XMLHttpRequest 的 Ajax 操作 |
| etc...             | etc...                           |



>3. **为什么 JavaScript 可以在浏览器中被执行**

***因为浏览器中的 JavaScript 解析引擎***

| 浏览器         | JavaScript引擎     |
| -------------- | ------------------ |
| Chrome 浏览器  | V8                 |
| Firefox 浏览器 | OdinMonkey(奥丁猴) |
| Safri 浏览器   | JSCore             |
| IE 浏览器      | Chakra(查克拉)     |
| etc...         |                    |



> 4. **为什么 JavaScript 可以操作 DOM 和 BOM**

*A：因为每个浏览器都==内置了==DOM、BOM 这样的 API 函数，因此，浏览器中的 JavaScript 才可以调用它们*



> 5. **浏览器中的 JavaScript 运行环境**

==运行环境== 是指==代码正常运行所需的必要环境==。

1. V8 引擎负责解析和执行 JavaScript 代码
2. 内置的 API 是由==运行环境==提供的特殊接口，==只能在所属的运行环境中被调用==。



> 6. **JavaScript 能否做后端开发**

**Node.js**





#### 1.2 Node.js 简介

> 1. **什么是 Node.js**

==Node.js 是==一个基于 Chrome V8 引擎的==JavaScript 运行环境==



> 2. **Node.js 中的 JavaScript 运行环境** 

V8引擎

| 内置API |      |      |             |             |        |
| ------- | ---- | ---- | ----------- | ----------- | ------ |
| fs      | path | http | js 内置对象 | querystring | etc... |

注意：

1. ==浏览器==是 JavaScript 的==前端运行环境==。
2. ==Node.js==是 JavaScript 的==后端运行环境==。
3. Node.js 中==无法调用==DOM 和 BOM 等==浏览器内置 API==。



> 3. **Node.js 可以做什么** 

1. 基于 Express 框架 ()，可以快速构建 Web 应用
2. 基于 Electron 框架 ()，可以构建跨平台的桌面应用
3. 基于 restify 框架 ()，可以快速构建 API 接口项目
4. 读写和操作数据库，创建实用的命令行工具辅助前端开发、etc...

总之：Node.js 是==大前端时代==的"大宝剑"，有了 Node.js 这个超级 buff 的加持，前端程序员的==行业竞争力==会越来越强！



> 4. **Node.js 好学吗？   Node.js 怎么学？**

==会 JavaScript，就能学会 Node.js！！！==



浏览器中的 JavaScript 学习路径：

JavaScript 基础语法 + 浏览器内置 API（DOM + BOM）+ 第三方库（JQuery、art-template 等）



Node.js 的学习路径：

JavaScript 基础语法 +==Node.js 内置 API 模块==(fs、path、http 等) +==第三方 API 模块==（express、mysql 等）





#### 1.3 Node.js 环境的安装

> 什么是终端

*A: 终端（英文：Terminal）是专门为开发人员设计用的，==用于实现人机交互==的一种方式*

作为一名合格的程序员，我们有必要识记一些==常用的终端命令==，来辅助我们更好的操作与使用计算机。



#### 1.4 在 Node.js 环境中执行 JavaScript 代码

1. 打开终端
2. 输入 node 要执行的js文件路径

> 1. **终端中的快捷键**

1. ==↑==上一次执行的命令
2. ==tab==补全路径
3. ==esc==清空当前命令
4. ==cls==清空终端



### 2. fs 文件系统模块

#### 2.1 什么是 fs 文件系统模块

==fs 模块==是 Node.js 官方提供的，用来操作文件的模块。它提供了一系列的方式和属性，用来满足用户对文件的操作需求。

* fs.readFile() 方法，用来==读取==指定文件中的内容
* fs.writeFile() 方法，用来向指定的文件==写入==内容

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```js
const fs = require('fs')
```



  

#### 2.2 ==读取==指定文件中的内容

> 1. **fs.readFile() 的语法格式**

使用 fs.readFile() 方法，可以读取指定文件中的内容，语法格式如下：

```js
fs.readFile(path[, options], callback) 
```

参数读解：

* 参数1：==必选==参数，字符串，表示文件的路径。
* 参数2：可选参数，表示以什么==编码格式==来读取文件。
* 参数3：==必选==参数，文件读取完成后，通过回调函数拿到读取的结果。



> 2. **fs.readFile() 的示例代码**

以 utf8 的编码格式，读取指定文件的内容，并打印 err 和 dataStr 的值：

```js
const fs = require('fs')
fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  console.log(err)
  console.log(dataStr)
})
```



> 3. **判断文件是否读取成功**

可以判断 err 对象是否为 null，从而知晓文件读取的结果：

```js
const fs = require('fs')
fs.readFile('./files/1.txt', 'utf8', function(err, result) {
  if(err) {
    return console.log('文件读取失败！' + err.message)
  }
  console.log('文件读取成功，内容是：' + result)
})
```





#### 2.3 向指定的文件中写入内容

> 1. **fs.writeFile() 的语法格式**

使用  fs.writeFile() 方法，可以向指定的文件中写入内容，语法格式如下：

```js
fs.writeFile(file, data[, options], callback)
```

参数读解：

* 参数1：==必选==参数，需要指定一个==文件路径的字符串==，代表文件的存放路径。
* 参数2：==必选==参数，表示要写入的内容。
* 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
* 参数4：==必选==参数，文件写入完成后的回调函数。



>2. **fs.writeFile() 示例代码**

向指定的文件路径中，写入文件内容：

```js
const fs = require('fs')
fs.writeFile('./files/2.txt', 'Hello Node.js!', function(err) {
  console.log(err)
})
```



> 3. **判断文件是否写入成功**

可以判断 err 对象是否为 null，从而知晓文件写入的结果：

```js
const fs = require('fs')
fs.writeFile('./files/2.txt', 'Hello Node.js!', function(err) {
  if(err) {
    return console.log('文件写入失败！' + err.message)
  }
  console.log('文件写入成功！')
})
```



#### 2.5 练习 - 考试成绩整理

使用 fs 文件系统模块，将素材目录下==成绩.txt==文件中的考试数据，整理到==成绩-ok.txt==文件中。

整理前，成绩.txt文件中的数据格式如下：

```
小红=99 小白=100 小黄=70 小黑=66 小绿=88
```

整理完毕之后，希望看到的成绩-ok.txt文件中的数据格式如下:

```
小红：99
小白：100
小黄：70
小黑：66
小绿：88
```

> 核心实现步骤

1. 导入需要的 fs 文件系统模块
2. 使用==fs.readFile()==方法，读取素材目录下的==成绩.txt==文件
3. 判断文件是否读取失败
4. 文件读取成功后，处理成绩数据
5. 将处理完成的成绩数据，调用==fs.writeFile()==方法，写入到新文件==成绩-ok.txt==中



#### 2.6 fs 模块 - 路径动态拼接的问题

在使用 fs 模块操作文件时，如果提供的操作路径是以==./==或==../==开头的==相对路径==时，很容易出现路径动态拼接错误的问题。

原因：代码在运行的时候，==会以执行 node 命令时所处的目录==，动态拼接出被操作文件的完整路径。

解决方案：在使用 fs 模块操作文件时，==直接提供完整的路径==，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。

 ```js
 // 不要使用 ./ 或 ../ 这样的相对路径
 fs.readFile('./files/1.txt', 'utf-8', function(err, result) {
   if(err) return console.log('读取文件失败!' + err.message);
   console.log('读取文件成功!' + result);
 })
 
 // __dirname 表示当前文件所处的目录
 fs.readFile(__dirname + '/files/1.txt', 'utf-8', function(err, result) {
   if(err) return console.log('读取文件失败!' + err.message);
   console.log('读取文件成功!' + result);
 })
 ```





### 3. path 路径模块

#### 3.1 什么是 path 路径模块

==path 模块==是 Node.js 官方提供的，用来处理路劲的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

例如：

* path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
* path.basename() 方法，用来从路径字符串中，将文件名解析出来



如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

```js
const path = require('path')
```



#### 3.2 路径拼接

>1. **path.join() 的语法格式**

​	使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下:

```js
path.join([...paths])
```

参数解读：

* ...paths <string> 路径片段的序列
* 返回值：<string>



> 2. **path.join() 的代码示例**

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串：

```js
const pathStr = path.join('/a', '/b/c', '../', './d', 'e')
console.log(pathStr) // 输出 \a\b\d\e

const pathStr2 = path.join(__dirname, './files/1.txt')
console.log(pathStr2) // 输出 当前文件所在处目录\files\1.txt
```

注意：==今后凡是涉及到路径拼接的操作，都要使用 path.join() 方法进行处理==。不要直接使用 + 进行字符串的拼接。



#### 3.3 获取路径中的文件名

> 1. ###### **path.basename() 的语法格式**

使用 path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```js
path.basename(path[,ext])
```

参数解读：

* path <string> 必选参数，表示一个路径的字符串
* ext <string> 可选参数，表示文件扩展名
* 返回：<string> 表示路径中的最后一部分



> 2. **path.basename() 的代码示例**

使用 path.basename() 方法，可以从一个文件路径中，获取文件的名称部分：

 ```js
 const fpath = '/a/b/c/index.html' // 文件的存放路径
 
 var fullName = path.basename(fpath)
 console.log(fullName) // index.html
 
 var nameWithoutExt = path.basename(fpath, '.html')
 console.log(nameWithoutExt) // index
 ```



#### 3.4 获取路径中的文件扩展名

> 1. **path.extname() 的语法格式**

使用 path.extname() 方法，可以获取路径中的扩展名部分，语法格式如下：

```js 
path.extname(path)
```

参数解读：

* path <string> 必选参数，表示一个路径的字符串
* 返回：<string> 返回得到的扩展名字符串 



> 2. **path.extname() 的代码示例**

使用 path.extname() 方法，可以获取路径中的扩展名部分：

```js
const fpath = '/a/b/c/index.html' // 路径字符串

const fext = path.extname(fpath)
console.log(fext) // .html
```

 

#### 3.5 综合案例 - 时钟案例

> 1. **案例实现的功能**

将素材目录下的 index.html 页面，拆分成三个文件，分别是：

* index.css
* index.js
* index.html

并且将拆分出来的3个文件，存放到 clock 目录中。



> 2. **案例的实际步骤**

1. 创建两个正则表达式，分别用来匹配 <style> 和 <script> 标签
2. 使用 fs 模块， 读取需要被处理的 HTML 文件 
3. 自定义 resolveCSS 方法，来写入 index.css 样式文件
4. 自定义 resolveJS 方法，来写入 index.js 脚本文件
5. 自定义 resolveHTML 方法，来写入 index.html 文件



> 3. **步骤1 - 导入需要的模板并创建正则表达式**

```js
const fs = require('fs')
const path = require('path')

// 其中 \s 表示空白字符;  \S 表示非空白字符; * 表示匹配任意次  
const regStyle = /<style>[\s\S]*<\/style>/
const regScript =  /<script>[\s\S]*<\/script>/
```



> 3. **步骤2 - 使用 fs 模块读取需要被处理的 html 文件**

```js
fs.readFile(path.join(__dirname, '../素材/index.html'), 'utf-8', function(err, result) {
  if(err) console.log(err.message);
  
  resolveCSS(result)
  resolveJS(result)
  resolveHTML(result)
})
```



> 3. **步骤3 - 自定义 resolveCSS 方法**

```js
function resolveCSS(htmlStr) {
  // 使用正则提取页面中的 <style></style> 标签
  const r1 = regStyle.exec(htmlStr)
  // 把 <style> 标签去掉
  const newCSS = r1[0].replace('<style>', '').replace('</style>', '')
  // 然后写入到 index.css 文件中
  fs.writeFile(path.join(__dirname, './clock/index.css'), newCSS, err => {
    if(err) {
      return console.log(err.message)
    }
    console.log('写入 CSS 样式成功!');
  })
}
```



> 3. **步骤4 - 自定义 resolveJS 方法**

```js
function resolveJS(htmlStr) {
  // 使用正则提取页面中的 <script></script> 标签
  const r1 = regScript.exec(htmlStr)
  // 把 <script> 标签去掉
  const newJS = r1[0].replace('<script>', '').replace('</script>', '')
  // 然后写入到 index.js 文件中
  fs.writeFile(path.join(__dirname, './clock/index.js'), newJS, err => {
    if(err) {
      return console.log(err.message)
    }
    console.log('写入 JS 脚本成功!');
  })
}
```



> 3. **步骤5 - 自定义 resolveHTML 方法**

```js
function resolveHTML(htmlStr) {
  // 将内嵌的 <style>和<script> 标签，替换为外联的 <link>和<script> 标签
  const newHTML = htmlStr
  .replace(regStyle, '<link rel="stylesheet" href="index.css">')
  .replace(regScript, '<script src="index.js"></script>')
  // 然后写入到 index.html 文件中
  fs.writeFile(path.join(__dirname, './clock/index.html'), newHTML, err => {
    if(err) {
      return console.log(err.message);
    }
    console.log('写入 HTMl 页面成功!');
  })
}
```



> 4. **案例的==两个注意点==**

1. fs.writeFile() 方法只能用来创建文件，不能用来创建路径
2. 重复调用 fs.writeFile() 写入同一个文件，新写入的内容会覆盖之前的旧内容





### 4. http 模块

#### 4.1 什么是 http 模块

回顾：什么是==客户端==、什么是==服务器==？

在网络节点中，负责消费资源的电脑，叫做客户端；==负责对外提供网络资源==的电脑，叫做服务器。



==http 模块==是 Node.js 官方提供的、用来==创建 Web 服务器==的模块。通过 http 模块提供的==http.createServer()==方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。



如果需要使用 http 模块创建 Web 服务器，则需要先导入它：

```js
const http = require('http')
```



#### 4.2 进一步理解 http 模块的作用

服务器和普通电脑的==区别==在于，服务器上安装了==web 服务器软件==，例如：IIS、==Apache==等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。



在 Node.js 中，我们==不需要使用==IIS、Apache 等这些==第三方 web 服务器软件== 。因为我们可以基于 Node.js 提供的 http 模块，==通过几行简单的代码，就能轻松的手写一个服务器软件==，从而对外提供 web 服务。



#### 4.3 服务器相关的概念

> 1. **IP 地址**

==IP 地址==就是互联网上==每台计算机的唯一地址==，因此 IP 地址具有唯一性。只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。

 

IP 地址的格式：通常用 “==点分十进制==” 表示成 (a.b.c.d) 的形式，其中，a,b,c,d 都是 0~255  之间的十进制整数。例如：用点分十进表示的 IP 地址 (192.168.1.1)



注意：

1. ==互联网中每台 Web 服务器，都有自己的 IP 地址==，例如：在 Windows 的终端中 ==ping== www.baidu.com 命令，即可查看到百度服务器的 IP 地址。

2. 在开放期间，自己的电脑既是一台服务器，也是一台客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。



> 2. **==域名==和==域名服务器==**

尽管 IP 地址能够唯一的标记网络上的计算机，但 IP 地址是一长串数字，==不直观==，而且==不便于记忆==，于是人们发明了另一套字符型的地址方案，即所谓的==域名 (Domain Name) 地址==。

 

==IP 地址==和==域名==是==一一对应的关系==，这份对应关系存放子啊一种叫做==域名服务器==(DNS,Domain name server) 的电脑中。使用者只需要通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，==域名服务器就是提供 IP 地址和域名之间的转换服务器的服务器==。



注意：

1. 单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。
2. 在开发测试期间，==127.0.0.1==对应的域名是==localhost==，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。



> 3. **端口号**

计算机中的端口号，就好像是实现生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中。

同样的道理，在一台电脑中，可以运行成百上千个 web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给==对应的 web 服务==进行处理。

注意：

1. 每个端口号不能同时被多个 web 服务占用。
2. 在实际应用中，URL 中的 ==80 端口可以被省略==。



#### 4.4 创建最基本的 web 服务器

> 1. **创建 web 服务器的基本步骤**

1. 导入 http 模块
2. 创建 web 服务器实例
3. 为服务器实例绑定 ==request==事件，==监听客户端的请求==
4. 启动服务器



> 2. **步骤1 - 导入 http 模块**

```js
const http = require('http')
```

> 2. **步骤2 - 创建 web 服务器实例**

调用==http.createServer()==方法，即可快速创建一个 web 服务器实例：

```js
const server = http.createServer()
```

> 2. **步骤3 - 为服务器实例绑定 request 事件**

为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求：

```js
// 使用服务器实例的 .on() 方法，为服务器绑定一个 request 事件
server.on('request', (req, res) => {
  // 只要有客户端来请求我们自己的服务器，就会触发 request 事件，从而调用这个事件处理函数
  console.log('Someone visit our web server.')
})
```

> 2. **步骤4 - 启动服务器**

调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例：

```js
// 调用 server.listen(端口号, cd回调) 方法，即可启动 web 服务器
server.listen(80, () => {
  console.log('http server running at http://127.0.0.1')
})
```



> 3. **==req==请求对象**

只要服务器接收到了客户端的请求，就会调用通过==server.on()== 为服务器绑定的==request 事件处理函数==。
如果想在事件处理函数中，==访问与客户端相关的数据或属性==，可以使用如下的方式：

```js
server.on('request', (req) => {
  // req 是响应对象，它包含了与服务器相关的数据和属性，例如：
  // req.url 是客户端请求的 URL 地址
  // req.method 是客户端请求的 method 类型
  const str = `You request url is ${req.url}, and request method is ${req.method}`
  console.log(str)
})
```



> 4. **==res==响应对象**

在服务器的 request 事件处理函数中，如果想==访问与服务器相关的数据或属性==，可以使用如下的方式：

```js
server.on('request', (req, res) => {
  // res 是响应对象，它包含了与服务器相关的数据和属性，例如：
  // 要发送到客户端的字符串
  const str = `You request url is ${req.url}, and request method is ${req.method}`
  // res.end() 方法的作用：
  // 向客户端发起指定的内容，并结束这次请求的处理过程
  res.end(str)
})
```



> 5. **解决==中文乱码==问题**

当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码，此时，需要手动==设置内容的编码格式==：

```js
server.on('request', (req, res) => {
	// 发送的内容包含中文
	const str = `您请求的 url 地址是 ${url}, 请求的 method 类型是 ${req.method}`
	// 为防止中文显示乱码的问题，需要设置响应头 Content-Type 的值为 text/html; charset=utf-8 
	res.setHeader('Content-Type', 'text/html; charset=utf-8')
	// 把包含中文的内容，响应给客户端
	res.end(str)
})
```





#### 4.5 根据不同的 url 响应不同的 html 内容

> 1. **核心实现步骤**

1. 获取==请求的 url 地址==
2. 设置==默认的响应内容==为 404 Not found
3. 判断用户请求的是否为 ==/== 或 ==/index.html== 首页
4. 判断用户请求的是否为 ==/about.html== 关于页面
5. 设置 ==Content-Type 响应头== ，防止中文乱码
6. 使用 ==res.end()== 把内容响应给客户端'



> 2. **动态响应内容**

```js
server.on('request', (req, res) => {
  // 1. 获取请求的 url 地址
	const url = req.url
  // 2. 设置默认的响应内容为 404 Not found
	let content = '<h1>404 Not found!</h1>'
  // 3. 判断用户请求的是否为 / 或 /index.html 首页
	if(url === '/' || url === '/index.html') {
    content = '<h1>首页</h1>'
  } else if (url === '/about.html') {
    // 4. 判断用户请求的是否为 /about.html 关于页面
    content = '<h1>关于页面</h1>'
  }
  // 5. 设置 Content-Type 响应头，防止中文乱码
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // 6. 使用 res.end() 把内容响应给客户端
  res.end(content)
})
```



#### 4.6 案例 - 实现 clock 时钟的 web 服务器

> 1. **核心思路**

把文件的==实际存放路径==，==作为==每个资源的==请求 url 地址==。

![](D:\desktop\learning\Node.js\img\实现web的思路.png)



> 2. **实现步骤**

1. 导入需要的模块
2. 创建基本的 web 服务器
3. 将资源的请求 url 地址映射为文件的存放路径
4. 读取文件内容并响应给客户端
5. 优化资源的请求路径



> 3. **步骤1 - 导入需要的模块**

```js
// 1.1 导入 http 模块
const http = require('http')
// 1.2 导入 fs 文件系统模块
const fs = require('fs')
//  1.3 导入 path 路径处理模块
const path = require('path')
```

> 3. **步骤2 - 创建基本的 web 服务器**

```js
// 2.1 创建 web 服务器
const server = http.createServer()

// 2.2 监听 web 服务器 request 事件
server.on('request', function() => {})

// 2.3 启动 web 服务器
server.listen('80', function() {
  console.log('server listen at http://127.0.0.1')
})
```

> 3. **步骤3 - 将资源的请求 url 地址映射为文件的存放路径**

```js
// 3.1 获取到客户端请求的 url 地址
const url = req.url
// 3.2 把请求的 url 地址，映射为本地文件的存放路径
const fpath = path.join(__dirname, url)
```

> 3. **步骤4 - 读取文件的内容并响应给客户端**

```js
// 4.1 根据 “映射” 过来的文件路径读取文件
fs.readFile(fpath, 'utf8', (err, dataStr) => {
  // 4.2 读取文件失败后，向客户端响应固定的“错误消息”
  if(err) return res.end('404 Not Fount!')
  // 4.3 读取文件成功后，将“读取成功的内容”响应给客户端
  res.end(dataStr)
})
```

> 3. **步骤5 - 优化资源的请求路径**

```js
// *** 将 3.2 的实现方式，改为如下代码 ↓↓↓ ***
// 5.1 预定义空白的文件存放路径
let fpath = ''
if (url === '/') {
  // 5.2 如果请求的路径是否为 /, 则手动指定文件的存放路径
  fpath = path.join(__dirname, './clock/index.html')
} else {
  // 5.3 如果请求的路径不为 /, 则动态拼接文件的存放路劲
  fpath = path.join(__dirname, './clock/', url)
}
```



