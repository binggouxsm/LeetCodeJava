[00104 Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 动态规划

### (1) 具体解法：

maxDepth(root) = 1 +Math.max( maxDepth(left) , maxDepth(right))

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return 1 + 
        Math.max((root.left!=null)?maxDepth(root.left):0 , 
        (root.right!=null)?maxDepth(root.right):0);
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 0ms | 40.4m

