[00130 Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

github地址：[LeetCodeJava](https://github.com/binggouxsm/LeetCodeJava)

## 错误思路：遍历

### (1) 具体解法

从外圈向内圈逐层递归遍历，遍历的过程中逐步扩展相临的节点

```java
class Solution {
    public void solve(char[][] board) {
        if(board.length == 0 || board[0].length == 0) return;
        List<Point> zeros = new ArrayList<>();
        recursive(board,0,0, board.length, board[0].length, zeros,true);
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                board[i][j] = 'X';
            }
        }
        for (int i = 0; i < zeros.size(); i++) {
            board[zeros.get(i).x][zeros.get(i).y] ='O';
        }

    }

    private void addZeros(char[][] board, int x, int y,List<Point> zeros,boolean first){
        if(board[x][y] == 'O'){
            Point t = new Point(x,y);
            if(first) {
                zeros.add(t);
                return;
            }
            for (int i = 0; i < zeros.size(); i++) {
                if(t.adjacent(zeros.get(i))){
                    zeros.add(t);
                    return;
                }
            }
        }
    }
// 从外圈到内圈循环遍历，第一圈先记录下所有O, 后面每次看与之前加入的O是否相邻，相邻则记录，如此循环只没有
    public void recursive(char[][] board, int x, int y, int n , int m, List<Point> zeros, boolean first){
        if(n <= 0 || m <= 0) return;
        for (int i = x; i < x + n; i++) {
//            System.out.print(board[i][y]);
            addZeros(board,i,y,zeros,first);
        }
        for (int i = y + 1; i < y + m; i++) {
//            System.out.print(board[x + n - 1][i]);
            addZeros(board,x + n - 1,i,zeros,first);
        }

        for (int i = x + n - 2; i >= x && m >=2; i--) {
//            System.out.print(board[i][y + m -1]);
            addZeros(board, i,y + m -1,zeros,first);
        }

        for (int i = y + m - 2; i > y ; i--) {
//            System.out.print(board[x][i]);
            addZeros(board, x,i,zeros,first);
        }

        recursive(board, x+1, y+1 , n - 2, m -2 , zeros, false);
    }
}

class Point{
    public int x;
    public int y;
    public Point(int x,int y){
        this.x = x;
        this.y = y;
    }

    public boolean equals(Object obj) {
        if(obj instanceof Point){
            return (this.x == ((Point)obj).x) && (this.y == ((Point)obj).y) ;
        }
        return false;
    }

    public boolean adjacent(Object obj){
        if(obj instanceof Point) {
            return (Math.abs(this.x - ((Point)obj).x) + Math.abs(this.y - ((Point)obj).y)) == 1;
        }
        return false;
    }
}
```

### (2)错误原因

遍历判断相邻时的顺序，与遍历顺序相反时，导致关联相邻的判断失败。如下图所示，从外圈逆时针遍历时，第二列第三行至第四行开始没有相邻，等到第5列时才判断相邻。如下图所示：

$$
  \begin{matrix}
O & X & O & O & X & X \\
O & X & X & X & O & X \\
X & O & O & X & O & O \\
X & O & X & X & X & X \\
O & O & X & O & X & X \\
X & X & O & O & O & O 
  \end{matrix} 
$$


## 思路：深度遍历

### (1) 具体解法：

先遍历外圈，找到O作为深度遍历的入口，以此为入口，深度递归遍历上下左右位置，如果为O，则继续遍历，如果不为O则停止继续遍历下去。

两个细节：

(1) 遍历判断当前节点的位置是否在有效取值范围内，避免在上下左右递归前判断当前位置是否有效，降低代码复杂和可读性
(2) 将目标位置O修改为S，能有效避免循环遍历，而且不占用额外空间。

```java
class Solution {
    public void solve(char[][] board) {
        if(board.length == 0 || board[0].length == 0) return;
        int N = board.length, M = board[0].length;
        // 最外圈开始进行深度遍历
        for (int i = 0; i < N; i++) {
            if(board[i][0] == 'O'){
                dfs(board,i,0,N,M);
            }
            if(board[i][M-1] == 'O'){
                dfs(board,i,M-1,N,M);
            }
        }
        for (int i = 1; i < M - 1; i++) {
            if(board[0][i] == 'O'){
                dfs(board,0,i,N,M);
            }
            if(board[N-1][i] == 'O'){
                dfs(board,N-1,i,N,M);
            }
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if(board[i][j] == 'S'){
                    board[i][j] = 'O';
                }else if(board[i][j] == 'O'){
                    board[i][j] = 'X';
                }
            }
        }
    }

    public  void dfs (char[][] board, int x, int y , int N, int M){
        if( x < 0 || y < 0 || x >= N || y >= M ) return;
        
        if(board[x][y] == 'O'){
            // 通过换个标记，保证不会重复遍历
            board[x][y] = 'S';
            // 接着向上下左右深度遍历
            dfs(board,x-1, y, N, M);
            dfs(board,x+1, y, N, M);
            dfs(board,x, y-1, N, M);
            dfs(board,x, y+1, N, M);
        }
    }
}
```

### (2) 复杂度：

时间复杂度| 空间复杂度 | 耗时 | 内存
--- | --- | --- | ---
O(N*M) | O(N*M) | 1ms | 41.3m


