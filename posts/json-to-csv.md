<!-- # JSONToCSV -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/json-to-csv/poster.png)

## 简介



> 👉 [一天 30 秒 ⏱ 一段代码 ✍️ 一个场景 🖼](https://github.com/pushmetop/30-seconds-for-everyday) 👈

我们在 [每日 30 秒之 arrayToCSV](https://pushmetop.github.io/blog/array-to-csv-for-30-seconds-of-code) 中一起学习了将数组数据转化为 `csv` 表格数据并导出，那如果是对象数组怎么办呢？小脑袋瓜转得快的同学肯定会说：“使用 `Array.prototype.map` 把需要导出的字段先遍历取出，再使用 `arrayToCSV` 将其导出为 CSV 数据表格。”

可是你有没有想过如果一个对象数组数据非常之大时，使用 `Array.prototype.map` 和 `arrayToCSV` 将会多出一倍的数据遍历操作。作为优化狂魔的我们（那之前文章的使用场景还这么用！！！）肯定不允许这种事情发生，那就一起来学习一个用于对象数组且少花一半时间的转换表格函数。

```javascript
// 该源码来自于 https://30secondsofcode.org
const JSONtoCSV = (arr, columns, delimiter = ',') =>
  [
    columns.join(delimiter),
    ...arr.map(obj =>
      columns.reduce(
        (acc, key) => `${acc}${!acc.length ? '' : delimiter}"${obj[key] || ''}"`,
        ''
      )
    )
  ].join('\n');
```

<!--more-->

## 代码分析

把传入需要提取的对象属性作为表头用分隔符分割开来：

```javascript
columns.join(delimiter)
```

使用 `Array.prototype.map` 来遍历对象数组获得 表头属性属性对应的值 并将其解构开：

```javascript
...arr.map(obj => fn)
```

当属性不存在时利用 `||` 技巧来初始化数据，并利用 `Array.prototype.reduce` 来拼接数据，注意 `分隔符` 应该在每两个数据之间：

```javascript
columns.reduce((acc, key) => {
    let value = obj[key] || ''
    acc += !acc.length ? '' : delimiter
    acc += `"${value}"`
}, '')
```

把表头数组和对应的属性数据组成的数组用 `\n` 来拼接数据：

```javascript
[..., ...].join('\n')
```

## 使用场景

将页面上用户数据导出为 Excel 表格并且提供下载，本文的 `JSONtoCSV` 直接使用属性作为表头数据，机智的同学可以自己增加上表头默认字段来将 `JSONtoCSV` 函数变得更加完美。

##### 结构

```html  
<a id="download-user-data"
    onclick="downloadUserData(this)"
    download="downlaod.csv"
    href="#">download</a>      
```

##### 脚本

```javascript
const users = [
    { name: 'xiaoer', age: 24, sex: '男' },
    { name: 'xiaosi', age: 8, sex: '男' },
    { name: 'menty', age: 18, sex: '女' },
]

function downloadUserData(target) {
    const csv = JSONtoCSV(users, ['name', 'age', 'sex'])
    target.href = `data:text/csv;charset=utf-8,\ufeff${csv}`
}
```

一些面向百度编程的同学直接使用 `data:text/csv;charset=utf-8,${csv}` 来导出数据会出现乱码，而本文中相对网络上的版本增加了 `\ufeff` 这个BOM头来告诉 `Excel` 数据为 `UTF-8` 编码解决乱码问题。想知道更多关于 BOM 头的内容可以查看 [你所不知道的 BOM](https://pushmetop.github.io/blog/you-dont-know-bom)。

## 一起成长

> 👇 更新平台多偶尔会漏掉，如果觉得文章还行点个 `star` 防走失。

如果您感觉有收获可以点赞关注`激励我`，也欢迎到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 加个 star。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)