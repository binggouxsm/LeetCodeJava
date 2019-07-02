[00136 Single Number](https://leetcode.com/problems/single-number/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1 ：加减法

### (1)具体解法

2* 去重后的和 - 所有值的和

```java
class Solution {
    public int singleNumber(int[] nums) {
        Set <Integer> numSet = new HashSet<>();
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            numSet.add(nums[i]);
        }
        int setsum = 0;
        Iterator<Integer> iterator = numSet.iterator();
        while (iterator.hasNext()){
            setsum += iterator.next();
        }

        return  2* setsum - sum;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(N) | O(N) |  6ms | 39.7MB

## 思路2： 异或

### （1）具体解法

利用异或运算

a XOR 0 = a

a XOR a = 0

```java
class Solution {
    public int singleNumber(int[] nums) {
        int a = 0;
        for (int i = 0; i < nums.length; i++) {
            a = a ^ nums[i];
        }
        return a;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(N) | O(1) | 0ms | 38.7MB




