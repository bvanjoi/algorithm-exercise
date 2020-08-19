# 题目地址

https://leetcode-cn.com/problems/group-anagrams/

# 题目描述：Pow(x, n)

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例：
>例 1:
>
>输入: 2.00000, 10
>
>输出: 1024.00000
>
>例 2:
>
>输入: 2.10000, 3
>
>输出: 9.26100
>
>例 3:
>
>输入: 2.00000, -2
>
>输出: 0.25000
>
>解释: 2-2 = 1/22 = 1/4 = 0.25


# 解答
方法一：用库函数，直接``return pow(x, n);``, 当然，这样做没有任何意义。

方法二：遍历。通过循环将 x 自乘 n 次，时间复杂度为 O(n). 该算法运行时间有点长。

方法三：递归。

求数值 x 的 n 次幂，其中必定有重复的项，例如 n > 1 且 n 为偶数时，pow( x, n/2) * pow( x, n/2) == pow( x, n), 此时乘数与被乘数是相同的，我们只需要计算一次就好。

代码：
```cpp
class Solution {
public:
    double myPow(double x, int n) {
        //两个基准情况
        if( n == 0)
            return 1;
        if( n == -1)
            return 1/x;
        
        //当 n 为奇数时
        if( n % 2)
            return x * myPow( x, n - 1);
        //当 n 为偶数时
        double temp = myPow(x, n / 2);  //设置该变量是为了减少递归次数
        return temp * temp;
    }
};
```

