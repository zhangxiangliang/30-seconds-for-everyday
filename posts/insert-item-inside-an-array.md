<!-- # 优雅插入数组 -->

![封面](../images/insert-item-inside-an-array/poster.png)

## 简介

> 数组、插入数组、性能、可读性

> 代码能运行起来就行了为什么要编写优雅的代码？

其实很多时候项目进度很赶、小姐姐不理你了、老板不给你加薪等等事情都会成为你今天偷偷把代码写那么不好一点的理由，根据`破窗效应`这样带来的结果可能会不好。

写出优雅的代码会使得你的小伙伴对你 BUG `仇恨值降低`，写出优雅的代码会使得小伙伴哎呀一声惊叹让你`心情大好`，写出优雅的代码会让自己陷入陶醉感叹自己的 `学识渊博`，写出优雅的代码可以留以后人观瞻`名留青史`，写出优雅的代码可以让自己变得更加 `优秀`。

回归正题把 `数据` 插入到 `数组` 中是开发中最经常遇到的场景，也是简单且容易改变的写法习惯，让我们一起学习怎么把它写得更加优雅且易读。

## 把数据插入数组尾部

##### 利用数组长度进行赋值

```javascript
let arr = [1,2,3,4,5];
arr[arr.length] = 6;
```

##### 利用 Array.prototype.push 方法

```javascript
let arr = [1, 2, 3, 4, 5];
arr.push(6);
```

##### 利用 Array.prototype.concat 方法

```javascript
let arr = [1, 2, 3, 4, 5];
arr = arr.concat(6);
```

##### 利用 spread 运算符

```javascript
let arr = [1, 2, 3, 4, 5];
arr = [...arr, 6];
```

## 把数据插入数组头部

##### 利用 Array.prototype.unshift 方法

```javascript
let arr = [1,2,3,4,5];
arr.unshift(0);
```

##### 利用 Array.prototype.concat 方法

```javascript
let arr = [1,2,3,4,5];
[0].concat(arr);
```

##### 利用 spread 运算符

```javascript
let arr = [1, 2, 3, 4, 5];
arr = [0, ...arr];
```

## 把数据插入数组指定位置

##### 利用 Array.prototype.splice 方法

```
let items = [1, 2, 4, 5];
items.splice(items.length / 2, 0, 3);
```

## 拼接两个数组

##### 利用 Array.prototype.concat 方法

```javascript
let arr = [1,2,3,4,5];
[-2, -1, 0].concat(arr);
```

##### 利用 spread 运算符

```javascript
let arr = [1,2,3,4,5];
arr = [...[-2, -1, 0], ...arr];
```

> 如果大家还有什么优雅的写法留言评论，也可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 提交。

## 基准测试

* [把数据插入数组尾部](https://jsperf.com/insert-item-inside-an-array-at-the-end)
* [把数据插入数组头部](https://jsperf.com/insert-item-inside-an-array-at-the-head)
* [把数据插入数组指定位置](https://jsperf.com/insert-item-inside-an-array-at-the-merge)

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)