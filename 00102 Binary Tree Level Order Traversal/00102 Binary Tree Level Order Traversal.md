[00102 Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路；递归

### (1)具体解法

中序递归遍历的基础上，增加层级序号

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        recursiveLevelOrder(root, 0 , ret);
        return ret;
    }

    public void recursiveLevelOrder(TreeNode node, int level, List<List<Integer>> ret){
        if(node == null) return;
        if(ret.size() <= level){
            ret.add(new ArrayList<Integer>());
        }
        ret.get(level).add(node.val);
        recursiveLevelOrder(node.left, level+1 , ret);
        recursiveLevelOrder(node.right, level+1 , ret);
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 0ms | 39.5m

