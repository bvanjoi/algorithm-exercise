# 题目地址
https://leetcode-cn.com/problems/implement-strstr/

# 题目描述：实现 strStr()
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例：
>例 1:
>
>输入: haystack = "hello", needle = "ll"
>
>输出: 2
>
>例 2:
>
>输入: haystack = "aaaaa", needle = "bba"
>
>输出: -1


# 解答
方法一：直接调用库函数

虽然快，但无意义。

代码：
```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        return haystack.find( needle);
    }
};
```


方法二：朴素的字符串匹配方法。

遍历字符串 haystack, 设置两个变量 i,k, 并初始化 i = 0, k = 0, 其中 i 为遍历 haystack 的变量。 

对于每一个字符 haystack[i], 检查是否等于 needle[k], 若不想等，则 i++ 继续遍历； 若相等，则检查 haystakc[++i] == needle[++k] ,...., 直到 k 等于 needle 的长度，此时返回 i.

若遍历结束仍然没有匹配的字串，则返回 -1.

代码：
```cpp
class Solution {
public:
    //最简单直观的匹配方法, 时间复杂度为O(n^2)
    bool isRight( string& haystack, string& needle, int begin){
        for( int i = begin, k = 0; k < needle.size(); i++,k++)
            if( haystack[i] != needle[k])
                return false;
        return true;
    }
    int strStr(string haystack, string needle) {
        if( haystack.size() < needle.size())
            return -1;
        
        for( int i = 0; i <= haystack.size() - needle.size(); i++)
            if( isRight( haystack, needle, i)){
                return i;
            }
            
        return -1;
    }
};
```

方法三：KMP算法。

该算法由 D.E.Knuth，J.H.Morris 和 V.R.Pratt 三个人提出，因此选择三个人名字的头一个字母作为名称。

（Knuth 便是《计算机程序设计艺术》的作者——高德纳，一位享誉全球的计算机科学家）

KMP 是在线性时间内解决字符串匹配的算法。

首先给出 KMP 的操作步骤：给定文本串 S 和模式串 P, 实现 S.find( P).

1. 假定现在位于文本串 S 的第 i 个位置，位于模式串 P 的第 j 个位置；
2. 若 j == -1, 或当前匹配成功(S[i] == P[j]), 令 i++, j++, 继续匹配下一个字符；
3. 若 j != -1, 且当前字符串匹配失败，则令 i 不变，j = next[j]. 这意味着匹配失败时，模式串 P 会相对于文本串 P 向右移动了 j - next[j] 个位置。（换而言之，模式串 P 的匹配失败位置的 next 数组的值对应模式串 P 的索引位置移动到匹配失败处）

当然，以上过程是不容易理解的。我们用图例说明：

给定文本串 S = "acabaabaabcaccaabc", 模式串 P = "abaabcac".

我们先来看 next 数组的构造过程。

首先，有两个定义需要搞明白。前缀/后缀：前缀指的是除了最后一个字符串之外，一个字符串的全部头部组合；后缀指的是除了第一个字符之外，一个字符串的全部末尾组合。

我们需要获得相等的前缀后缀的最大长度。算出每个 index 下的最长长度构成最长长度数组 max_len, 最后通过 max_len 左侧添加元素 -1 并集体右移一位来得到 next 数组。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912094917846.png?)

接下来来到匹配过程，来看以下图例：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912100702273.png?)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912100718847.png?)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019091210073733.png?)


代码：
```cpp
class Solution {
public:
    vector<int> getNext( string& needle){
        //构建 next 数组
        vector<int> next( needle.size() + 1, 0);
        next[0] = -1;
        for( int i = 0, j = -1; i < needle.size(); ){
            if( j == -1 || needle[i] == needle[j]){
                i++, j++;
                next[i] = j;
            }
            else
                j = next[j];
        }    
        return next;
    }
    
    int strStr(string haystack, string needle) {
        vector<int> next = getNext( needle);
 
        int i = 0, j = 0;
        while(i < (int)haystack.size() && j < (int)needle.size() ){ //若没有强制类型转换，则 -1 为最大数
            if( j == -1 || haystack[i] == needle[j])
                i++, j++;
            else
                j = next[j];
        }
        
        if( j == needle.size())
            return i - j;
        
        return -1;
    }
};
```
