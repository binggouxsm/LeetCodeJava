[00122 Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 遍历

### (1) 具体解法：

遍历每个价格和前一个价格，加总每个利润差

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <= 1) return 0;

        int maxprofit = 0;
        for (int i = 1; i < prices.length; i++) {
            if(prices[i] - prices[i-1] >0)
                maxprofit += prices[i] - prices[i-1];
        }
        return maxprofit;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(1) | 1ms | 35.7m