# [00001 Two Sum](https://leetcode.com/problems/two-sum/)
github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)
## 思路一：暴力解法
1. 具体解法：遍历数组中所有数字两两相加，判断等于target

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0 ; i < nums.length; i++){
            for (int j = i + 1; j < nums.length; j++){
                if(nums[i] + nums[j] == target)
                    return new int[]{i,j};
            }
        }
        return null; 
    }
}
```

2. 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>2</sup>) | O(1) | 22ms | 27.6MB


## 思路二：HashMap
1. 具体解法：将数组按照按照\[值，下标\]的方式存入hashmap，遍历时，按照target - 值 查找下标，通过hashmap用空间O(n)换时间O(1)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> indiceMap = new HashMap<>();
        // 遍历数组
        for (int i = 0; i < nums.length ; i++){
            // 查找target - num[i]值在map中是否存在
            Integer mark = indiceMap.get(target - nums[i]);
            // 不存在则put Map
            if( mark == null){
                indiceMap.put(nums[i],i);
            }else{
                return new int[]{mark, i};
            }   
        }
        return null;
    }
}
```

2. 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 4ms | 27.5MB
