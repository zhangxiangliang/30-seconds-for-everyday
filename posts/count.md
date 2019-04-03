<!-- # 统计数组项目 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/count/poster.png)

## 简介

> 👉 [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday) 👈

根据指定的方法或者参数对数组中的项目进行统计。

```javascript
// 该源码来自于 https://30secondsofcode.org
const countBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val) => {
    acc[val] = (acc[val] || 0) + 1;
    return acc;
  }, {});
```

<!--more-->

## 代码分析

函数通过 `Array.prototype.map` 来对数据进行`清洗`，其中利用到 `typeof` 来判断是否为函数，否则使用 `(val) => val[fn]` 来读取属性，这个函数在编程中用到的频率挺高的。最后使用 reduce 来对数据进行归集，并返回统计好的数据。

## 使用场景

统计学生成绩的分布可以传入score属性，函数则会返回由成绩组成的统计对象。统计用户花费区间可以传入一个区间判断函数来获得对应的统计对象。

```javascript
const students = [
    { name: 'xiaoer', score: 80 },
    { name: 'xiaosi', score: 90 },
    { name: 'menty', score: 50 },
]

const scoreStat = countBy(students, 'score')

const users = [
    { name: 'xiaoer', cost: 17000 },
    { name: 'xiaosi', cost: 8000 },
    { name: 'menty', cost: 3000 },
]

const costStat = countBy(users, i => {
    return i.cost > 10000
        ? 'high'
        : (i.cost > 5000 ? 'mid' : 'low')
})
```
## 相似代码

判断一个数组中某个数据项出现的次数。

```javascript
// 该源码来自于 https://30secondsofcode.org
const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0)
```

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)