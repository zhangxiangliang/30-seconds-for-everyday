<!-- # 函数参数骚操作 -->

![封面](../images/function-params/poster.png)

## 前言

> 函数、参数、解构、优雅、可读性、技巧

不管是调用第三方库或者是项目自身的函数，开发过程中总少不了函数。可以说函数是解放代码的第一生产力，有的同学会说了那你把类放在那里了。其实用函数和数据一样可以模拟出来类，类更多的是对函数的`归集`和`复用`进行扩充升级。

在调用函数时不得不提的就是 `参数` 了，很多小伙伴写函数很容易就写成了：

```javascript
function area (width, height) {  
    return width * height;
}
```

两个参数还好脑子记得住，但是下面这种情况乍办：

```javascript
function infomation (
    name, sex, height, birthday, 
    color, likes, follow, age
) {
    // ...
}
```

这么多参数每次开发调用时有使用 `ide` 会自动提示还好，如果没有则有可能需要翻文档或者跳转到定义处查看，除了比较麻烦点外还行。

> 程序员何必为难程序员。

不知道大家有没有和别人对接过开发，有的同学开发有时候不会考虑别人是否对他的代码有`依赖`，直接脑袋一拍就给你的参数顺序对调了，结果代码提交后全军崩溃各种`报错飘红`。

## 传递对象而不是参数列表

可以利用 JavaScript 的对象来传递参数：

```javascript
function infomation (user) {
    // user.name
}

infomation({ name: 'xiaoer', age: 18 })
```

相对于参数列表传递对象属性更好记也没有强制的顺序，如果命名足够清晰在后期维护代码的时候甚至只要看`属性名`就可以马上理解过来。如果其他同学开发新的功能也不会怕他顺序乱调了，但是最好要对新加的参数做出兼容，不然还是会让依赖的其他函数一路飘红。

## 使用解构赋值

参数列表被对象替换解决了参数列表顺序的问题，可是每次调用的时候都需要从`对象中取值`使得函数每次都要访问对象，带来了变量长度变长和很多无意义的`赋值`。再者如果调用者不小心`多传递了参数`，再不巧函数中遍历了对象这可能会产生BUG，可以利用解构赋值来解决：

```javascript
function infomation ({ name, age, height }) {

}
```

这样既对传递的参数做出了`防御`又可以方便的使用参数。

## 使用默认值

> 你永远不知道用户会怎么使用产品。

产品上线后总会出现各种奇奇怪怪的错误，用户总是不按照预期进行操作产品，不断的 BUG 传来实在让人难受。

> 程序员何必为难程序员。

其实在调用函数时我们也是一个用户，有的参数不能为空但是我们却给出了空值，导致函数不能按预期执行。在书写函数时应该做好别人调用函数时不按套路出牌的情况，例如给出默认值和对数据进行转化：
```javascript
function infomation ({ name = 'anonymous', age = 0, height = 160 }) {
    // ...
}
```

当然你也可以使用 `TypeScript` 等工具来提升编程的安全性，但 `巧妇难为无米之炊` 在有的时候不是你想用就能用的，需要整个公司一起进行技术的升级。

## 参数变为可选参数

上面例子中的函数在 `infomation({ age: 16 })` 这样调用的情况下，可以按照预期的默认值执行。但是想让这个对象也可选的时候 `infomation()` 将会报错，因为没有对象让其解构。可以利用 `{}` 来使得对象也可选：

```javascript
function infomation ({ name = 'anonymous', age = 0, height = 160 } = {}) {
    // ...
}
```

## 重命名

有时候需要对参数进行重命名，但是已经很多地方都使用了这个参数时。可以在函数执行最开始的时候进行重命名，但是这样显然不够 geek（主要是不够偷懒）依旧利用 `解构赋值` 来实现重命名：

```javascript
function infomation ({ name:username = 'anonymous', age = 0, height = 160 } = {}) {
    // ...
}
```

当然 `解构赋值` 也可以在平常开发中使用，方便我们写出 `规范` 的 `奇淫技巧`，带来偷懒摸鱼同时也带来优雅。

## 强制传递参数

除了使用参数默认值，也可以对函数参数进行强制传递参数：

##### 脚本

```javascript
// 帮助函数
const err = ( message ) => {
    throw new Error( message );
}

// 函数
const sum = function (
    num = err('first param is not defined'), 
    otherNum = err('second param is not defined')
) {
    return num + otherNum;
}
```

##### 调用测试

```javascript
// 测试函数
// 输出: 3
console.log(sum(1, 2));

// 测试第一个参数不传递
// Uncaught Error: first param is not defined
sum( undefined, 10 );

// 测试第二个参数不传递
// Uncaught Error: second param is not defined
sum( 10 );
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)