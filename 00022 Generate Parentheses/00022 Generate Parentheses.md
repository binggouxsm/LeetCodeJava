# [00022 Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)


github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路： 回溯法

### (1) 具体解法：

想象一个栈，压栈时字符串末尾添加左括号，出栈字符串末尾添加右括号

总的压栈次数为n，不同的压栈和出栈顺序，对应不同的字符串结果

```java
class Solution {
    public static List<String> generateParenthesis(int n) {
		List<String> result = new ArrayList<String>();
		recursiveGenParenthesis("",0, n , result);
        return result;
    }
    
    public static void recursiveGenParenthesis(String parenthesis,int stacklen, int left, List<String> result){
    	// 回溯退出条件，剩余压栈次数为0，栈为空
    	if(left == 0 && stacklen == 0) {
    		result.add(parenthesis);
    		return ;
    	}
    	// 压栈情况 
    	if(left > 0) {
    		recursiveGenParenthesis(parenthesis + "(", stacklen + 1, left - 1, result);
    	}
    	// 出栈情况
    	if(stacklen > 0 ) {
    		recursiveGenParenthesis(parenthesis + ")", stacklen - 1, left, result);
    	}
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(2<sup>n</sup>) | O(2<sup>n</sup>) | 1ms | 37.9MB
