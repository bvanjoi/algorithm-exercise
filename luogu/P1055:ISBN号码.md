# 题目地址
https://www.luogu.com.cn/problem/P1055

# 解答
阅读理解题。

这里需要注意两点：
- js 中 String 类型不可被修改。
- js 中运算符优先级。

```JavaScript
const rd = require('readline');
var rl = rd.createInterface({
    input: process.stdin,
    output: process.stdout
})
rl.on( 'line', (input) => {
    var test = 0;
    for( let i = 0, count = 0; i < input.length - 2; i++) {
        if( input[i] !== '-'){
            test += parseInt(input[i],10) * (i+1-count);
        }
        else {
            count++;
        }
    }
    if( test % 11 === 10 ? input[input.length - 1] === 'X' : test % 11 === parseInt(input[ input.length - 1], 10)) {
        console.log( "Right");
    }
    else {
        console.log( input.slice(0, input.length - 1) + (test%11 === 10 ? 'X' : test%11));
    }
    rl.close();
})
```
