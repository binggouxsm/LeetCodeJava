# [00005 Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1： 转换成查两个子串中相同的字符
### (1)具体解法：
将字符串反转后，查找原字符( s )和反转后字符( r )最长的相同字符且最长字符的下标与反转前的下标保持一致。
例如 “aacdefcaa”， 反转字符为 “aacfedcaa” ,运用动态规划，
步骤1：初始化如下矩阵，横轴为原始字符，纵轴为反转字符
初始化矩阵第一行，如果s\[x] == r\[0] 则 dp\[0]\[x] =1 否则为0；
初始化矩阵第一列，如果s\[0] == r\[y] 则 dp\[y]\[0] =1 否则为0；
$$
 \begin{bmatrix}
      & a & a & c & d & e & f & c & a & a \\
   a & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 1  & 1 \\
   a & 1 \\
   c & 0 \\
   f & 0 \\
   e & 0 \\
   d & 0 \\
   c & 0 \\
   a & 1 \\
   a & 1 \\
  \end{bmatrix}
$$

步骤2： 逐步计算dp矩阵值
如果 s\[x] == r\[y] 则 dp\[x]\[y] =  dp\[x - 1]\[y - 1] + 1
$$
 \begin{bmatrix}
      & a & a & c & d & e & f & c & a & a \\
   a & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 1  & 1 \\
   a & 1 & 2 & 0 & 0 & 0 & 0 & 0 & 1  & 2 \\
   c & 0 & 0 & 3 & 0 & 0 & 0 & 1 & 0  & 0 \\
   f & 0 \\
   e & 0 \\
   d & 0 \\
   c & 0 \\
   a & 1 \\
   a & 1 \\
  \end{bmatrix}
$$
在计算的同时找出最大值，除了最大值的条件之外，还需满足最长字符的下标与反转前的下标保持一致。
纵轴开始和结束位置 y - dp\[y]\[x] +1 , y
横轴开始和结束位置 x - dp\[y]\[x] +1 , x
按照位置对应得到如下关系： s.len - 1 - y = x - dp\[y]\[x] +1

步骤3：考虑额外情况，当空或者空字符，或者字符长度为1时。

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";
        // 对字符串进行反转, 问题转换为找两个字符串最长相同子串的动态规划问题
        String reverse = new StringBuffer(s).reverse().toString();
        int dp[][] = new int[s.length()][s.length()];
        // 初始化矩阵第一行，s[x] == r[0] 则 dp[0][x] =1 否则为0
        for ( int x = 0 ; x < s.length(); x++){
            dp[0][x] = (s.charAt(x) == reverse.charAt(0))? 1 : 0;
        }
        // 初始化矩阵第一列，如果s[0] == r[y] 则 dp[y][0] =1 否则为0
        for ( int y = 0 ; y < s.length(); y++){
            dp[y][0] = (s.charAt(0) == reverse.charAt(y))? 1 : 0;
        }
        
        int max = 1, maxx = 0 , maxy = 0;
        for ( int x = 1 ; x < s.length(); x++){
            for ( int y = 1 ; y < s.length(); y++){
                if (s.charAt(x) == reverse.charAt(y)){
                    dp[y][x] = dp[y - 1][x - 1] + 1;
                    // 满足最长字符的下标与反转前的下标保持一致
                    if(dp[y][x] > max && (s.length() == x + y - dp[y][x] + 2 )){
                        max = dp[y][x];
                        maxx = x;
                        maxy = y;
                    }
                }else{
                    dp[y][x] = 0;
                }
            }
        }
        return reverse.substring(maxy - max + 1 , maxy +1); 
    }
}
```

### (2) 复杂度：
时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>2</sup>) | O(n<sup>2</sup>) | 128ms | 44.9MB
