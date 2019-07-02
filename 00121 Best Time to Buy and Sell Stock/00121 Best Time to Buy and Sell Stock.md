[00121 Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 遍历

### (1) 具体解法：

遍历的同时记录下最小值，后续计算当前值和最小值的差是否大于maxprofit，是的话更新maxprofit

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <= 1) return 0;

        int maxprofit = 0, minprice = prices[0];
        for (int i = 1; i < prices.length; i++) {
            if(prices[i] <= minprice){
                minprice = prices[i];
            }else if(prices[i] - minprice > maxprofit){
                maxprofit = prices[i] - minprice;
            }

        }
        return maxprofit;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 1ms | 35.9m
