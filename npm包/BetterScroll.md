### BetterScroll

#### 基础用法

```js
// 引入
import BScroll from 'better-scroll'

// 在vue中使用
this.scroll = new BScroll(document.querySelector('.wrapper'), {
  
})

// 在原生js中使用
const BScroll = new BScroll(document.querySelector('.wrapper'), {
  
})
```



#### 常用方法

```js
// probeType 有3个可选参数 
// 0 为默认值不侦测； 1 不侦测； 2 只侦测手指滚动 不侦测惯性滚动；3 滚动都侦测
const BScroll = new BScroll(document.querySelector('.wrapper'), {
  probeType: 2, // 实时监听滚动
  click: true, // 开启可触发点击事件
  pullUpLoad: true, // 上拉加载更多
})

// 实时监听滚动
BScroll.on('scroll', (position) => {
  console.log(position)
})

// 上拉加载更多
BScroll.on('pullingUp', () => {
  console.log('上拉加载更多')
  
	setTimeout(() => {
    BScroll.finishPullUp() // 结束上拉加载行为
  }, 2000)
})
// 注意：每次触发 pullingUp 钩子后，你应该主动调用 finishPullUp() 告诉 BetterScroll 准备好下一次的 pullingUp 钩子。

// 返回顶部
// scrollTo 可传入三个参数 第一个x轴 第二个y轴 第三个过渡时间(毫秒)
BScroll.scrollTo(x, y, time)
```

