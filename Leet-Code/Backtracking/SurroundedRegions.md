# Surrounded Regions
https://leetcode.com/problems/surrounded-regions/

```java
class Solution {
    public void solve(char[][] board) {
        
        if (board == null || board.length == 0 ) {return;}
        
        for(int r = 0; r < board.length; r++) {
            bfs(board, r, 0);
            bfs(board, r, board[0].length-1);
        }
        for(int c = 0; c < board[0].length; c++) {
            bfs(board, 0, c);
            bfs(board, board.length-1, c);
        }
        
        for(int r = 0; r < board.length; r++) {
            for( int c = 0; c < board[0].length; c++) {
                if( board[r][c] == 'O' ) { board[r][c] = 'X';}
                if ( board[r][c] == 'T' ) { board[r][c] = 'O';}
            }
        }
        return;

    }
    
    public void bfs(char[][] board, int r, int c) {
        if(r<0 || c<0 || r>=board.length || c>=board[0].length || board[r][c] == 'X') {
            return;
        }
        if(board[r][c] == 'O') {
            board[r][c] = 'T';
            bfs(board, r+1, c);
            bfs(board, r-1, c);
            bfs(board, r, c+1);
            bfs(board, r, c-1);
            
        }
        return;
    }
}
```
