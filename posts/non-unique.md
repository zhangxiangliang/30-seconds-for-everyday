<!-- # 非唯一数据集 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/non-unique/poster.png)

## 简介



> 👉 [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday) 👈

取出对象数组中唯一的数据集。

```javascript
// 该源码来自于 https://30secondsofcode.org
const filterNonUniqueBy = (arr, fn) =>
  arr.filter((v, i) => arr.every((x, j) => (i === j) === fn(v, x, i, j)));
```

<!--more-->

## 代码分析

代码使用了 `Array.prototype.filter` 来进行遍历数组并获取过滤，通过 `Array.prototype.every` 和 `fn` 来对数据项进行判断是否重复出现过。

## 使用场景

从后端或者数据库分别获取到参加不同马拉松的用户并对这些用户做归集，通过 `filterNonUniqueBy` 来寻找只参加过一次马拉松的用户。

```javascript
// 查询到参加 2019厦门马拉松的数据
const join2019 = [
    { id: 1, name: 'xiaoer', join: ['2019厦门马拉松', '2018厦门马拉松'] },
    { id: 2, name: 'xiaosi', join: ['2019厦门马拉松'] },
]

// 查询到参加 2018年马拉松的数据
const join2018 = [
    { id: 1, name: 'xiaoer', join: ['2019厦门马拉松', '2018厦门马拉松'] },
    { id: 3, name: 'menty', join: ['2018厦门马拉松'] },
]

// 合并数据
const users = [...join2019, ...join2018]

// 获取只参加过一次的用户
// 输出:
// [
//    {id: 2, name: "xiaosi", sales: 50000},
//    {id: 3, name: "menty", sales: 150000}
// ]
const joinOnce = filterNonUniqueBy(users, (a, b) => a.id === b.id)
```

## 相似代码

取出数组中唯一的数据集。

```javascript
// 该源码来自于 https://30secondsofcode.org
const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i))
```

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)