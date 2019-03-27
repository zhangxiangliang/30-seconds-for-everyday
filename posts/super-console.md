<!-- # 调试黑魔法 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/super-console/poster.png)

## 简介

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

> 👉 [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday) 👈

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

## Superme Debug

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

## Superme Plus Debug

除了 iphone 有 plus 我们的 `debug` 怎么可能没有呢？

```javascript
const supermePlus = function (x, fn = (x) => x) {
    return fn(x);
}
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

## 其他

提供一个简单的函数定义，方便大家测试本文章中的代码

```javascript
const github = x => x;
const pushmetop = x => x + '!';
const star = x => x + '?';
```

## 一起成长

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)