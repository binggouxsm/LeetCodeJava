# [00011 Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1：暴力解法

### (1)具体解法：

遍历所有的两条线，找出面积最大的两根线

```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0;
        for (int i = 0 ; i < height.length; i++){
            for (int j = i + 1 ; j < height.length; j++){
                int area = Math.min(height[i], height[j]) * (j - i);
                max = (area > max) ? area : max;
            }
        }
        return max;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>2</sup>) | O(1) | 227ms | 29.8MB

### (3) 改进：

存在重复计算，避免掉(j - i) 小，且 height更小的计算

## 思路2：步长缩小的贪婪算法

### (1) 具体解法：

指针指向数组两头，然后在缩进指针时，保留长边用于计算，因为在同等步长下，长边的面积更大。

```java
class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0, l = 0, r = height.length - 1;
        while (l < r) {
            maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return maxarea;        
    }
}
```
### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 5ms | 29.2MB




