<!-- 优雅初始化数组 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/init-array/poster.png)

## 简介

> 数组、初始化、快速生成数组、内存泄露

有时候会需要对数组进行一些初始化，最常用到的便是 for 循环：

```javascript
let num = [];
for (let i = 0; i < 10; i++) {
    // 做一些其他操作
    // 或者返回一些值
    num[i] = i;
}
```

其实有一些简单好用的小技巧可以帮助我们优雅的初始化数组：

## Array.from

在支持 ES6 的时候可以利用 `Array.from()` 来初始化数组：

```javascript
Array.from({ length: 10 }, (val, index) => {
    // 做一些其他操作
    // 或者返回一些值
    return index;
})

Array.from(new Array(10), (val, index)=> {
    // 做一些其他操作
    // 或者返回一些值
    return index;
});
```

## Array.apply

在不支持 ES6 的时候可以利用 `Array.apply()` 来初始化数组：

```javascript
Array.apply(null, {length: 10}).map(Function.call, (index, arr) => {
    // 做一些其他操作
    // 或者返回一些值
    return index;
});

const num = Array.apply(null, {length: 5}).map(Function.call, Number);

// 输出 [0, 1, 2, 3, 4]
console.log(num);
```

## spread

当需要快速创建类似 [0, 1, 2, ...] 这种数组时可以：

```javascript
const num = [...Array(5).keys()];

// 输出 [0, 1, 2, 3, 4]
console.log(num)
```

## Array.fill

利用 new Array 配合 Array.fill 可以快速生成 [0, 0, 0, 0, ...] 这种数组：

```javascript
const num  = (new Array(5)).fill(0)

// 输出: [0, 0, 0, 0, 0]
console.log(num)
```

关于 `new Array` 会产生一个稀疏数组，可以查看 [数组也会秃顶](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/sparse-array.md)

## 清空数组

除了初始化新的数组，对已有的数组进行清空操作也算`半个初始化`。如果直接对变量赋予新值 `list=[]` 虽然说以前清空了数组，但是旧值还放在内存之中，没被垃圾回收机制自动回收的话算是 `内存泄露` 了：

```javascript
let first = [1,2,3];
let second = first;

// 清空
first = [];

// 输出 []
console.log(first);

// 输出 [1, 2, 3]
console.log(second);
```

> 不再用到的内存，没有及时释放，就叫做内存泄漏。

也可以利用 `list.length = 0` 来进行操作可以销毁掉数组里的所有内容，也将影响到其他引用。例子：
```javascript
let first = [1,2,3];
let second = first;

// 清空
first.length = 0;

// 输出 []
console.log(first);

// 输出 []
console.log(second);
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)