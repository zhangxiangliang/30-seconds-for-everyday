<!-- # 根据条件将数组分成两个集合 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/bifurcate/poster.png)

## 简介

> 数组、拆分

根据条件将数组分成两个集合。

```javascript
// 该源码来自于 https://30secondsofcode.org
const bifurcateBy = (arr, fn) =>
  arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []])
```

<!--more-->

## 代码分析

这个代码主要是利用了 Array.prototype.reduce 和 Array.prototype.push，一边遍历一边进行归集。其中巧妙之处是一个`逗号表达式`来在对 acc 进行操作后并返回 acc的值。下面举一个简单的例子：

```javascript
let acc = []

let pushed = (acc.push(2), acc)

// 输出 [2]
console.log(pushed)
```

## 使用场景

将及格和不及格成绩的同学进行分组，当然也可以用 `Array.prototype.filter` 直接获得及格和不及格成绩。

```javascript
const CUT_OFF_SCORES = 60
const students = [
    { name: 'xiaoer', score: 80 },
    { name: 'xiaosi', score: 90 },
    { name: 'menty', score: 50 },
]

const group = bifurcateBy(students, (student) => student.score >= CUT_OFF_SCORES)
```

## 相似代码

根据条件数组来对原数组进行分类，例如 `bifurcate(['beep', 'boop'], [true, false])`。

```javascript
// 该源码来自于 https://30secondsofcode.org
const bifurcate = (arr, filter) =>
  arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []])
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)