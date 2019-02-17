# [00021 Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：链表合并

### (1) 具体思路

设置一个dummyhead，设置pre指针指向head，然后两个指针p,q分别指向l1,l2，当p,q不为空时，判断p.val, q.val的大小，如果p.val小,则pre.next 指向p，然后p指向下一节点。反之亦然。

当p,q中一条链表遍历完毕，则pre.next指向剩余的链表即可

最终返回dummyhead.next

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        
        ListNode dummyhead = new ListNode(0) , p = l1, q = l2, pre = dummyhead;
        
        while(p != null && q != null){
            if(p.val <= q.val){
                pre.next = p;
                p = p.next;
            }else{
                pre.next = q;
                q = q.next;
            }
            pre = pre.next;
        }
        
        if(p != null) pre.next = p;
        if(q != null) pre.next = q;
        
        return dummyhead.next;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 6ms | 41.3MB


## 思路2： 递归

### (1) 具体解法

这个看别人提交的，代码的思路能理解，很难直观想到。
每次递归解决当前节点应该返回哪个节点，同时将下一节点的指向交由下一层的递归处理。

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2){
		if(l1 == null) return l2;
		if(l2 == null) return l1;
		if(l1.val < l2.val){
			l1.next = mergeTwoLists(l1.next, l2);
			return l1;
		} else{
			l2.next = mergeTwoLists(l1, l2.next);
			return l2;
		}
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 6ms | 41.3MB
