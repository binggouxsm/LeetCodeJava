# [00041 First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1：位运算（错误解法）

### (1) 具体解法：

正常遍历之后，记录那些整数有，那些整数没有，但是这个是空间复杂度O(n)，不符合题目要求，所以考虑用位运算压缩空间复杂度为O(1)

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        long bytemap = 0l;
        for(int i = 0 ; i < nums.length; i++){
            if (nums[i] <= nums.length && nums[i] > 0){
                bytemap = bytemap | (1 << (nums[i] - 1));
            }
        }
        int ret = 1;
        while(bytemap % 2 == 1){
            bytemap = bytemap >> 1;
            ret++;
        }
        return ret;
    }
}
```

已经考虑位运算最长的长度为，采取long运算，最长为64位。果然还是没有通过测试，当数组长度为65以上时，没有通过测试，T^T。


### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 


## 思路2：用下标计数

### (1)具体解法

中心思想，是用下标记录，是否目标值是否存在；遍历数组时，当在i位置找到1时，将替换num\[i] 与num\[0]进行替换

注意由于元素替换，导致可能元素漏检查，所以下标自增需要等确认替换后的元素不符合要求之后再替换

最后遍历所有数组，找nums\[i] != i+1 的下标，返回下标+1

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for(int i = 0 ; i < nums.length; ){
            if(nums[i] <= nums.length && nums[i] > 0 && nums[nums[i] -1 ] != nums[i] ){
                int tmp = nums[i];
                nums[i] = nums[tmp -1 ];
                nums[tmp -1] = tmp;
            }else{
                i++;
            }
        }
        for(int i = 0 ; i < nums.length; i++){
            if(nums[i] != i+1)
                return i+1;
        }
        return nums.length+1;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 5ms | 37.2MB



