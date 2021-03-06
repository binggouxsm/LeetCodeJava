# [00034 Find First and Last Position of Element in Sorted Array]()


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：二叉查询

### (1) 具体解法：

先运用二叉查找法，如果找不到返回\[-1,-1]
如果找到第一个目标元素后停止，然后向左向右遍历，直到第一个不等于目标的元素。

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int low = 0 ;
        int high = nums.length -1 ;
        int index = -1;
        while(low <= high) {
        	int mid = (low + high) / 2;
        	if (target == nums[mid]) {
        		index = mid;
        		break;
        	}else if( target < nums[mid]) {
        		high = mid -1;
        	}else {
        		low = mid +1;
        	}
        }
        if (index == -1) return new int[] {-1,-1};
        low =index; high =index;
        while(low >= 0 && nums[low] == target) {
        	low--;
        }
        while(high <nums.length && nums[high] == target) {
        	high++;
        }
        return new int[] {low+1,high-1};
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(log(n)) | O(1) | 3ms | 41.2MB

