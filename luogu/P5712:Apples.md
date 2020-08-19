
# 题目地址
https://www.luogu.com.cn/problem/P5712

# 解答
水题，无任何意义。

```javascript
const rd = require('readline');

var rl = rd.createInterface({
    input: process.stdin,
    output: process.stdout
})

rl.on('line', (input) => {
    let num = parseInt( input, 10);
    console.log( `Today, I ate ${num} apple${num > 1 ? 's': ''}.`);
    rl.close();
})
```
