[00056 Merge Intervals](https://leetcode.com/problems/merge-intervals/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：排序后遍历合并

### (1) 具体解法

先按照Interval 的上标进行排序，排序进行遍历，看当前Interval和下一个有没有重合，有重合修改end 取最大值，没有重合新加一个Interval

```java

class IntervalComparator implements Comparator<Interval>{
    public int compare(Interval o1, Interval o2) {
        return new Integer(o1.start).compareTo(o2.start) ;
    }
}

class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval>result = new ArrayList<>();
        if (intervals == null || intervals.size() == 0) return result;
        // 先对数组按照上标的升序排序
        Collections.sort(intervals, new IntervalComparator());
        int start = intervals.get(0).start, end = intervals.get(0).end;
        for(int i = 1 ; i < intervals.size(); i++) {
            // 如果存在交集，记录合并后最大的下标
            if (intervals.get(i).start <= end) {
                end = Math.max(end, intervals.get(i).end);
            }else {
                // 如果不存在交集,则结束合并，将当前合并结果放入数组
                Interval t = new Interval(start, end);
                result.add(t);
                //重新设置start, end 
                start = intervals.get(i).start;
                end = intervals.get(i).end;
            }
        }
        result.add(new Interval(start, end));
        return result;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(nlog(n)) | O(n) | 11ms | 45m
