[00066 Plus One](https://leetcode.com/problems/plus-one/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 遍历

### (1) 具体做法

从后往前遍历，算是否进位，不需进位则退出循环，如需进位则接着循环。判断退出时，是否遍历到头而且还需要进位，如果需要进位，则新建一个数组，首位置1即可，因为后面肯定都是0

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int push, i = digits.length -1;
        do{
            int tmp = digits[i] + 1;
            push = tmp / 10;
            digits[i] = tmp % 10;
            i--;
        }while( i >= 0 && push == 1);

        if(i == -1 && push == 1){
            int[] ret = new int[digits.length+1];
            ret[0] = 1;
            return ret;
        }
        return digits;
        
    }
}

```

网上更简单的写法:

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        for(int i = n - 1; i >= 0; i--) {
            if(digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            digits[i] = 0;
        }

        int[] newNumber = new int [n+1];
        newNumber[0] = 1;
        return newNumber;
    }
}
```
### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 0ms | 37.3m

