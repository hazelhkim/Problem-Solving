# Number of Islands (200)
https://leetcode.com/problems/number-of-islands/
```python
class Solution {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {return 0;}
        
        int count = 0;
        for(int r = 0; r< grid.length; r++) {
            for(int c = 0; c<grid[0].length; c++) {
                if( grid[r][c] == '1') {
                    count += countIsland(grid, r, c);
                    
                }
            }
        }
        return count;
        
    }
    public int countIsland(char[][] grid, int r, int c) {
            if(r<0 || c<0 || r>= grid.length || c >= grid[0].length || grid[r][c] == '0') {
                return 0;
            }
            grid[r][c] = '0';
            
            countIsland(grid, r+1, c);
            countIsland(grid, r-1, c);  
            countIsland(grid, r, c+1);
            countIsland(grid, r, c-1);
            
            return 1;
    }
}
```
