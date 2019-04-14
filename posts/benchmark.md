<!-- # 谁敢与我一战 -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/benchmark/poster.png)

## 简介

> benchmark、基准测试、jsPerf

在 [优雅插入数组](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/insert-item-inside-an-array.md) 一文中大家最多的评论就是 “能不能加个基准测试”。小二不是不喜欢加基准测试而是现在硬件设备的性能越来越快了，有时候一些操作不是性能问题的主要原因，当然这不是我们不写出好代码的理由。

书写代码还是应该在 `优雅易读` 和 `运行性能`中做出平衡，适合的场景做适合的事情。不过既然大家都提到了 `基准测试` 碰巧我又刚好没有想到要写什么那就一起了解一下 `基准测试` 吧。

> 人非圣贤孰能无过，三两八哥常伴吾身。-- 嗯是我

`测试` 在中大型和和开源项目中算是 `必备内容`，好测试可以在假定的场景下找到项目的错误帮助我们写出质量更好的代码，也是协作开发中的调和剂。`测试` 是一门开发中的大学问不是一篇文章就能讲得明白的。

> Talk is cheap, Show me the code. -- Linus Torvalds

本文选择的 `基准测试` 只是 `测试` 中一个小分支，本文简单帮助大家涉猎一些简单的概念和测试工具。学习后当遇到野生程序猿说出骚话：`“废话少说，放马过来”`，请抄起键盘打开 `基准测试` 工具大喊：`“吾乃燕人张翼德，谁敢与我一战？”`。

## 抛硬币

抛一次硬币就得到 `出现正面概率是百分百` 的结论显然是错误的，数学老师教过我们 `大数定律`：“需要数据量足够多、样本足够打才能下结论”。当抛均匀硬币次数足够多时出现正面概率应该无限趋近于百分五十，对照抛硬币实验 `基准测试` 一样不能只记录一次代码运行时间就可以得出结果的，需要进行足够多的次数。

## 吓螃蟹

> 科学家从笼子里抓出一只螃蟹，放在地上，冲着它大吼大叫，螃蟹被吓得不轻，到处乱窜，慌不择路。然后科学家把螃蟹的腿拆卸下来重复之前的步骤，继续大吼大叫，螃蟹一动不动，非常的淡定从容，得到结论`螃蟹的耳朵是长在腿上的`。

这个小笑话大家应该都听过，没有考虑螃蟹逃跑是需要用腿。在做生物对照实验时出现的三个概念 `自变量` 和 `因变量`、`无关变量`，控制好它们从而得到真实的结果。`基准测试`的影响变量可以是手机进入省电模式带来的运行速度降低，可以是电脑正在运行无关软件导致某一时刻测试环境不一致，也是可以是代码初始状态的不一致例子如下：

```javascript
// 代码一
let a = [1, 2, 3, 4];
a.push(5);

// 代码二
let b = [1, 2, 3, 4, 5, 6, 7, 8];
b = [...b, 9];
```

测试上面两个代码并不能得出谁的性能更好，因为初始数组的长度不一样存在数组越大操作越慢的情况。

## Benchmark

