# 题目地址

https://leetcode-cn.com/problems/read-n-characters-given-read4-ii-call-multiple-times/

# 题目描述：用 Read4 读取 N 个字符II

给你一个文件，并且该文件只能通过给定的 read4 方法来读取，请实现一个方法使其能够读取 n 个字符。注意：你的 read 方法可能会被调用多次。


>read4 的定义：
>
>参数类型: char[] buf 
>
>返回类型: int
>
>注意: buf[] 是目标缓存区不是源缓存区，read4 的返回结果将会复制到 buf[] 当中。

下列是一些使用 read4 的例子：

>File file("abcdefghijk"); // 文件名为 "abcdefghijk"， 初始文件指针 (fp) 指向 'a' 
>
>char[] buf = new char[4]; // 创建一个缓存区使其能容纳足够的字符
>
>read4(buf); // read4 返回 4。现在 buf = "abcd"，fp 指向 'e'
>
>read4(buf); // read4 返回 4。现在 buf = "efgh"，fp 指向 'i'
>
>read4(buf); // read4 返回 3。现在 buf = "ijk"，fp 指向文件末尾

read 方法：

通过使用 read4 方法，实现 read 方法。该方法可以从文件中读取 n 个字符并将其存储到缓存数组 buf 中。您 不能 直接操作文件。

返回值为实际读取的字符。

>read 的定义：
>
>参数类型:   char[] buf, int n
>
>返回类型:   int
>
>注意: buf[] 是目标缓存区不是源缓存区，你需要将结果写入 buf[] 中。
 
示例：
>例 1：
>
>File file("abc");
>
>Solution sol;
>
>// 假定 buf 已经被分配了内存，并且有足够的空间来存储文件中的所有字符。
>
>sol.read(buf, 1); // 当调用了您的 read 方法后，buf 需要包含 "a"。 一共读取 1 个字符，因此返回 1。
>
>sol.read(buf, 2); // 现在 buf 需要包含 "bc"。一共读取 2 个字符，因此返回 2。
>
>sol.read(buf, 1); // 由于已经到达了文件末尾，没有更多的字符可以读取，因此返回 0。
>
>例 2：
>
>File file("abc");
>
>Solution sol;
>
>sol.read(buf, 4); // 当调用了您的 read 方法后，buf 需要包含 "abc"。 一共只能读取 3 个字符，因此返回 3。
>
>sol.read(buf, 1); // 由于已经到达了文件末尾，没有更多的字符可以读取，因此返回 0。


# 解答
同前一道题一样，这道题难就难在读不懂题目。。。

```cpp
// Forward declaration of the read4 API.
int read4(char *buf);

class Solution {
public:
    /**
     * @param buf Destination buffer
     * @param n   Number of characters to read
     * @return    The number of actual characters read
     */
    char* temp = new char[4];
    int index = 0;
    int count = 0;
    
    int read(char *buf, int n) {
        int i = 0;
        while( i < n){
            if( index == 0)
                count = read4( temp);
            if( count == 0)
                break;
            while( i < n && index < count)
                buf[i++] = temp[index++];
            if( index >= count)
                index = 0;
        }
        return i;
    }
};
```
