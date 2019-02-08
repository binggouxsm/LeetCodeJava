# [00007 Reverse Integer](https://leetcode.com/problems/reverse-integer/)
github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：暴力解法
### （1）具体解法：

循环用数字%10取个位数，数字/10取下一个数字，取到的数字里面用于result计算，result = result * 10 + 取到的数字，无需堆栈。

注意点在于，1647483647这种原来在int范围内，反转后超出int范围内的这种情况，需特殊判断。

```java
class Solution {
    public int reverse(int x) {
        int pop, result = 0;
        while (x  != 0){
            pop = x % 10;
            x = x / 10;
            if(result > Integer.MAX_VALUE / 10 ||( result == Integer.MAX_VALUE / 10 &&  pop > 7)  ) return 0;
            if(result < Integer.MIN_VALUE / 10 || (result == Integer.MIN_VALUE / 10 &&  pop < -8)  ) return 0;
        	result = result * 10 + pop;
        }
        return result;
    }
}
```
### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(log(x)) | O(1) | 16ms | 27.1MB
