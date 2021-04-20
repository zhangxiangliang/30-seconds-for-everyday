<!-- # 数组也会秃顶 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/sparse-array/poster.png)

## 简介

> 稀疏数组、数组性能、密集数组、遍历

你可能很难相信除了程序员会秃顶，数组也会秃顶。什么你不相信我？那我证明给你看：

```javascript
let arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

delete arr[2]

// 输出 [0, 1, empty, 3, 4, 5, 6, 7, 8, 9]
console.log(arr)

// 输出 0 1 3 4 5 6 7 8 9
arr.forEach(i => console.log(i))
```

当 `拔掉(delete)` arr 的第 3 根 `头发(arr[2])` 时，直接硬生生的出现了一个 `空毛囊(empty)`，这难道不是数组秃顶了嘛？`数(forEach)` 一下头发，确实没有把空毛囊算进去，这下你相信了把数组也会秃顶，那不如让我们好好研究研究？

## 班级点名

上学时最常见的一个场景便是老师点名，按着学号`连续的`读出学生的名字并在`记录本`上打上勾，速度是相当的快。反过来随机叫一个学生的名字并在`记录本`上，需要在记录本上找到这个名字并打上勾，速度是相当慢的。

在上面两个场景中一个使用了 `索引` 而另外一个使用了 `hash`，而在 Array 中也存在类似的现象。

在 Array 若是执行了连续数组操作如 `Array.prototype.pop()`、`Array.prototype.unshift()` 来操作数组，由于整个空间都是 `连续的` 使用索引直接定位，遍历起来非常快，这种 Array 叫做 `密集数组`。

而 Array 若是执行了非连续数组操作如 `delete arr[2]`、赋值超出当前数组长度、赋值为非连续索引 来操作数组，由于空间的 `连续性` 被破坏了，只能通过 hash 定位，遍历起来就会变慢。这种 Array 叫做 `稀疏数组`，你可以理解为它被对象化了使得更像是一个 Object。

`稀疏数组`通常在实现上比`密集数组`更慢更耗内存，在这样的数组中查找元素变得跟常规对象的查找一样失去了性能的优势。所以我们在使用 Array 要尽量避免破坏它的连续性，尽量使用数组相关的方法来操作它。

## 在控制台查看

其实在控制台中可以非常明显的看出`密集数组`和`稀疏数组`的索引是否连续：

![对比](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/sparse-array/compare.png)

## 稀疏数组转换密集数组

##### 利用 `Array.prototype.apply`

```javascript
// 进行一下破坏连续性的操作
let arr = [1, ,3, 4];
delete arr[3];
arr['a'] = 5;

// 输出 [1, empty, 3, empty, a: 5]
console.log(arr);

// 进行转换
arr = Array.apply(null, arr);

// 输出 [1, undefined, 3, undefined]
console.log(arr);
```

##### 利用 `Array.prototype.from`

```javascript
// 进行一下破坏连续性的操作
let arr = [1, ,3, 4];
delete arr[3];
arr['a'] = 5;

// 输出 [1, empty, 3, empty, a: 5]
console.log(arr);

// 进行转换
arr = Array.from(arr);

// 输出 [1, undefined, 3, undefined]
console.log(arr);
```

##### 利用 spread 运算符

```javascript
// 进行一下破坏连续性的操作
let arr = [1, ,3, 4];
delete arr[3];
arr['a'] = 5;

// 输出 [1, empty, 3, empty, a: 5]
console.log(arr);

// 进行转换
arr = [...arr];

// 输出 [1, undefined, 3, undefined]
console.log(arr);
```

##### 注意 `new Array`

要注意 `new Array` 只是会生成一个指针指向连续的空间，此时它也是非连续的：

```javascript
let arr = new Array(4);

// 输出 [empty × 4]
console.log(arr);
```

## 传入空参数

##### 利用 null, undefined 调用函数

在调用函数的时候有时候，我们需要跳过一些参数可以使用 `null` 和 `undefined` 来实现：

```javascript
method('a', null, 'c');
method('a', undefined, 'c');
```

当然也可以利用稀疏数组：

```javascript
method(...['a',, 'c']);
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)