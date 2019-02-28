# [00048 Rotate Image](https://leetcode.com/problems/rotate-image/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：上下颠倒，对角线换位

### (1) 具体解法

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        // 先上下对着颠倒
        for(int i = 0; i <  n / 2; i++) {
        	for (int j = 0 ; j < n; j++) {
        		int tmp = matrix[i][j];
        		matrix[i][j] = matrix[n - 1 - i][j];
        		matrix[n - 1 - i][j] = tmp;
        	}
        }
        // 沿对角线颠倒
        for(int i = 0; i <  n ; i++) {
        	for (int j = i+1 ; j < n; j++) {
        		int tmp = matrix[i][j];
        		matrix[i][j] = matrix[j][i];
        		matrix[j][i] = tmp;
        	}
        }
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>2</sup>) | O(n<sup>2</sup>) | 1ms | 37.4MB
