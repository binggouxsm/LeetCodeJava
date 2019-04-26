[00094 Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 递归

### (1) 具体解法：

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<Integer>();
        recursiveTraversal(root, list);
        return list;
    }

    public void recursiveTraversal(TreeNode node, List<Integer> ret) {
        if (node == null) return;
        recursiveTraversal(node.left, ret);
        ret.add(node.val);
        recursiveTraversal(node.right, ret);
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(log(n)) - O(n) | 0ms | 36.3m


## 思路： 堆栈

### (1) 具体解法：

向左遍历不为空，则压栈，直到最左的元素出栈，再把右元素压栈

```java
public class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        Stack < TreeNode > stack = new Stack < > ();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(log(n)) - O(n) | 1ms | 36.2m


