
# 题目地址

https://leetcode-cn.com/problems/excel-sheet-column-title/

# 题目描述：Excel表列名称
给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```
示例：
>例 1:
>
>输入: 1
>
>输出: "A"
>
>例 2:
>
>输入: 28
>
>输出: "AB"
>
>例 3:
>
>输入: 701
>
>输出: "ZY"


# 解答
这道题本质上属于进制转换：十进制转二十六进制。

注意好细节处理即可。

```cpp
class Solution {
public:
    string convertToTitle(int n) {
        string res = "";
        while( n > 0){
            if( n % 26 == 0)
                res += 'Z', n/=27;
            else
                res += (n % 26) - 1 + 'A', n /= 26;
        }
        reverse( res.begin(), res.end());
        return res;
    }
};
```
