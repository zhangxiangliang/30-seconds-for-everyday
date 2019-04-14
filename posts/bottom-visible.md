<!-- # 判断是否为页面底部 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/bottom-visible/poster.png)

## 简介

> 分页、优化、可视区域、无限加载

写前端页面时最经常遇到的开发需求之一就是 渲染后端数据返回的数据对象，当数据对象数量极多的时候便需要进行分页。

常见的分页方式有三种：

1. 在页面底部生成 `上一页`、`下一页`、`页面列表` 按钮。
    * 用户可以很直接的选择自己需要浏览的页面。
    * 不需要担心页面数据过多造成的卡顿。
    * 比起 `自动加载更多数据` 略显不智能。
2. 在页面底部生成 `加载更多数据` 按钮。
    * 相对于页面底部生成分页相关按钮体验好一点
    * 用户可以控制自己是否需要加载更多数据。
    * 比起 `自动加载更多数据` 略显不智能。
    * 需要注意页面数据过多造成的卡顿。
3. 当用户滚动到页面底部时 `自动加载更多数据`。
    * 更符合用户直觉体验很好。
    * 需要注意页面数据过多造成的卡顿。
    * ​用户需要翻遍数据才能看到页脚。

<!-- more -->

当然分页没有绝对的银弹得根据不同的情况进行略微的调整和交叉搭配使用分页方式。例如：页面页脚有需要用户查看的数据时，可以使用 `自动加载更多数据`，当加载二到三页时提示 `加载更多数据` 按钮，使得特定用户可以较为方便的看到页脚内容更多的情景就不一一列举了。

页面数据过多造成的卡顿可以参考 [每日 30 秒之 chunk](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/chunk.md) 中给出的情景案例，利用 `数据分组显示` 来减少 DOM 节点进而优化页面卡顿,这里不讨论分页及其相关的优化。

今天分享的代码是分页过程中会用到的一个函数 `判断是否到达了页面底部`：

```javascript
// 该源码来自于 https://30secondsofcode.org
const bottomVisible = () =>
  document.documentElement.clientHeight + window.scrollY >=
  (document.documentElement.scrollHeight || document.documentElement.clientHeight);
```

## 代码分析

`窗口可见区域的高度` 和 `窗口已经滚动的距离高度` 得到当前页面所处的位置：

```javascript
document.documentElement.clientHeight + window.scrollY
```

再与 `整个页面的高度` 作比较来判断是否已经到达了页面底部，如果 `整个页面的高度` 不存在则使用 `窗口可见区域的高度` 做代替：

```javascript
... >= (document.documentElement.scrollHeight || document.documentElement.clientHeight)
```

> 小技巧：利用 `||` 技巧来初始化数据

## 使用场景

做一个无限加载数据项的分页功能，当页面到达底部时进行数据加载。

```javascript

// 监听页面滚动
document.addEventListener('scroll', () => {
    // 如果到达页面底部
    if(bottomVisible()) {
        // 1.发送网络请求获取数据
        // 2.插入数据到页面
    }
});
```

## 相似代码

判断是否到达了页面顶部

```javascript
const topVisible = () => window.scrollY == 0
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)