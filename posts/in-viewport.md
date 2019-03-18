# 巧用可视区域
## 简介

`可视区域`是一个前端优化经常出现的名词，不管是显示器、手机、平板它们的`可视区域`范围都是有限。在这个 `有限可视区域` 区域里做到完美显示和响应，而在这个区域外少做一些操作来减少渲染的压力、网络请求压力。在 [每日 30 秒之 对海量数据进行切割](https://pushmetop.github.io/blog/chunk-for-30-seconds-of-code/) 中的使用场景，我们就是利用了 `有限可视区域` 只渲染一部分 DOM 节点来减少页面卡顿。

> 既然 `可视区域` 这么重要是否有什么速成秘籍来帮我们？

![生活终于对我这只小猫咪动手了](https://raw.githubusercontent.com/pushmetop/resource/master/pushmetop.github.io/element-is-visible-in-viewport-for-30-seconds/life-taken-me.png)

控制住每一个元素在`可视区域`的出现，就可以扼住命运的后颈为所欲为：

```javascript
// 该源码来自于 https://30secondsofcode.org
const inViewport = (el, partiallyVisible = false) => {
    const { top, left, bottom, right } = el.getBoundingClientRect();
    const { innerHeight, innerWidth } = window;
    return partiallyVisible
        ? ((top > 0 && top < innerHeight) || (bottom > 0 && bottom < innerHeight)) &&
        ((left > 0 && left < innerWidth) || (right > 0 && right < innerWidth))
        : top >= 0 && left >= 0 && bottom <= innerHeight && right <= innerWidth;
};
```

<!--more-->

## 代码分析

使用 [Element.getBoundingClientRect](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect) 方法返回元素的大小及其相对于视口的位置，可以得到当前元素相对 `可视区域` 的坐标：

```javascript
const { top, left, bottom, right } = el.getBoundingClientRect();
```

得到元素的坐标信息后，就需要获得 `可视区域` 的宽高来帮助我们确定是否在范围内：

```javascript
const { innerHeight, innerWidth } = window;
```

先判断是否需要整个元素都出现在 `可视区域`：

```javascript
if (partiallyVisible) {
    // 只需要出现在可视区域 
} else {
    // 需要整个元素都在可视区域内
}
```

判断元素头部或者底部是否在 `可视区域` 出现：

```javascript
(top > 0 && top < innerHeight) || (bottom > 0 && bottom < innerHeight)
```

判断元素左部或者右部是否在 `可视区域` 出现：

```javascript
(left > 0 && left < innerWidth) || (right > 0 && right < innerWidth)
```

当需要整个元素都出现在屏幕的时候，需要同时判断四个相对坐标：

```javascript
top >= 0 && left >= 0 && bottom <= innerHeight && right <= innerWidth
```

## 使用场景

现在网页中经常会出现大量的图片，然而加载大量图片会影响网页加载速度，我们可以利用 `可视区域` 来实现图片的懒加载。为什么要懒加载图片：

##### 大量的图片请求会增加服务器的压力。
* 使用 CDN 加速来缓解服务器压力例如 `七牛云`。

##### 加速用户的网页加载速度，当图片数量巨大需要占用请求资源和显示速度。
* HTTP1 文件限制会对同一个域名限制文件请求数 可以通过 `影子域名` 来绕过这个限制。
* 利用 `可视区域` 当移动到某个 `标志元素` 时再进行更多数据和图片的加载。
* 利用占位图片来防止页面塌陷。

##### 用户访问页面有时候只是粗略的一撇。
* 利用 `可视区域` 加载部分数据图片节省网络流量。

##### 结构

```html
<div class="container">
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
    <div class="img-box img-placeholder" data-src="http://suo.im/5p9IOS"></div>
</div>
```

##### 样式
```css
.img-box {
    width: 200px;
    height: 200px;
    margin: 10px 0 10px 10px;
    background: #eee;
    display: inline-block;
}

.img-box > img {
    width: 100%;
    height: 100%;
}
```

##### 脚本

```javascript
window.onload = () => lazyLoading()
document.addEventListener('scroll', lazyLoading)

function lazyLoading() {
    const boxs = document.querySelectorAll('.img-placeholder')

    Array.from(boxs).map(box => {
        if (!inViewport(box, true)) return;

        // 获取图片地址并清除数据记录 
        const src = box.getAttribute('data-src');
        box.removeAttribute('data-src');

        // 插入图片 DOM
        box.innerHTML = `<img src='${src}'>`;

        // 去除占位 class
        box.className = box.className.replace('img-placeholder', '')
    })
}
```

## 打赏&联系

如果您感觉有收获，欢迎给我打赏，以激励我输出更多的优质内容。

![打赏&联系](https://raw.githubusercontent.com/pushmetop/resource/master/donate/donate.png)

> 本文原稿来自 [PushMeTop](https://pushmetop.github.io)
