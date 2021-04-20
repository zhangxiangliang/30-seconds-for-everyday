<!-- # 数据类型大乱炖 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/type/poster.png)

## 简介

> 字符串、数字、布尔值、Null、Undefined、对象、数组、函数、判断方法

JavaScript 中有两种数据类型，分别是基本数据类型和引用数据类型：

| 基本数据类型 | 引用数据类型 |
| --- | --- |
| Number、String、Boolean、Null、Undefined、Symbol | Object、Array、Function |

在开发过程中我们有时候会需要对变量进行类型判断，一般是利用 `typeof` 并搭配相应的`特性` 来完成。

## Number

判断一个变量是不是 `Number` 可以利用 `typeof` 判断是不是 `number` 但是有个小坑就是 `typeof NaN === number`，可以利用 `NaN !== NaN` 的特性来加以判断。

```javascript
const isNumber = val => typeof val === 'number' && val === val;
```

## String

判断 `String` 就很简单了没有那么多弯弯绕绕一个 `typeof` 搞定。

```javascript
const isString = val => typeof val === 'string';
```

## Boolean

`Boolean` 的判断也很简单使用 `typeof`，当然也可以使用 `===` 来进行判断。

```javascript
const isBoolean = val => typeof val === 'boolean';
```

## Null 和 Undefined

> 为什么要把这两个数据类型放在一起讲呢？

在其他编程语言中往往只有 `Null`、`Undefined`、`Nil`中的其中一个，而 JavaScript 却把它们两个都单独进行了定义：

| 名称 | 定义 |
| --- | --- |
| null | 是一个对象，表示无值 |
| undefined | 是一个特殊属性，其值是未定义，表示缺少值 |

由于在 JavaScript 中都有自己定义对应的值直接利用值来判断就可以了：

```javascript
const isNull = val => val === null;
const isUndefined = val => val === undefined;
const isNil = val => val === undefined || val === null;
```

## Symbol

`Symbol` 是 ES6 新引入的数据类型用于表示表示独一无二的值，由于是新引入并没有特别大的坑直接利用 `typeof` 梭它就对了。

```javascript
const isSymbol = val => typeof val === 'symbol';
```

## Object

> Null 也是对象需要进行判断。

`Object` 可以是 `PlainObject` 字面量对象 也可以是由 `new` 操作符生成的对象：

在 JavaScript 中可以利用函数来实现类的功能：

```javascript
function Person (name) {
    this.name = name;
}

var person = new Person('xiaoer')
```

对于这样的类对象 和 字面量对象、类对象类型 我们都可以使用下面方法进行判断，`Object.constructor` 当遇到 Null 和 Undefined 会返回一个空对象，否则则会返回给予的对象。

```javascript
const isObject = obj => obj === Object(obj);
```

而字面量对象则指的是通过 `Object.constructor` 方法创建的对象，当然 `const a = {a: 1}` 这样声明创建的对象其实也是调用了`Object.constructor` 方法，利用 `constructor` 和 `typeof` 则可以进行判断。这里巧妙的利用 `!!` 来进行布尔值的转换来判断是否为 Null 和 Undefined：

```javascript
const isPlainObject = val => !!val && typeof val === 'object' && val.constructor === Object;
```

## Array

`Array` 算是一个特殊的 `Object` 不信你用上面的对象方法判断看看就知道了。

> 那我们这么判断 `Array` 呢？

`ES6` 提供了一个判断数组的方法 `Array.isArray`，但是如果你在使用不支持 `ES6` 的浏览器时需要自己实现一下这个方法了：

```javascript
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

## Function

`Function` 在引用数据类型中算是简单的了，只需要使用 `typeof` 进行判断：

```javascript
const isFunction = val => typeof val === 'function';
```

## JSON

在日常开发中 `JSON` 实在是太经常使用拉，在这里我们也把它当做一种“类型”给出它的判断方法：

```javascript
const isValidJSON = str => {
  try {
    const o = JSON.parse(str)
    return o != null && typeof o === "object"
  } catch (e) {
    return false;
  }
};
```

## 终极奥义

> 内容太多让你无法呼吸了？

没事小二这里还有杀手锏可以提供大家使用：

```javascript
function getType(obj) {
    if(obj && obj.constructor && obj.constructor.name) {
        return obj.constructor.name;
    }
    return Object.prototype.toString.call(obj).replace(/^\[object (.+)\]$/,"$1").toLowerCase();
}
```

需要注意的是 `NaN` 在这里依旧返回的是 'number'，在 [每日 30 秒 ⏱ 终极等号](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/equals.md) 中有同学提问了为什么没有对 `NaN` 进行判断，在日常开发中出现 `NaN` 是一件不好的事情，所以小二就没有把它加到判断中去了，如果有需要可以利用 `isNaN()` 这个方法来进行判断。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)