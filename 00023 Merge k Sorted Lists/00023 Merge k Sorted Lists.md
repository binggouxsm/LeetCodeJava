# [00023 Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1：递归

### (1) 具体解法:

参考 00021 Merge Two Sorted Lists 的递归实现，在当前指针中找最小的值对应的指针进行返回，最小指针对应的下一节点，在下一递归中计算产生。

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        
        int min = Integer.MAX_VALUE, minindex = -1, i = -1;
        for(i = 0 ; i < lists.length; i++){
            if(lists[i] != null && lists[i].val < min){
                min = lists[i].val;
                minindex = i;
            }
        }
        if (minindex == -1) return null;
        
        ListNode head = lists[minindex]; 
        lists[minindex] = lists[minindex].next;
        head.next = mergeKLists(lists);
        return head;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(k*k*len) | O(k*len) | 172ms | 40.2MB

### (3) 改进：

第5-10行找最小值的排序存在重复计算，在第一轮找到最小值的结果，在下一层递归中没法重复应用





