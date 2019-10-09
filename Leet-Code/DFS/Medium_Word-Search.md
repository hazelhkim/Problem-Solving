# Word Search

<img width="554" alt="Screen Shot 2019-10-09 at 5 06 30 PM" src="https://user-images.githubusercontent.com/46575719/66520456-2f994780-eab7-11e9-9eaf-f91752dbe8df.png">


#### My Answer

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] arr = word.toCharArray();
       for(int r = 0; r < board.length; r++) {
           for(int c = 0; c < board[0].length; c++) {
               if(board[r][c] == arr[0]){
                   if(dfs(board, arr, r, c, 0)) {return true;}
               }
           }
       }
        return false;
    }
    
    private boolean dfs(char[][] board, char[] arr, int r, int c, int count) {
        if(count == arr.length) {return true;}
        if(r < 0 || c<0 || r >= board.length || c>= board[0].length) {return false;}
        
        if(board[r][c] == arr[count]) {
            char ch = arr[count];
             board[r][c] = '#';
             if(dfs(board, arr, r+1, c, count+1) || dfs(board, arr, r-1, c, count+1) || dfs(board, arr, r, c+1, count+1) || dfs(board, arr, r, c-1, count+1)) {return true;}
            board[r][c] = ch;
        }
        return false;
    }
}

```
<img width="533" alt="Screen Shot 2019-10-09 at 5 06 35 PM" src="https://user-images.githubusercontent.com/46575719/66520449-2c9e5700-eab7-11e9-899b-c57307e6d3df.png">
