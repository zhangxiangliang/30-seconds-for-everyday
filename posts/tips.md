<!-- # 优雅三连击 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/tips/poster.png)

## 简介

> 短路运算、逗号运算、简化条件语句、初始化小技巧

昨天一个同学在 [URL 大爆炸](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/url.md) 问了我一个问题：这是什么写法 `(data[key] = value, data) `。平时在写文章的时候会把这些技巧稍微提示一下，认为大家都知道这些技巧，引起了小二的自我反省。

> 希望大家可以一起成长，都不掉队。

可能很多人都了解这些方法了,如果懂的同学就`温故知新`，不懂的同学咱们`迎头追上`。由于是个人常用技巧可能并不是最好的，如果有知道的同学也可以提出来`一起成长`。

## 短路运算

只有当第一个运算数的值无法确定逻辑运算的结果时，会按照顺序对剩下运算数进行求值。一起回忆初中常背的一句口诀：`一真即真,一假即假`。

### 一真即真

`一真即真` 指的是 `||` 或运算符，当一个值为真并停止对后面的判断。

#### 默认值

```javascript
function test(name) {
    name = name || 'Bar' ;
    console.log(name)
}

// 输出 Bar
console.log(test());
```

当然也可以用 ES6 的 `spread` 语法来完成默认值，关于更多函数参数技巧可以查看 [函数骚操作](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/function-params.md)。不支持 ES6 时等需要默认值操作时，`||`一个值得使用的小技巧。
#### 简化条件语句

在开发是时候，偶尔会遇到只有一行代码的条件语句：

```javascript
if(!name) {
    initName()
}
```

不知道同学会不会和我一样会觉得这样写不好看，这里可以利用 `||` 来简化代码：

```javascript
name || initName()
```

### 一假即假

`一假即假` 指的是 `&&` 或运算符，当一个值为假时则会停止判断，为真时则会一直判断下去。

#### 默认值

在取一些对象属性的时候，对象属性有可能为 `null` 或者 `undefind` 则会出现错误：

```javascript
const data = {
    name: 'xiaoer',
    age: 18,
    company: null
}

// 抛出错误: Uncaught TypeError: Cannot read property 'name' of null
console.log(data.company.name)
```

在这里 `&&` 搭配 `||` 使用可以写出更实用的默认值操作：

```javascript
const data = {
    name: 'xiaoer',
    age: 18,
    company: null
}

const name = data.company && data.company.name || 'no name';
```

#### 简化条件语句

在开发是时候，偶尔会遇到只有一行代码的条件语句：

```javascript
// 假设后端返回的用户数据为 data
const data = {
    name: 'xiaoer',
    age: 18,
    company: null
}

if (data.company && data.company.name) {
    initCompany();
}
```

`&&` 和 `||` 一样也可以用来简化条件语句：

```javascript
data.company && data.company.name && initCompany();
```

## 逗号运算符

### for 循环

在使用 for 循环的时候，可能不止需要迭代一个参数，可以利用逗号表达式：

##### 脚本

```javascript
let i = 0, j = 0, times = 5;

for (let i = 0, j = 0; i < times; i++, j++, j++){
    console.log(i, j);
}
```

##### 输出

```
i:0, j:0
i:1, j:2
i:2, j:4
i:3, j:6
i:4, j:8
```

### 语句赋值

有时候会需要一次声明多个变量：

```javascript
const a = 0,
    b = 1,
    c = 2;

// 输出 a, b, c
console.log(a, b, c);

// 下面操作都会报错
// 证明确实都是 const 常量
a = 2;
b = 1;
c = 1;
```

### 简化语句

在写一些简短的函数时常常写成下面这样：

```javascript
const ins = (x) => {
    x++;
    return x;
}

[{count: 1}].map((x) => {
    x.count++;
    return x;
})
```

如果需要进行的操作很多倒是需要写得详细方便他人阅读，而且开发并不是一个人。如果是这种一点点操作的时候，可以利用逗号运算符来简化：

```javascript
const ins = (x) => (x++, x)

[{count: 1}].map((x) => (x.count++, x));
```

### 交换数据

在不增加变量的情况下如何调换a和b的值。

```javascript
let a = 1, b = 2;
a=[b, b=a][0]
```

当然也可以用 es6 的 `spread` 新语法做到：

```
let a = 1, b = 2;
[a, b]=[b, a]
```

> 这里谢谢 [徐永飞](https://juejin.im/user/5abf0365518825556534a140) 和  [老贼同学](https://juejin.im/user/5c00ce116fb9a049ee802de9) 的补充。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)