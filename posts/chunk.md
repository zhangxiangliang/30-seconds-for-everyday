# 海量数据切割

## 简介

> [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday)

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/chunk/poster.png)

把数组按指定大小进行分组，可以用于分页、数据切割、异步操作数据。

```javascript
// 该源码来自于 https://30secondsofcode.org
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
```

<!--more-->

## 代码分析

`Array.prototype.from` 从一个类似数组或者可迭代对象中创建一个新的数组实例，`类似数组` 这个词可能很多人都不是很清楚，类似数组是 `javascript` 中一个神奇的对象，只要拥有 `length` 就算是类似数组了。

最常见的`类似数组`是函数中的 `arguments` 有长度和 arguments[0] 的调用方法，但是却没有数组的 push 等函数方法。利用 `Array.prototype.from` 则可以把 `类似数组` 转化为 `数组`。这个代码的巧妙之处在于用了 `{ length: 3 }` 这样的对象来快速 `生成数组`，而 `Array.prototype.from` 的第二个参数会对刚生成的数组进行循环遍历相当于调用了 `map`。

在循环遍历新生成`数组`时，使用了 `Array.prototype.slice` 的方法来实现了分割数据的效果，这个方法相当常用同学们可以记住它。

## 使用场景

假设现在有一个消息列表数组里面有一万条数据让你渲染到页面上，大部分人会直接遍历数组并拼接成 `dom` 一股脑的渲染到页面上，这样带来的后果是大量的 dom 操作会花费很多时间导致页面卡顿，且上下滑动页面时也会卡顿。

我们不妨换个角度来看这个问题`无论是手机屏幕还是电脑屏幕`用户可见的页面数据条目可能就十几条。那为什么我们要一次性渲染一万多条，而且用户也不见得会把所有数据都查看了。

那我们是否可以只渲染`十几条数据`，其他数据等用户滚动了某个高度时再进行下一个`十几条数据`的渲染。在分页操作中，`chunk` 就可以帮助我们快速的进行分页。

##### 样式
```css
.news > div {
    text-align: center;
    height: 50px;
}
```

##### 结构
```html
<!-- 用于标识到页面顶部了 -->
<div class="news-header"></div>
<!-- 新闻数据 -->
<div class="news"></div>
<!-- 用于标识到页面底部了 -->
<div class="news-footer"></div>
```

##### 脚本
```javascript
// 模拟生成 1万条数据，这里就利用了 Array.from 来快速生成数据
const originNews = Array.from(
    { length: 10000 },
    (v, k) => ({ content: `新闻${k}` })
)

// 需要插入的容器
const element = document.querySelector('.news')[0]

// 创建视图监听
const loadObserver = new IntersectionObserver((entries) => {
    // 如果不可见，就返回
    if (entries[0].intersectionRatio <= 0) {
        return;
    }

    // 判断是否有上一页和下一页
    const hasPrePage = page != 0
    const hasNextPage = page != news.length - 1

    const now = news[page]
    const pre = hasPrePage ? news[page - 1] : []
    const next = hasNextPage ? news[page + 1] : []

    // 传递锚点的坐标 和 当前页面显示的数据
    render(pre.length, [ ...pre, ...now, ...next ])
    
    // 判断是否需要翻页，且防止数组越界
    page = entries[0].target.className == 'news-footer' || page === 0
        ? (hasNextPage ? page + 1 : page)
        : (hasPrePage ? page - 1 : page)
}, { threshold: [1] })

// 设置监听
loadObserver.observe(document.querySelector('.news-header'))
loadObserver.observe(document.querySelector('.news-footer'))

// 根据当前页面高度和新闻高度算出每一页可以放几条数据
let pageNum = Math.ceil(document.body.clientHeight / 50)
let page = 0 // 当前显示了第几页的数据
let news = chunk(originNews, pageNum) // 分页后的数据

// 渲染新闻 并 跳转到锚点
function render(last, data) {
    element.innerHTML = ''

    data.forEach((i, v) => element.innerHTML += v == last
        ? `<div id="news-herf">${i.content}</div>`
        : `<div>${i.content}</div>`
    )

    window.location.href = "#news-herf"
}

```

## 打赏&联系

如果您感觉有收获，欢迎给我打赏，以激励我输出更多的优质内容。

![打赏&联系](https://raw.githubusercontent.com/pushmetop/resource/master/donate/donate.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)