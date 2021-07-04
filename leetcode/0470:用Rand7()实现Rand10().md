# 题目地址

<https://leetcode-cn.com/problems/implement-rand10-using-rand7/>

# 解答

有意思的数学题。

下述方法效率并不高。

```rust
/** 
 * The rand7() API is already defined for you.
 * @return a random integer in the range 1 to 7
 * fn rand7() -> i32;
 */

impl Solution {
    pub fn rand10() -> i32 {
        let mut sum = 0;
        for i in 0..10 {
            sum += rand7();
        }
        // sum is [10, 70]
        // 10 - sum % 10 is [1,10] 足够均匀
        10 - sum % 10
    }
}
```
