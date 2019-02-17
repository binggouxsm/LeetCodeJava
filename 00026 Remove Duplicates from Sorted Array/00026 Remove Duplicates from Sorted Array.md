# [00026 Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：暴力解法

### (1)具体解法：

初始化len =1, nonduplicate = nums\[0]

从1开始遍历数组，如果num\[i] != nonduplicate 则单方面调换位置，len++

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int len = 1 , nonduplicate = nums[0];
        for (int i = 1; i < nums.length; i++){
            if(nums[i] != nonduplicate){
                nums[len] = nums[i];
                nonduplicate = nums[len];
                len++;
            }
        }
        return len;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 6ms | 39.5MB

