### 元数据块

@name  脚本名称

```
// @name Hello world!
```

@namespace  命名空间 可以是任意一个字符串

```
// @namespace   http://tampermonkey.net/
```

// @version   脚本的版本号

```
// @version    0.1
```

// @description  脚本的简要介绍，可多次定义

```
// @description  try to take over the world!
```

// @author  作者

```
// @author    Cicada
```

// @match  定义执行脚本的网站 可多次定义

```
// @match     *://*.tk/*
// @match     https://www.bilibili.com/video/BV15b4y1x7oJ?spm_id_from=333.1007.top_right_bar_window_history.content.click
```

// @icon     脚本的图标，后面写图标的url

```
// @icon   https://www.google.com/s2/favicons?sz=64&domain=bilibili.com
```

// @grant     none  指定一些特殊API

```
// @grant GM_getValue
// @grant GM_setValue
```

// @require  引入其他脚本到此脚本

```
// @require      file:///C:/Users/XianYu/goodscrawler/pdd-auto/pdd-auto.js
```

// @run-at  脚本的执行时间

```
// @run-at       document-start 
```

* `document-end`：`DOMContentLoaded`开始时
* `document-start`：尽早执行脚本
* `document-idle`：`DOMContentLoaded`结束后







