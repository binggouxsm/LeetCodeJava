# [00014 Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：暴力解法

### (1) 具体解法

按照index ,逐个遍历字符串，每个字符串index位置的字符都相等时，则index++, 否则终止循环返回相同字符串结果

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) return ""; 
        
        int minlen = Integer.MAX_VALUE;
        for(int i = 0 ; i < strs.length; i++){
            minlen = Math.min(minlen,strs[i].length());
        }
        int index = 0;
        StringBuffer ret = new StringBuffer();
        while (index < minlen){
            for(int i = 1 ; i < strs.length; i++){
                if(strs[0].charAt(index) != strs[i].charAt(index)){
                    return ret.toString();
                }
            }
            ret.append(strs[0].charAt(index));
            index++;
        }
        return ret.toString();
    }
}
```

### (3) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n*minLen) | O(minLen) | 5ms | 38MB

n为字符串数组的长度， minLen是所有字符串中最短长度

### (4) 改进：

5 -7 行无需计算最小字符串长度
13行 终止条件为index == 长度或者 字符串不一致

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) return "";
        for (int i = 0; i < strs[0].length() ; i++){
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; j ++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c)
                    return strs[0].substring(0, i);             
            }
        }
        return strs[0];
    }
}
```

改进后的复杂度

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n*minLen) | O(1) | 5ms | 38MB

n为字符串数组的长度， minLen是所有字符串中最短长度



