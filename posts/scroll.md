<!-- # 迴囬囘回到顶部 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/scroll/poster.png)

## 简介

> 回到页面顶部、兼容性、最佳写法、滚动到任意处

在 [大家一起被捕吧](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/lets-get-arrested.md) 中刚写了：

> 在日常开发中我们往往会从用户那获得各种输入，例如搜索框、评论框、文章内容等等。

结果在 `segmentfault` 阅读评论时看到了一个链接一点直接把我给`滚动到顶部`，顿时心中一阵 `惨叫双手捶胸` 后把页面拉回评论并打开了 `控制台` 查看了链接为何方神圣：

```html
<a href="#">...</a>
```

顿时又是一阵 `惨叫双手捶胸` 原来 `segmentfault` 评论是支持 markdown 语法的，如果再评论里输入 `[...](#)` 则会被转换成如上代码。

好奇心突发跑到了 `掘金` 测试了一下带连接的评论，打开 `控制台` 看了看由于使用了 `target="_blank"` 没有出现被传送到顶部的情况，心里暗暗道 `喵哉 🐱` 以后还是得小心行事，碰巧每日30秒正愁不知道写什么那就来写写 `回到顶部` 吧。

## 回到顶部

第一种写法就介绍一下今天被中全套的代码，利用了 `锚点` 来实现回到顶部：

```html
<a href="#"回顶部></a>
```

如果需要滚动到别的元素可以使用 `id` 属性配合 `锚点` 来实现：

```html
<header id="header">我是头部</header>
<a href="#header">回到页面头部</a>
```

不过由于这种方法 `滚动` 得太快了，性能肯定是很好就是体验不怎么好。不过我们可以使用 css 的 `scroll-behavior` 属性来提升体验：

```css
html, body {
  scroll-behavior: smooth;
}
```

虽然第一种方法配合 css 的 `scroll-behavior` 属性显得挺不错，但是 `scroll-behavior` 兼容性挺不高的具体可以看 [caniuse](https://caniuse.com/#search=scroll-behavior)。

## 迴到顶部

由于在页面垂直滚动过程中会改变 `window.scrollY` 的值，第二种便是写法利用 `window.scrollTo()` 把它设置为 `0` 来实现回到顶部：

```javascript
window.scrollTo(0, 0)
```

不过这样使用也会导致 `滚动` 得太快带来的体验不好，这个时候我们可以利用 `window.requestAnimationFrame()` 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画，该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。

这里使用里一个来判断当页面没有滚动到顶部时循环调用 `window.requestAnimationFrame` 来进行逐步滚动，每次滚动的距离 `c - c / 8` 随着 `c` 的减小而减小进而实现滚动效果：

```javascript
const scrollToTop = () => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }
};
```
不过继续查阅 [caniuse](https://caniuse.com/#search=requestAnimationFrame) 中的 `window.requestAnimationFrame()` 在主流浏览器中支持挺好的，但是需要兼容 `ie6-9` 的同学就得另外寻找方法了。仔细想想 `window.requestAnimationFrame()` 跟 `setTimeout()` 好像有点相似。

`window.requestAnimationFrame` 回调函数执行次数通常是每秒60次即一秒60帧，将 `setTimeout` 执行的频率也设置为一样的就行了：

```javascript
if (!window.requestAnimationFrame) {
    window.requestAnimationFrame = function (callback) {
        return setTimeout(callback, 1000 / 60);
    }
}

const scrollToTop = () => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }
};
```

搞定神器 `ie6-9` 的兼容问题。

## 囬到顶部

第三种写法使用函数 `Element.scrollIntoView()` 可以将选中的元素移动到 `可视区域`，`可视区域` 更多相关知识点可以看之前的一篇文章 [巧用可视区域](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/in-viewport.md)。

```javascript
document.querySelector('body')
    .scrollIntoView({
        behavior: 'smooth',
        block: 'start',
    })
```

代码实现比起第三种简单了不少，当 css 的 `scroll-behavior` 被设置时会默认设置 `Element.scrollIntoView()` 的 `behavior`，依旧打开 [caniuse](https://caniuse.com/#search=scrollIntoView) 查看兼容性会发现和 `window.requestAnimationFrame()` 比起来差不了多少，在神器 `ie6-9` 也有兼容问题。

## 囘到顶部

第四种方法将前面方法进行一个整合，页面支持 `Element.scrollIntoView()` 则直接使用第三种方法，如果页面不支持则使用第二种方法。对于 `Element.scrollIntoView()` 的支持利用到了 `window.getComputedStyle()` 也有兼容性问题需要判断一下：

```javascript
let scrollToTop;

if (window.getComputedStyle && window.getComputedStyle(document.body).scrollBehavior) {
    scrollToTop = () => document.querySelector('body')
        .scrollIntoView({
            behavior: 'smooth',
            block: 'start',
        });
} else {
    if (!window.requestAnimationFrame) {
        window.requestAnimationFrame = function (callback) {
            return setTimeout(callback, 1000 / 60);
        }
    }

    scrollToTop = () => {
        const c = document.documentElement.scrollTop || document.body.scrollTop;
        if (c > 0) {
            window.requestAnimationFrame(scrollToTop);
            window.scrollTo(0, c - c / 8);
        }
    };
}
```

在开发中要注意浏览器的兼容性，多使用 `caniuse` 来帮助我们参看兼容性情况。并根据产品的开发需求来书写代码，例如不需要兼容 `ie6-9` 时我们可以直接使用 `Element.scrollIntoView()`。在刚才的学习中除了学习了回到顶部外，只需再学习一下获取元素所在 `y` 轴坐标或者高度就会 `一不小心顺手` 学习了滚动到页面各处。

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)