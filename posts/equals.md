<!-- # 终极等于 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/equals/poster.png)

## 简介

> 👉 [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday) 👈

> 科学家发现，人脑中会分泌多种能让人感到快乐、安全和成就感的物质，这些物质统称为“快乐素”。通常情况下，快乐素的释放水平很低，维持我们心情平静。只有当我们完成了预设目标，作为奖励，大脑才会增加快乐素的分泌，让人感受到满足和成功的喜悦。

这是之前看到的一篇关于 `大脑奖励机制` 文章的一段话，为了要获得奖励我们需要有预设目标，而是每日 30 秒系列也是为了帮助大家设立一个目标，每日完成一小段代码的学习来实现 `对学习上瘾`。

到了周末发现大家相比起工作日的学习欲望下降得较快，昨天又刚好更新了一个需要花费时间且值得阅读的 [每日 30 秒之 巧用可视区域](https://pushmetop.github.io/blog/element-is-visible-in-viewport-for-30-seconds) 希望大家有时间可以看看。那今天学习一段比较简单和常用的代码片段来奖励一下大脑 🧠。

在开发中我们最最最最经常用到的一个功能就是 `等于`，在 JavaScript 中拥有 `===（全等于）` 和 `==（等于）`再加上 JavaScript 是弱类型直接使用 `==` 会被解释器所转换，转换的规则浮渣且难以记忆这也是各种 `==` 相关文章层出不穷的原因。在 `《JavaScript 语言精粹》`中 `==` 被归类到了糟粕附录中且建议我们请始终使用 `===` 和 `!==`，更加规范的开发也有利于 BUG 的减少这也是 TypeScript 语言出现的原因之一。

<!-- more -->

但是 `===` 和 `!==` 也不是万能的当遇上 `Object` 和 `Array` 时就会吃瘪了，因为它们虽然数据一样但是对应这地址不一样这点在开发过程中要小心。爱思考的同学肯定不甘心于小心和谨防掉入坑中，那让我们一起写一个 `终极等于`：

```javascript
// 该源码来自于 https://30secondsofcode.org 有所修改
const equals = (a, b) => {
  if (a === b) return true;
  if (a instanceof Date && b instanceof Date) return a.getTime() === b.getTime();
  if (!a || !b || (typeof a !== 'object' && typeof b !== 'object')) return a === b;
  if (a.prototype !== b.prototype) return false;
  if (Array.isArray(a) && Array.isArray(b)) (a.sort(), b.sort());

  let keys = Object.keys(a);
  if (keys.length !== Object.keys(b).length) return false;
  return keys.every(k => equals(a[k], b[k]));
};
```

## 代码分析
 
首当其冲当然是利用 `===` 来完成最基础判断：

```javascript
if (a === b) return true;
```

当传入 `Date` 对象是先对两者类型进行判断，再利用 `Date.prototype.getTime()` 来比较对应的时间是否相等：

```javascript
if (a instanceof Date && b instanceof Date) return a.getTime() === b.getTime();
```

当 a 和 b 为 null 或者 undefinded 等非正值时对两者进行比较并过滤掉对象类型，这里也包含了在 a === b 遗留下来不相等值：

```javascript
if (!a || !b || (typeof a !== 'object' && typeof b !== 'object')) return a === b;
```

由于剩下来的便是 `Object` 和 `Array` 类型的数据且 `Array` 算是特殊的 `Object` 需要进行递归遍历数据，可以利用`原型链`来减少递归层数：

```javascript
if (a.prototype !== b.prototype) return false;
```

如果两个值都是数组则对他们进行排序，不然由于 `Array` 是特殊的 `Object` 被当做 Object 遍历时会因为顺序问题而出现判断错误：

```javascript
if (Array.isArray(a) && Array.isArray(b)) (a.sort(), b.sort());
```

如果两个值相等那他们的键值肯定也相等，这里对 `length` 的判断可以直接先验证长度是否一致。

```javascript
let keys = Object.keys(a);
if (keys.length !== Object.keys(b).length) return false;
return keys.every(k => equals(a[k], b[k]));
```

最后只需要利用其中一个的键值数组 和 `every` 来进行遍历全等判断，更多相关的用法可以看 [每日 30 秒之 数组所有数据是否满足某条件](https://pushmetop.github.io/blog/all-for-30-seconds-of-code/) 这篇文章。

```javascript
return keys.every(k => equals(a[k], b[k]));
```

> 小扩展：为什么不直接判断他们的长度是否相等呢?

有的眼尖的同学肯定发现了这个问题，这就不得不提一个很经典的例子：

```javascript
var myObject = new Object();
myObject["firstname"] = "Gareth";
myObject["lastname"] = "Simpson";
myObject["age"] = 21;

console.log(myObject.length); // 输出 undefined
```

当出现这种情况的时候我们可以利用 `Object.prototype.size()` 或者 `Object.keys(obj).length` 来获取它的长度。

#### 使用场景

这里就简单举几个例子：

```javascript
equals(null, null)  // 输出 true
equals(null, undefined) // 输出 false
equals([1, 2, 3], [3, 2, 1]); // 输出 true
equals([1, 2, 3], [1, 2, 3]); // 输出 true
equals({ i: 'love u' }, { i: 'love u' }); // 输出 true
```

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)