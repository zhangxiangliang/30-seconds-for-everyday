<!-- # 对象数组分组 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/group-by/poster.png)

## 简介

> 数组、对象、分组、map、reduce

把对象数组进行分组可能是日常开发中最经常使用到的功能了，除了杀鸡用牛刀引入`lodash`外也可以自己实现一个短小精悍的数组分组。

```javascript
// 该源码来自于 https://30secondsofcode.org
const groupBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
    acc[val] = (acc[val] || []).concat(arr[i]);
    return acc;
  }, {});
```

<!--more-->

## 代码分析

先利用 `Array.prototype.map` 来对需要分组的数据进行提取，再使用 `Array.prototype.reduce` 来遍历提取后的数据并做归集。点睛之笔是 `fn` 为函数时可以进行复杂的操作和判断，不为函数时直接从对象属性中读取使得易用和实用性都得到了增强。

> 小技巧：使用 `||` 来进行数据的初始化。

## 使用场景

把用户购买过的物品按照品类进行分组，并生成标签方便用户快速查询对应种类的商品。

```javascript
// 原始数据
const items = [
    { name: 'Apple iPhone X', category: '手机数码' },
    { name: '索尼 NW-A55 音乐播放器', category: '手机数码' },
    { name: '舒克 海洋之风牙膏', category: '日常用品' },
    { name: '洁丽雅 纯棉强吸水毛巾', category: '日常用品' },
]

// 分类后的商品数据
const categoryItems = groupBy(items, 'category')

// 分类种类
const categoryKeys = Object.keys(categoryItems)
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)