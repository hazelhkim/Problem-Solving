# Word Search II

<img width="790" alt="Screen Shot 2019-10-09 at 6 33 23 PM" src="https://user-images.githubusercontent.com/46575719/66525374-4c3b7c80-eac3-11e9-9ff5-b6ce11572799.png">

#### My Answer:

```java
class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        List<String> ans = new ArrayList();
 
        for(String word : words) {
            char[][] new_board = reset(board);
            if(check(new_board, word)) {
                ans.add(word);
            }  
        }
        
        return ans;
    }
    
    private boolean check(char[][] brd, String word) {
        char[] arr = word.toCharArray();
        //char[][] new_board = board.clone();
        for(int r = 0; r < brd.length; r++) {
            for(int c = 0; c < brd[0].length; c++) {
                if(brd[r][c] == arr[0]) {
                    if(dfs(brd, arr, r, c, 0)) return true;
                }
            }
        }
        return false;
    }
    
    private boolean dfs(char[][] table, char[] arr, int r, int c, int count) {
        if(count == arr.length) {return true;}
        if(r < 0 || c < 0 || r >= table.length || c >= table[0].length) {
            return false;
        }
        
        char ch = arr[count];
        if(table[r][c] == ch) {
            table[r][c] = '#';
            if(dfs(table, arr, r+1, c, count+1) || dfs(table, arr, r-1, c, count+1) || dfs(table, arr, r, c+1, count+1) || dfs(table, arr, r, c-1, count+1)) {return true;}
            table[r][c] = ch;
        }
        return false; 
    }
    
    private char[][] reset(char[][] b) {
        char[][] output = new char[b.length][b[0].length];
        for(int r = 0; r < b.length; r++ ) {
            for(int c = 0; c < b[0].length; c++) {
                output[r][c] = b[r][c];
            }
        }
        return output;
    }
}

```


<img width="534" alt="Screen Shot 2019-10-09 at 6 32 43 PM" src="https://user-images.githubusercontent.com/46575719/66525344-3463f880-eac3-11e9-814b-faa4f27b7747.png">
