# Node Cron

## 起点在这(Getting Started)

* 安装 **node-cron**

```shell
$ npm install --save node-cron
```

* 引入 `node-ceon` 并开始一个定时任务:

```node
var cron = require('node-cron');

cron.schedule('* * * * *', () => {
    console.log('running a task every minute');
});
```

## Cron 时间表达式(expression)

快速预览 **cron** 语法,同时介绍`node-cron`的参数支持

### 允许 时间字段
```
 # ┌────────────── second (optional)
 # │ ┌──────────── minute
 # │ │ ┌────────── hour
 # │ │ │ ┌──────── day of month
 # │ │ │ │ ┌────── month
 # │ │ │ │ │ ┌──── day of week
 # │ │ │ │ │ │
 # │ │ │ │ │ │
 # * * * * * *
```

### 允许 时间值()

field |value
---|---
second|0-59
minute|0-59
hour|0-23
day of month|1-31
month|1-12 (或者 january等月份单词)
day of week|0-7 (或者是 monday等星期单词, 0和7是sunday)

### 使用多个值

同时使用多个值,使用逗号`,`分隔

```node
var cron = require('node-cron');

cron.schedule('1,2,4,5 * * * *', () => {
    console.log('每到分钟数等于 1,2,4,5 时执行一次任务');
});
```

### 使用时间范围

定义一个时间段

```node
var cron = require('node-cron');
 
cron.schedule('1-5 * * * *', () => {
  console.log('每到分钟数等于 1,2,3,4,5 时执行一次任务');
});
```

### 使用分段值

分段值支持和范围值配合,后面紧跟着`/`,例如:`1-10/2`等同`2,4,6,8,10`.<br>
分段值同时支持配合星号`*`,`*/2`意味着每两分钟执行一次.

```node
var cron = require('node-cron');
 
cron.schedule('*/2 * * * *', () => {
  console.log('每两分钟执行一次');
});
```

### 使用时间单词

表示月份和星期时,也可以直接使用单词和简写

```node
var cron = require('node-cron');
 
cron.schedule('* * * January,September Sunday', () => {
  console.log('在 一月和九月 的 星期天 执行一次');
});
```

或者使用简写
```node
var cron = require('node-cron');
 
cron.schedule('* * * Jan,Sep Sun', () => {
  console.log('在 一月和九月 的 星期天 执行一次');
});
```

## Cron 函数

### 定时

任务在时间表达式匹配时进行执行

Arguments:

* **expression** `string`: Cron 表达式
* **function** `Function`: 需要执行的任务
* **options** `Object`: 参数

### 参数(options)

* **scheduled**: 在定时任务创建时,是否直接启动定时,默认值: `true`,布尔类型(Boolean)
* **timezone**: 定时任务所使用的时区

### 完整例子:

```node
var cron = require('node-cron');

cron.schedule('0 1 * * *', () => {
    console.log('在 01:00 执行任务,使用 美国/圣保罗 时区');
}, {
    scheduled: true,
    timezone: "America/Sao_Paulo"
});
```
## 定时任务的方法(Methods)

### Start

开始一个定时任务<br>

```node
var cron = require('node-cron');

var task = cron.schedule('* * * * *', () =>  {
    console.log('当前任务不自动执行');
}, {
    scheduled: false
});
 
// 开始执行任务
task.start();
```

### Stop

任务停止执行,知道任务重新开始(start)

```node
var cron = require('node-cron');
 
var task = cron.schedule('* * * * *', () =>  {
  console.log('当前任务每分钟执行一次,直到停止');
});
 
// 停止执行当前任务
task.stop();
```

### Destroy

当前任务被停止,并且被完全销毁

```node
var cron = require('node-cron');
 
var task = cron.schedule('* * * * *', () =>  {
  console.log('删除当前任务,永远不能再开始');
});
 
// 删除当前任务
task.destroy();
```

### Validate

验证给定的字符串是不是一个可用 cron 表达式(expression)

```node
var cron = require('node-cron');
 
var valid = cron.validate('59 * * * *');
var invalid = cron.validate('60 * * * *');
```