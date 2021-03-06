[00062 Unique Paths](https://leetcode.com/problems/unique-paths/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1：动态规划

### (1)具体思路：

动态规划的核心思路，将一个问题拆成多个子问题，找到最优子结构，同时记录之前子问题的结果，用于后续的计算。

对于一个m * n的矩阵，可以分解为，向右走的 m-1 * n 矩阵 和向下走的 m * (n -1) 的矩阵两个子问题，即存在最优子结构:

uniquePaths(m,n) = uniquePaths(m-1, n) + uniquePaths(m,n-1)

初始化当m =1 或者 n = 1 时， uniquePaths(m,n) = 1

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] grid = new int[m][n];
        for(int i = 0; i<m; i++){
            for(int j = 0; j<n; j++){
                if(i==0||j==0)
                    grid[i][j] = 1;
                else
                    grid[i][j] = grid[i][j-1] + grid[i-1][j];
            }
        }
        return grid[m-1][n-1];
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(m*n) | O(m*n) | 0ms | 31.9 m

## 思路2:  数学办法

### (1)具体解法

从开头到结尾，总共需要 m-1 向右的步骤， n-1 向下的步骤，即行走步骤转变为排列组合问题，结果为 $A_{m-1+n-1}^{n-1}$

例如 7*3的矩阵，需要6步向右（用R标识），需要2步向下(用D标识)，其中一条行进路线可以用如下序列表示：

D R R R D R R R
所有排列组合为  $A_{8}^{2} = 28$ 

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if( m == 1 || n == 1) return 1;
        if(m < n){
            int tmp = m;
            m = n;
            n = tmp;
        }
        long div = 1 , todiv =1;
        for (int i = 1; i < n ; i++) {
            div = div * i;
            todiv = todiv * ( m + n -1 - i );
        }
        return (int)(todiv / div);
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(min(m,n)) | O(1) | 0ms | 31.7 m


