[00101 Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 递归

### (1) 具体解法

一棵树左右两个节点，左边节点的值等于右边节点的值，同时左边节点的左节点 与 右边节点的 右节点 递归下去相等，  同时左边节点的右节点 与 右边节点的 左节点 递归下去相等。则这课树左右对称

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return recursiveSymmetric(root, root);
    }

    public boolean recursiveSymmetric(TreeNode left, TreeNode right){
        if (left == null && right == null) return true;
        if (left == null || right == null) return false;
        return (left.val == right.val)
                && recursiveSymmetric(left.left, right.right)
                && recursiveSymmetric(left.right, right.left);
    }
}

```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 0ms | 39.5m

