<!-- # 调试黑魔法 -->

![封面](../images/super-console/poster.png)

## 简介

> console.log、调试辅助函数、调试小技巧

> ⚠️ 请注意本文不是讲 console 各种方法，请不要点出去。

本来想取名为 `console` 黑魔法，顺手讲一点 `console` 的其他方法。可是查阅资料的时候发现好多文章都已经写得非常好了，这部分相关的内容大家可以到`掘金`查看 👉 [传送门](https://juejin.im/search?query=console&type=all)。

今天来讲点不一样的，其实有了那么多 `console` 方法开发中最经常用到的还是 `console.log`，那你知道怎么让 `console.log` 来帮你摸 🐟 减少 Debug 工作量嘛？

> ps: 当然天下除虫，唯断点调试不破。

## 普通 Debug

在开发时最经常碰到的场景之一就是函数嵌套了：

```javascript
star(
    pushmetop(
        github('ok!')
    )
)
```

好家伙这嵌套够深，如果前方产品八米加急找到你说请求 star 函数出错了，一脸视死如归的同学打开对应代码开始调试：

```javascript
const a = github('ok!');
console.log(a);

const b = pushmetop(a);
console.log(b);

const c = star(b);
console.log(c);
```

## 超级 Debug

好家伙满满当当的魔术变量和 `console.log`，这显然会减少大量摸🐟时间，机智的我们为何不对 `console.log` 进行升级：

```javascript
const superme = (x) => (console.log(x), x)
```

> 小技巧：利用逗号表达式来写写出优雅的代码，例如 `x => (x=x+1, x)`。

这下再除虫简直不要太舒服，简直`指哪打哪`：

```javascript
star(pushmetop(
    // 想除哪就除拿
    superme(github('ok!'))
))
```

## 超超级 Debug

除了 iphone 有 plus 我们的 `debug` 怎么可能没有呢？

```javascript
const supermePlus =  (x, fn = (y) => y) => fn(x)
```

有了 supermePlus 我们可以在调试的时候方便的插入调试代码：

```javascript
star(
    // 想怎么加就怎么加
    supermePlus(pushmetop(github('ok!')), (x) => {
        // 测试 x 是不是数字
        console.log(typeof x === 'number' && x === x);
        return x;
    })
);
```

也可以方便的替换值：

```javascript
star(
    supermePlus(pushmetop(github('ok!')), (x) => 'good!')
);
```

## 字符串妙用

> 在新版的 chrome 已经可以直接输出函数内容了。

在调试时打印函数时，往往会输出一段字符串：

```javascript
const user = {
    greet: function () {
        console.log('hello world')
    }
}

// 输出: [Function: greet]
console.log(user.greet)
```

但是在需要参看函数详情时可以利用拼接字符串来实现：

##### 脚本

```javascript
const user = {
    greet: function () {
        console.log('hello world')
    }
}

console.log(user.greet + '')
```

##### 输出

```
function () {
    console.log('hello world')
}
```

## 其他

提供一个简单的函数定义，方便大家测试本文章中的代码

```javascript
const github = x => x;
const pushmetop = x => x + '!';
const star = x => x + '?';
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)