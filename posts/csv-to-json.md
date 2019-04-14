<!-- # CSVToJSON -->

![封面](https://raw.githubusercontent.com/pushmetop/resource/master/30-seconds-for-everyday/csv-to-json/poster.png)

## 简介

> 数组、CSV、表格、工具

我们之前的两期 [数组转 CSV 表格数据](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/array-to-csv.md) 和 [JSON 对象数组转换 CSV 表格数据](https://github.com/pushmetop/30-seconds-for-everyday/blob/master/posts/json-to-csv.md) 中学习了转化为 `CSV` 表格数据的代码片段，今天就讲讲 如何把 CSV 表格数据转换为 JSON 对象：

```javascript
// 该源码来自于 https://30secondsofcode.org
const CSVToJSON = (data, delimiter = ',') => {
  const titles = data.slice(0, data.indexOf('\n')).split(delimiter);
  return data
    .slice(data.indexOf('\n') + 1)
    .split('\n')
    .map(v => {
      const values = v.split(delimiter);
      return titles.reduce((obj, title, index) => ((obj[title] = values[index]), obj), {});
    });
};
```

## 代码分析

利用 `\n` 取出表头数据 并使用 `Array.prototype.split` 把表头数据分割为 表头字段数组用于构造 `JSON` 对象的键值：

```javascript
const titlesData = data.slice(0, data.indexOf('\n'));
const titles = titlesData.split(delimiter);
```

取出表格数据并使用 `Array.prototype.split` 分割为行数组

```javascript
const rows = data
    .slice(data.indexOf('\n') + 1)
    .split('\n')
```

使用 `Array.prototype.map` 遍历所有行数据获得对象数组：

```javascript
return rows.map(v => {
    // ...
    // 返回创建对象
});
```

遍历过程中进行数据分割 和 对象拼装：

```javascript
const values = v.split(delimiter);
titles.reduce((obj, title, index) => (obj[title] = values[index]), obj), {});
```

> 小技巧：利用 `,` 运算顺序可以优雅的写出先赋值后返回数据的精简代码。

## 使用场景

用户上传 CSV 表格数据转化为 JSON 并上传到服务端，这里不对 CSV 的 BOM 进行判断和处理（相关内容可以查看 [你所不知道 ❌ BOM](https://segmentfault.com/a/1190000006833935)）。

##### 结构

```html
<input type="file" name="file" onchange="importPostData(this.files)">
```

##### CSV内容

```csv
title,content
pushmetop,让我们一起变得更好
sf,答题平台
掘金,掘金是一个帮助开发者成长的社区
```

##### 脚本

```javascript
function importPostData(files) {
    const reader = new FileReader();
    reader.onload = function (e) {
        const data = CSVToJSON(e.target.result)
        // 发送数据请求到服务端
    };
    reader.readAsText(files[0]);
}
```

> 动手试试：利用 CSVToJSON 和 JSONtoCSV 实现一个简单的数据库？

## 一起成长

> 在困惑的城市里总少不了并肩同行的 `伙伴` 让我们一起成长。

* 如果您想让更多人看到文章可以点个 `点赞`。
* 如果您想激励小二可以到 [Github](https://github.com/pushmetop/30-seconds-for-everyday) 给个 `小星星`。
* 如果您想与小二更多交流添加微信 `m353839115`。

![微信公众号](https://raw.githubusercontent.com/pushmetop/resource/master/donate/pushmetop.png)

> 本文原稿来自 [PushMeTop](https://github.com/pushmetop)