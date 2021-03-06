[00079 Word Search](https://leetcode.com/problems/word-search/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 思路: 回溯法

### (1)具体思路:

先遍历数组找到等于第一个字符的作为回溯的入口，进入回溯的入口后尝试左右上下四个方向，不行的话回到上层，对于已经遍历的过的位置，用特殊字符替代，回溯时进行还原。

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        if (word.length() == 0) return true;
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                if(board[i][j] == word.charAt(0)){
                    char tmp = board[i][j];
                    board[i][j] = '&';
                    if(backtrack(board, i, j, word, 1))
                        return true;
                    board[i][j] = tmp;
                }
            }
        }
        return false;
    }

    public boolean backtrack(char[][] board, int x, int y, String word, int widx){
        if(widx == word.length()) return true;
        // 判断左的方向
        if(x > 0 && board[x-1][y] == word.charAt(widx)){
            char tmp = board[x-1][y];
            board[x-1][y] = '&';
            if(backtrack(board, x-1, y, word, widx+1))
                return true;
            board[x-1][y] = tmp;
        }

        // 判断右的方向
        if(x < board.length -1 && board[x+1][y] == word.charAt(widx)){
            char tmp = board[x+1][y];
            board[x+1][y] = '&';
            if(backtrack(board, x+1, y, word, widx+1))
                return true;
            board[x+1][y] = tmp;
        }

        // 判断上的方向
        if(y > 0 && board[x][y -1] == word.charAt(widx)){
            char tmp = board[x][y - 1];
            board[x][y - 1] = '&';
            if(backtrack(board, x, y - 1, word, widx+1))
                return true;
            board[x][y-1] = tmp;
        }

        // 判断下的方向
        if(y < board[x].length -1 && board[x][y + 1] == word.charAt(widx)){
            char tmp = board[x][y + 1];
            board[x][y + 1] = '&';
            if(backtrack(board, x, y + 1, word, widx+1))
                return true;
            board[x][y+1] = tmp;
        }

        return false;

    }
}
```

### (2) 复杂度：

M,N为board的长宽，W为字符的长度

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(M*N*2<sup>W</sup>) | O(W) | 5ms | 42.6m

