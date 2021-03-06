# [00054 Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：递归

### (1) 具体解法

采用递归的思路，每次递归，只遍历外圈元素，按照上右下左的顺利，遍历外圈，然后一直递归下去，直到没有长度

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
		List<Integer>ret = new ArrayList<Integer>();
        if(matrix.length == 0 || matrix[0].length == 0) return ret;
		traverse(0,0,matrix.length,matrix[0].length, matrix, ret);
        return ret;
    }
	
	public void traverse(int x, int y , int m , int n , int[][] matrix, List<Integer> ret) {
		if (m <= 0 || n <= 0) return;
    // 遍历上边
		for (int i = 0 ; i < n; i++) {
			ret.add(matrix[x][y+i]);
		}
    // 遍历右边
		for (int i = 1 ; i < m; i++) {
			ret.add(matrix[x+i][y+n -1]);
		}
		if(m > 1) {
      // 遍历下边
			for (int i = 1 ; i < n ; i++) {
				ret.add(matrix[x+m - 1][y+n - 1-i]);
			}
		}
		if(n > 1) {
      // 遍历左边
			for (int i = 1 ; i < m - 1  ; i++) {
				ret.add(matrix[x +m - 1 - i][y]);
			}
		}
    // 递归遍历下一层
		traverse(x+1, y+1, m -2, n -2, matrix , ret);
	}
}
```
### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(m*n) | O(m*n) | 1ms | 37.2MB

### (3) 改进方案

采用同样的思路，用两个指针代替函数递归

```java
class Solution {
    public List < Integer > spiralOrder(int[][] matrix) {
        List ans = new ArrayList();
        if (matrix.length == 0)
            return ans;
        int r1 = 0, r2 = matrix.length - 1;
        int c1 = 0, c2 = matrix[0].length - 1;
        while (r1 <= r2 && c1 <= c2) {
            for (int c = c1; c <= c2; c++) ans.add(matrix[r1][c]);
            for (int r = r1 + 1; r <= r2; r++) ans.add(matrix[r][c2]);
            if (r1 < r2 && c1 < c2) {
                for (int c = c2 - 1; c > c1; c--) ans.add(matrix[r2][c]);
                for (int r = r2; r > r1; r--) ans.add(matrix[r][c1]);
            }
            r1++;
            r2--;
            c1++;
            c2--;
        }
        return ans;
    }
}
```
时间复杂度和空间复杂度与之前一致
