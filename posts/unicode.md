<!-- # 字符编码排雷录 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/unicode/poster.png)

## 简介

> [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday)

计算机重重底层之下都是由 0 和 1 组合，但是你知道他们是怎么一步步变成字符串的嘛？在我们现实生活中最常见的例子可以通过 `wo` 在新华字典中找到 `我` 这个字。同样计算机通过 0 和 1 组合在 `字典` 中查找到对应的字符，那 `字典` 内容是什么呢？

##### 起源

计算机诞生于 `美国` 它的使用者大多数使用英文，`美国国家标准学会` 便制定了这本`字典`包括了 `26个大写英文字母`、`26个小写英文字母`、`10个阿拉伯数字`等总共 `256` 个字符的 ASCII 字符集。

##### 混乱

ASCII 用二进制来表示就是 `0000 0000` 到 `1111 1111` 被用得满满当当，汉字就没有地方可以放得下了这下怎么办？正所谓江山大有人才出，国标编码 `GB` 系列出现了，其中最耳熟能详的就是 `GB2312`。

那么问题来了世界拥有 `2500` 至 `3500` 种语言，有文字的语言有 930 种。你能想象你在浏览不同语言界面的时候，需要自己不断的去切换 `字典` 并且 每次切换查找不到的字符就会`乱码`出现。

##### 统一

> 书同文，车同轨，行同伦。

上面这句话歌颂了秦始王具有跨时代意义的成就，但是现实世界中统一语言显得不可能。那我们能否换个思路解决这个问题呢？先思考一个问题：“把大象放入冰箱需要几步”，答案大家都知道“打开，装进去，关上”。那统一字符怎么办呢？那就是创建一个足够大的`字典`把所有的字符都放进去。

##### 万国码

Unicode 万国码 轰隆一声诞生了，顾名思义统一了全世界的所有文字编码可以到 [Unicode Consortium](http://unicode.org/) 和 [codepoints](https://codepoints.net/basic_multilingual_plane) 中查看，对应的实现有UTF8、UTF16
、UTF-32。

##### 可变长度字符编码

UTF8、UTF16、UTF-32最大区别在于对应多少字节的数据，越大能存储的字符也就越多。其中 UTF-8 就是在互联网上使用最广的一种 Unicode 的实现方式，也就是现在 html 中最常看到的 `<meta charset="UTF-8">` 所声明字符集。

UTF 最大的特点在于`可变长的字节`，例如 UTF8 可以是 1到4个字节来记录 `万国码`，为什么这么设计呢？日常使用得到的字符对应的字符编码没有必要占用这么多字节，例如 `0000 0000` 和 `0000 0000 0000 0000` 都能表示 0，那使用更短的字节所占用的空间更小，传输的速度更快。

##### 小插曲

在统一编码的过程中还出现了一个字符集 `UCS-2`，它固定使用 2个字节来编码 与 UTF 可变长度字符编码有一定程度上的不同，但是随着统一进程下被 `UTF-16` 收编了。

## JavaScript 字符处理

了解字符基本原理和进程后，那么 JavaScript 是什么编码呢？没错它就刚才 `小插曲` 中提到的 `UCS-2`，原因是 JavaScript 诞生时 `UTF-16` 还没有出现。

但是现在大家都在使用 `UTF 可变长度字符编码`，`UTF-16` 的可变字节为 2个或者 4个，而 `UCS-2` 却只有 2个。这样两个字符集之间就有存在一个 `UCS-2` 无法识别的 4字节，JavaScript 在处理字符时会`傻傻`的按着 `UCS-2` 的两字节去处理，再加上`字典`里没有这个字符`笨笨`的小脑袋瓜无法处理只能输出乱码。

由于 emoji 表情的普及，而且 emoji 刚好就是处于 `UCS-2` 的`字典`之外，在前端开发中遇到可能出现 emoji 的地方需要小心谨慎：

### 长度

##### BUG 预警

现在最为常用的 emoji 表情为 4个字节编码表示，由于 `UCS-2` 固定两个字节，在统计长度时 emoji 会被当做两个 `UCS-2` 字符，结果会和我们预期的输出大了一倍。

```javascript
let emoji = "😊";

// 输出 2
console.log(emoji.length);
```

##### BUG 解除

利用 es6 的 `Array.prototype.from` 和 `spread` 来做字符串转数组并计算长度：

```javascript
let emoji = "😊";

// 输出 1
console.log(Array.from(emoji).length);

// 输出 1
console.log([...emoji].length);
```

如果不支持 `Array.prototype.from` 可以利用正则替换把 4字节的字符替换为 _ 并计算长度：

```javascript
let emoji = "😊";

function countSymbols(string) {
    var regexAstralSymbols = /[\uD800-\uDBFF][\uDC00-\uDFFF]/g;
    return string
        .replace(regexAstralSymbols, '_')
        .length;
}

// 输出 1
console.log(countSymbols(emoji));
```

对于其他的字符串操作，例如拼接或者替换也可以利用数组来实现。

### 反转字符串

如同上面所讲 emoji 会被当做两个 `UCS-2` 字符，反转的时候 4个完整的字节会被硬生生的拆分开来，可以使用 [Esrever](https://github.com/mathiasbynens/esrever) 来解决。

```javascript
let emoji = "😊";

// 输出为两个乱码字符
console.log(emoji.split('').reverse().join(''));
```

### 字符编码转换

在使用 `String.prototype.charCodeAt` 和 `String.fromCharCode` 会出现问题。可以使用 ES6 的两个新方法来替换 `String.prototype.codePointAt` 和 `String.fromCodePoint`。

### 正则匹配

正则里 `.` 表示匹配一个字符，但是 `UTF-16` 4字节字符会被当做两个字符来处理，进而引起错误。ES6 给出了新的解决方法加上 `u` 标志 `/./u.text('😊')`，所以写正则的时候要记得加上哦。

### 字符串遍历

对于字符串的遍历可以使用 `for...of` 语句。

### 场景

如果后端数据库运行存储 emoji 作为用户名时，前端在限制用户名长度判断时需要注意`UTF-16` 4字节字符带来的统计错误，其他类似场景同理可得。

> 小提示：在做微信公众号开发时，由于用户名和用户输入可能出现 emoji 等字符，需要对数据库进行字符集的设置。

> 不要问我为什么知道，因为我的眼里常含泪水。

## 一起成长

如果您感觉有收获可以点赞关注我，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)