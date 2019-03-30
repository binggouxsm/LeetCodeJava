[00070 Climbing Stairs ](https://leetcode.com/problems/climbing-stairs/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：动态规划

### (1)具体解法

问题拆分找出最优子结构

ways(n) = ways(n-1) + ways(n-2)

初始化 ways(1) = 1 , ways(2) = 2

```java
class Solution {
    public int climbStairs(int n) {
        int[] ret = new int[(n>2)? n:2];
        ret[0] = 1;
        ret[1] = 2;
        for (int i = 2; i < n; i++) {
            ret[i] = ret[i-1] + ret[i-2];
        }
        return ret[n-1];
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 0ms | 31.6m