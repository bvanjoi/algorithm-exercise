
# 题目地址
https://www.luogu.com.cn/problem/P4956

# 解答
水。

```javascript
const fl = require('readline');
const fd = fl.createInterface({
  input: process.stdin,
  output:process.stdout
})

fd.on('line', ( input) => {
  let num = parseInt(input, 10);
  for( let x = 100; x > 0; x--){
    if( (num - 364 * x) % 1092 === 0 && (num - 364 * x) / 1092 > 0) {
      console.log( x)
      console.log((num - 364 * x) / 1092);
      break;
    }
  }
  fd.close();
})
```
