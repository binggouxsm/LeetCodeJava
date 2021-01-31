[00139 Word Break](https://leetcode.com/problems/word-break/)


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1 ：递归

### (1)具体解法

运用递归，对当前字符串s ，遍历wordDict，看当前字符串s是否以wordDict开头，是的话，截取开头后，继续下一轮递归

```java
class Solution {
    public static boolean wordBreak(String s, List<String> wordDict) {
        if( s.length() == 0) return true;
        boolean ret = false;
        for (String dict: wordDict){
            if(s.startsWith(dict) && wordBreak(s.substring(dict.length()), wordDict)){
                return true;
            }
        }
        return false;
    }
}
```

### (2) 复杂度：

L为s的长度，N为wordDict的个数， M为wordDict中字符串的最长长度

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(L * N * M) | O( L ) |  超时 | 超时导致无法故事

### (3)优化

由于中间结果没有缓存下来，导致重复计算

s="aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaab"
wordDict = ["a","aa","aaa","aaaa","aaaaa","aaaaaa","aaaaaaa","aaaaaaaa","aaaaaaaaa","aaaaaaaaaa"]

## 思路2：动态规划

### (1)具体解法

初始化一个s.length +1 的缓存 cache，用于存储每个子串是否可达的结果。cache[0] 为true。

如果存在cache[i - word.length()] 为true, 且word与 s.substring(i - word.length(), i )相同（ word为wordDict数组中一员），则
cache[i] = true, 否则为false

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] cache = new boolean[s.length()+1];
        cache[0] = true;
        // 初始化所有值为false
        for (int i = 1; i <= s.length(); i++) {
            cache[i] = false;
        }
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < wordDict.size() ; j++) {
                String word = wordDict.get(j);
                if (i - word.length() < 0 ) continue;
                if (cache[i - word.length()] == true && word.equals(s.substring(i - word.length(), i ))){
                    cache[i] = true;
                    break;
                }
            }
        }

        return cache[s.length()];
    }
}
```

### (2) 复杂度：

L为s的长度，N为wordDict的个数， M为wordDict中字符串的最长长度

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(L * N * M) | O( L ) |  2ms | 35.8MB
