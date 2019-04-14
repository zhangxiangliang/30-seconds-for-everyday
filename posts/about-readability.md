<!-- # 该不该优雅 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/about-readability/poster.png)

## 简介

> 可读性、性能、Spread、Reduce

在 [优雅三连击](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/tips.md) 中有同学提到了 `可读性` 这个关键词，就小二个人的观点 `在某个范围内使用比较常用到的小技巧，可以提升一定的可读性`，文中提到的短路运算在`初始化变量`是提升可读性的，并且在很多提倡优化`if 语句`的时候，短路运算符也可以起到对简单条件语句的优雅。

```javascript
// 优雅前
if (name == '') {
    name = 'anonymous'
}

// 优雅后
name = name || 'anonymous'
```

毕竟可读性能使得代码方便`理解`，甚至做到不需要`注释`，也包括让人能阅读愉快。但不能`滥用`这些方法来把代码全都`揉成一团`，这个度怎么把握就是一门学问，很多时候与个人习惯和经验都有一定的关系。

> 优雅不是一蹴而就，而是在丑化的代码中慢慢优雅。-- 鲁迅

## Spread

ES6的新语法糖 `spread` 甜得不得了，但是你知道它并不比`Object.assign()` 快吗？

```javascript
const user = { name: 'xiaoer', height: '183' }; 

// ES6 - spread
const useSpread = { age: 18, ...params };

// Object.assign()
const useAssign = Object.assign({}, { age: 18 }, params);
```

这两种方法 `spread` 语法显然更优雅，但是在 [性能基准测试](https://jsperf.com/30-seconds-for-everyday-comparing-object-asign-spread) 中 `Object.assign()` 肉眼可见的快了50%-60%。

![基准测试](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/about-readability/spread-vs-object-assign.png)

## Reduce

`Array.reduce()` 可以和大程度上提升代码的可读性，但是你知道 `loop` 其实更快嘛？

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Array.reduce
numbers.reduce((count, i) => count + i, 0);

// loop
function sum(arr) {
    let count = 0;
    for (let i = 0; i < arr.length; i++) {
        count += arr[i]
    }
    return count;
}

sum(numbers);
```

很显然 `Array.reduce()` 的写法更优雅，但是在 [性能基准测试](https://jsperf.com/30-seconds-for-everyday-for-loop-vs-reduce) 中 `for 循环` 肉眼可见的快了90%。

![基准测试](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/about-readability/loop-vs-array-reduce.png)

## 怎么办

上面两个关于优雅的例子性能对比之下，不知道该不该继续使用`优雅方法`？是不是自己之前写的代码都`糟糕极了`？

其实不必于太过纠结`该不该`，新的 ES6 语法糖很大程度上是为了提升开发体验和功能， 并且一些小技巧可以提升可读性和愉悦感，当遇到海量数据需要考虑优化时选择 `性能`，当其他较为繁琐的代码选择`可读性`，如果你真的很在意这个可以看看这几个建议：

#### 什么时候可读性优先

* 其实现在的硬件性能已经非常快了，处理数据不多很多时候牺牲一点`性能`换取`可读性`是应该的，毕竟开发和维护在很多时候并不是一个人的事情，而是一整个团队几百号人。
* 有的时候项目开发中上级给你分配了好几个新人，出于开发进度和新人的不熟练，可以选择可读性优先，并在后期维护时对性能分析并选取优化性能。
* 编写实例代码或者教程、类库时，考虑到读者的水平不一定都一样时，也可以优先`可读性`在后续文章或者迭代中补充说明。小二在写文章的时候，就是这样把很多`概念`拆开来，使得阅读时只需要`聚焦`一个知识点，并通过`不断更新`来完善其他知识。
* 个人项目那肯定是怎么舒服怎么来，毕竟是要愉悦自己。

#### 什么时候性能优先

* 其实性能优先和可读性优先都是`相对`的。
* 当项目在运行时发现了特别明显的卡顿等性能问题时，就需要优先考虑性能了。
* 在处理`大量数据`时就需要考虑性能了。有的同学会说项目哪里有这么多数据，还真别说小二做过一个非常蛋疼的项目，后端直接返回几万条数据让前端来处理。别说话吻我，我不想回忆这段过去了。
* 更多的取舍应该要出于项目`实际情况`进行选择，有些性能问题是可以`提前预知`的，一定程度的分析需求可以节省很多代码时间。

## 其他

* 关于 `基准测试` 更多操作可以查看 [谁敢与我一战](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/benchmark.md) 。
* 关于 `spread` 更多操作可以查看 [函数参数骚操作](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/function-params.md)。
* 关于基准测试中`快速初始化`测试数组可以查看 [优雅初始化数组](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/init-array.md)。
* 关于`大量数据优化`可以查看 [海量数据切割](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/chunk.md)。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)