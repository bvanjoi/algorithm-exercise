# 题目地址
https://www.luogu.com.cn/problem/P5709

# 解答
练手题，单纯地用来熟悉 node.

注意：
- readline 输入的是一行字符串，如何转换为 Number.
- 注意题目的逻辑性：如果在给定的时间苹果全部吃完了，应该返回什么。

```javascript
const rd = require('readline');

var rl = rd.createInterface({
    input: process.stdin,
    output: process.stdout,
})

rl.on( 'line', ( l) => {
    var arr = l.split(' ');
    console.log( Math.floor( (arr[0] - arr[2]/arr[1]) > 0 ? arr[0] - arr[2]/arr[1]: 0));
    rl.close();
})
```
