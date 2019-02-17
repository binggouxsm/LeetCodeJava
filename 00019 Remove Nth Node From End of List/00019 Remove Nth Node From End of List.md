# [00019 Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：双指针一次遍历

### (1) 具体解法:

用两个指针标识位置，第一个指针遍历n次循环，指向下一节点，然后第二个指针指向head，之后两个指针一起指向下一个节点，直到第一个节点指向空

例外判断情况：第一个指针遍历n次循环，指向下一节点后，若节点为空，因为保证n为有效值，所以直接返回head.next

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode current = head ; ListNode pre = null;
        // 第一个指针遍历n次循环，指向下一节点
        for (int i = 0 ; i < n ; i++){
            current = current.next;
        }
        // 若节点为空，因为保证n为有效值，所以直接返回head.next
        if(current == null) return head.next;
        // 第二个指针指向head
        pre = head;
        // 两个指针一起指向下一个节点，直到第一个节点next指向空
        while (current.next != null){
            current = current.next;
            pre = pre.next;
        }
        // 删除目标节点
        pre.next = pre.next.next;
        return head;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 6ms | 35.5MB

