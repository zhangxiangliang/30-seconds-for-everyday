<!-- # 复制内容到剪贴板 -->

![封面](../images/copy-to-clipboard/poster.png)

## 简介

> 剪贴板、复制、兼容

`复制内容到剪贴板` 是前端开发过程中会经常遇到的一个需求，大部分同学开发时往往会直接打开搜索框开始寻找别人写好的组件库，而聪明的同学会开始思考问题：

* 产品的使用场景是什么？
* 是否需要兼容很多浏览器？
* 是否在项目中需要频繁使用？
* 是否需要使用第三方库额外提供的功能？

当产品使用场景并不大和复杂时，可以使用这段 `复制内容到剪贴板` 代码：

```javascript
// 该源码来自于 https://30secondsofcode.org
const copyToClipboard = str => {
    const el = document.createElement('textarea');
    el.value = str;
    el.setAttribute('readonly', '');
    el.style.position = 'absolute';
    el.style.left = '-9999px';
    document.body.appendChild(el);

    const selected = document.getSelection().rangeCount > 0 ? document.getSelection().getRangeAt(0) : false;

    el.select();
    document.execCommand('copy');
    document.body.removeChild(el);

    if (selected) {
        document.getSelection().removeAllRanges();
        document.getSelection().addRange(selected);
    }
};
```

<!--more-->

## 代码分析

浏览器提供了一个原生方法 `document.execCommand('copy')` 来实现 `复制内容到剪贴板`，但是它有一个使用前提“需要选择文本框或者输入框时”，所以先创建一个 `textarea` 文本框并通过定位让它不显示在屏幕里：

```javascript
const el = document.createElement('textarea');
el.value = str;
el.style.position = 'absolute';
el.style.left = '-9999px';
document.body.appendChild(el);
```

对创建好的 `textarea` 元素进行选中并使用复制里面的文本内容，最后移除掉  `textarea` 元素。

```javascript
el.select();
document.execCommand('copy');
document.body.removeChild(el);
```

### 为什么跳过了一大段代码了？

其实到此为止就已经实现好了 `复制内容到剪贴板`，跳过代码分别是对两个场景的优化，可以根据产品开发的场景来选着是否使用这两段代码：

* 场景是否包括移动设备
* 是否页面可以让用户选中文本

### 移动设备优化

移动设备上有一个问题 “当文本框被选中时，会弹出虚拟键盘” 会导致页面出现闪烁，如果手机响应较慢甚至可以看到虚拟键盘弹出和消失的过程。这段代码的点睛之笔之一在于把输入框设置为只读：

```javascript
el.setAttribute('readonly', '');
```
> 小技巧：利用只读属性来防止弹出虚拟键盘。

### 可选中文本优化

代码的另外一处点睛之笔在于：如果用户选中了某段文字后点击`复制内容到剪贴板`的复制操作这段选中的文字就会消失掉，肥肥的大拇指在手机屏幕像选着文本内容一直是一件挺让人不舒服的操作，选中文字的消失十分影响用户体验。

我们可以利用 `document.getSelection` 一系列光标选中 API 来帮助我们先记录下用户之前所选的文字对象：

```javascript
const selected = document.getSelection().rangeCount > 0 ? document.getSelection().getRangeAt(0) : false;
```

再进行完复制操作后对 `selected` 进行判断，并恢复先前记录下用户之前所选的文字对象：

```javascript
if (selected) {
    document.getSelection().removeAllRanges();
    document.getSelection().addRange(selected);
}
```

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/zhangxiangliang/30-seconds-for-everyday) 给个 `小星星`。

> 本文原稿来自 [ZhangXiangLiang](https://github.com/zhangxiangliang)