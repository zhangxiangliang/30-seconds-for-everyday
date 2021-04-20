<!-- # 数组所有数据是否满足某条件 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/all/poster.png)

## 简介

> 数组、every、any

判断一个数组中是否都满足特定的条件，如果满足则返回 `true` 否则返回 `false`。

```javascript
// 该源码来自于 https://30secondsofcode.org
const all = (arr, fn = Boolean) => arr.every(fn)
```

<!--more-->

## 代码分析

`Array.prototype.every(callback[, thisArg])`中`callback` 被调用时传入三个参数：元素值，元素的索引，原数组。`every` 方法为数组中的每个元素执行一次 `callback` 函数，直到它找到一个使 `callback` 返回 false（表示可转换为布尔值 false 的值）的元素。

有的同学会说了，这个 `all` 函数 和 直接使用 `Array.prototype.every` 有什么区别呢？答案就在`fn = Boolean` 这个点睛之笔，总所周知 javascript 中的对象其实是一种`特殊的函数`，利用 Boolean 这个对象可以非常方便对数据进行格式化为 boolean 并返回值。`every` 函数不能在没有 `callback` 时进行调用，这个函数更多的是拓展了 `every`。

## 使用场景

一个简单的微商场景，获得当前用户的所有下级并判断是否所有人都超过 平台规定的最低销售额，如果满足则可以获得特定的奖金奖励。

```javascript
const MIN_SALES = 100000 // 100000 分钱

// 抽取
const disciples = [
    { name: 'xiaoer', sales: 100000 },
    { name: 'xiaosi', sales: 50000 },
    { name: 'menty', sales: 150000 },
]

const canAward = all(disciples, (item, index, origin) => {
    return item.sales > MIN_SALES
})
```

## 相似代码

判断一个数组中是否有一个满足的数据，如果满足则返回 `true` 否则返回 `false`

```javascript
// 该源码来自于 https://30secondsofcode.org
const any = (arr, fn = Boolean) => arr.some(fn)
```

判断一个数组中所有数据是否相等。

```javascript
// 该源码来自于 https://30secondsofcode.org
const allEqual = arr => arr.every(val => val === arr[0])
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)