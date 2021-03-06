[00003 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路1：暴力解法

### (1) 具体解法: 
遍历所有可能的子串，判断是否有重复字符

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int longest = 0;
        // 遍历字符串
        for( int i = 0 ; i < s.length(); i++){
            // HashSet记录是否存在重复字符
            Set<Character> set = new HashSet<>();
            set.add(s.charAt(i));
            // 遍历后续字符串，不重复则加入HashSet，重复则退出循环
            for(int j = i + 1; j < s.length(); j++){
                if( set.contains(s.charAt(j))){
                    break;
                }else{
                    set.add(s.charAt(j));
                }
            }
            if(set.size() > longest){
                longest = set.size(); 
            }
        }
        return longest;
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>3</sup>) | O(n) | 94ms | 27.8MB

备注：hashset.contains的计算逻辑为按照对象的hashcode去比对set中所有的hashcode，如果都不一样则不存在，如果一样，则调用对象的equals方法比对，如果不一样则，不存在，一样则存在，所以为O(n)时间复杂度

### (3) 改进：

存在重复计算，例如 abcabcbb 当从0开始，计算abc最长，再加入a后出现重复字符，接下来从1开始，可以复用bc不同的结果，减少重复计算

## 思路2：滑动窗口

### (1)具体解法：

充分利用之前的计算不重复的结果，set中存放不重复字符，当窗口的末尾位置的字符如果不在set中，则末尾位置+1,末尾字符加入set中；如果重复，则移除窗口开头位置的字符，开头位置+1； 当末尾位置超出字符长度，没有计算长度，需要补计算一次长度 

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashSet<Character> set = new HashSet<>();
        int i = 0, j = 0, longest = 0;
        while ( i < s.length() && j < s.length()){
            // 如果set包含，则去掉头个字符，开头位置+1
            if(set.contains(s.charAt(j))){
                longest = Math.max(longest, j - i);
                set.remove(s.charAt(i));
                i++;
            // 如果set不包含则加入set,接着结尾位置+1，判断下一个字符    
            }else{
                set.add(s.charAt(j));
                j++;
            }
        }
        // 当j直接超过s.length()，没有计算最长值，需补充计算一次
        return Math.max(longest, j - i);
    }
}
```

变种：将计算长度纳入不包含的往set中插值的计算逻辑中，每次计算,避免因为超过字符长度时，需额外计算一次；

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashSet<Character> set = new HashSet<>();
        int i = 0, j = 0, longest = 0;
        while ( i < s.length() && j < s.length()){
            // 如果set包含，则去掉头个字符，开头位置+1
            if(set.contains(s.charAt(j))){
                set.remove(s.charAt(i++));
            // 如果set不包含则加入set,接着结尾位置+1，判断下一个字符    
            }else{
                set.add(s.charAt(j++));
                longest = Math.max(longest, j - i);
            }
        }
        return longest;
    }
}
```

### (2) 复杂度：
时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n<sup>2</sup>) | O(n) | 29ms | 25.5MB


### (3) 改进
开头位置的不止+1，而是跳相同字符同样的位置

### 思路3：改进步长的滑动窗口

Todo: 


