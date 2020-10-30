# 题目地址

https://www.luogu.com.cn/problem/P3741

# 解答

水

```js
"use strict"
const rl = require('readline');
const rd = rl.createInterface({
  input:  process.stdin,
  output: process.stdout
})

let maxLine = 2;

const count = (s) => {
  const res = new String(s).match(/VK/gi);
  return res? res.length : 0;
}

rd.on('line', (line)=>{
  if( maxLine-- === 1) {
    let res = 0;
    res = Math.max(res, count(line));
    for( let i = 0 ; i < line.length; i++) {
      res = Math.max( res, count(line.slice(0,i) + 'V' + line.slice(i + 1, line.length)));
      res = Math.max( res, count(line.slice(0,i) + 'K' + line.slice(i + 1, line.length)));
    }
    console.log(res);
    rd.close();
  }
})
```