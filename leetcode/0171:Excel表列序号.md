
# 题目地址

https://leetcode-cn.com/problems/excel-sheet-column-number/

# 题目描述：Excel表列序号
给定一个Excel表格中的列名称，返回其相应的列序号。

例如，
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```
示例：
>例 1:
>
>输入: "A"
>
>输出: 1
>例 2:
>
>输入: "AB"
>
>输出: 28
>例 3:
>
>输入: "ZY"
>
>输出: 701

# 解答
这道题本质上属于进制转换：二十六进制转十进制。

注意不要溢出即可。

```cpp
class Solution {
public:
    int titleToNumber(string s) {
        long res = 0, base = 1;
        for( int i = s.size() - 1; i > -1; i--)
            res += (s[i] - 'A' + 1) * base, base *= 26;
        return res;
    }
};
```
