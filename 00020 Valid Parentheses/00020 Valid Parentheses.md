# [00020 Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路：栈方式

### (1) 具体解法：

遍历字符串，当遇到 左符号时用右符号压栈，遇到右符号出栈，看出栈符号与当前是否一致，最后判断栈是否为空

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (char c : s.toCharArray()) {
            if (c == '(')
                stack.push(')');
            else if (c == '{')
                stack.push('}');
            else if (c == '[')
                stack.push(']');
            else if (stack.isEmpty() || stack.pop() != c)
                return false;
        }
        return stack.isEmpty();         
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(n) | O(n) | 4ms | 34.6MB


