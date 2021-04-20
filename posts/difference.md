<!-- # 两个数组中的差集 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/difference/poster.png)

## 简介

> 数组、差集、函数

根据给出的函数找出两个数组中的差集。

```javascript
const differenceBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.filter(el => !s.has(fn(el)));
};
```

## 代码分析

这段代码使用了ES2015中定义的 `Set 对象`。`Set 对象`的值的特点是不含有重复的值，这个特性可以用来实现对一个数组的去重。

有的同学会问了那为啥要在这把 b 转化为 `Set 对象` 呢，直接用 `Array.prototype.indexOf` 不是也可以实现查找数组中的值。实际上 `Set.prototype.has` 方法的效率会比 `Array.prototype.indexOf` 高一点。

`Set 对象` 还有很多有用的方法可以到 [MDN web docs](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#%E6%96%B9%E6%B3%95) 查看。

## 使用场景

找出两个公司职员中工作不同的职员，这里只是简单模拟一个小场景真实开发中往往会经过更多的判断和归集。

```javascript
const superHeroCompany = [
    { name: 'xiaoer', job: '程序员' },
    { name: 'xiaosi', job: '图书管理员', },
    { name: 'menty', job: '会计' },
]

const happyCompany = [
    { name: 'xiaofu', job: '程序员' },
    { name: 'panghu', job: '会计' },
]

const diffUsers = differenceBy(superHeroCompany, happyCompany, v => v.job)
```

## 相似代码

找出两个数组当中的差集，要注意的是对象的值一样并不是两个对象就相等了，而是对象的指向一样时才会相等。

```javascript
// 该源码来自于 https://30secondsofcode.org
const difference = (a, b) => {
  const s = new Set(b);
  return a.filter(x => !s.has(x));
};
```

根据比较函数 comp 的返回值来过滤两个数组中的差集。

```javascript
// 该源码来自于 https://30secondsofcode.org
const differenceWith = (arr, val, comp) => arr.filter(a => val.findIndex(b => comp(a, b)) === -1)
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)