上面简单两个例子帮助理解 `基准测试` 的一些基本要点。在开发中除了利用浏览器的特性来调优代码，有时候不同的代码写法也会带来不一样的性能表现。在 [优雅插入数组](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/insert-item-inside-an-array.md) 中把数据插入数组尾部就介绍了四种不一样的方法，利用哪一种写法会使得代码 `优雅、易懂、跑得快`呢，可以使用 [Benchmark](https://github.com/bestiejs/benchmark.js) 来帮助测试得到结论。

### 安装

```
npm i --save benchmark
```

### 使用

* `add` 接口添加测试代码。
* `on` 接口插入代码到测试周期中。
* `run` 运行代码。

### 例子

##### 代码

```javascript
let suite = new Benchmark.Suite;

suite
    .add('#1 利用数组长度进行赋值', () => {
        let arr = [1, 2, 3, 4, 5];
        arr[arr.length] = 6;
    })
    .add('#2 利用 Array.prototype.push 方法', () => {
        let arr = [1, 2, 3, 4, 5];
        arr.push(6);
    })
    .add('#3 利用 Array.prototype.concat 方法', () => {
        let arr = [1, 2, 3, 4, 5];
        arr = arr.concat(6);
    })
    .add('#4 利用 spread 运算符', () => {
        let arr = [1, 2, 3, 4, 5];
        arr = [...arr, 6];
    })
    .on('start', (event) => {
        // 在整个测试运行前
        console.log('把数据插入数组尾部');
    })
    .on('cycle', (event) => {
        // 每个测试代码运行后
        console.log(String(event.target));
    }).on('complete', () => {
        // 测试完成后
        console.log('最快方法是 ' + suite.filter('fastest').map('name'));
    }).run({ 'async': true })
```

##### 输出

```
#1 利用数组长度进行赋值 x 3,590,121 ops/sec ±0.97% (87 runs sampled)
#2 利用 Array.prototype.push 方法 x 15,796,478 ops/sec ±0.61% (88 runs sampled)
#3 利用 Array.prototype.concat 方法 x 2,373,044 ops/sec ±1.00% (83 runs sampled)
#4 利用 spread 运算符 x 2,405,217 ops/sec ±0.72% (91 runs sampled)
最快方法是 #2 利用 Array.prototype.push 方法
```

## jsPerf

> A benchmarking library. As used on jsPerf.com.

在 [Benchmark](https://github.com/bestiejs/benchmark.js) 仓库中的项目简介中提到了 [jsPerf](https://jsperf.com/) 一个基于 `Benchmark` 的便捷`基准测试`站点。使用 Github 登录后，按照创建表格中的数据填写就能生成`基准测试`。

`基准测试` 例子 在 jsPerf 中链接为 [数据插入数组尾部](https://jsperf.com/insert-item-inside-an-array-at-the-end)，利用 jsPerf 可以很方便的进行分享（就像现在），还可以在不同浏览器中打开测试。下面对页面名称进行简单翻译方便英语不好的同学使用：

### 个人信息 

| 名词 | 解释 |
| --- | --- |
| Your details | 个人信息，可选填 |
| Name | 作者名字 |
| Email | 作者邮箱，由于生成头像 |
| URL | 项目地址 |

### 案例信息 

| 名词 | 解释 |
| --- | --- |
| Test case details | 案例信息 |
| Title | 标题 |
| Slug | 网站 slug，会被拼接成 https://jsperf.com/slug |
| Description | 项目描述 |

### 预加载

| 名词 | 解释 |
| --- | --- |
| Preparation code | 预加载 |
| Preparation code HTML | 项目需要的 DOM 结构 和 引入外部脚本 |
| Define setup for all tests | 每次测试前将会执行的操作即 Benchmark.setup 中的配置，例如初始化变量。 |
| Define teardown for all tests | 每次测试后会执行的操作即 Benchmark.teardown 中的配置，例如清除变量。 |

### 需要比较的代码段

如果有不需要的测试代码框只需要放空内容并保存就会自己删除。

| 名词 | 解释 |
| --- | --- |
| Code snippets to compare | 需要比较的代码段 |
| Title | 测试代码段标题 |
| Async | 代码段是否异步 |
| Code | 需要测试的代码 |
| Add code snippet | 添加测试代码 |
| Save test case | 保存 |

### 测试页面

| 名词 | 解释 |
| --- | --- |
| Run test | 运行测试 |
| Testing in ... | 测试所在的浏览器及其版本、操作系统及其版本 |
| Ops/sec | 每秒钟代码执行次数，数值越大越好 |
| You can edit these tests or add even more tests to this page by appending /edit to the URL. | 点击该链接可以修改测试代码，但是 slug 这些是改不了的 |
| Compare results of other browsers | 所有浏览器测试结果 |
| Chart type | 数据展示方式：条形图、折线图、饼图、表格 |
| Filter | 浏览器环境 |

## 结尾

> 还不赶紧带上键盘与野生程序员大战三百回合，打满经验升级飞仙成为上古程序员。

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)