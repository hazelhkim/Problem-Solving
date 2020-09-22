# Number of Islands (200)
https://leetcode.com/problems/number-of-islands/

#### Java
```java
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
#### Python
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0
        
        
        rows, cols = len(grid), len(grid[0])
        count = 0
        visit = set()
        
        def bfs(r,c):
            directions = [[0,1],[0,-1],[1,0],[-1,0]]
            q = collections.deque()
            q.append((r,c))
            visit.add((r,c))
            
            while q:
                row, col = q.popleft()
                for (dr, dc) in directions:
                    r, c = row+dr, col+dc
                    if ((r,c) not in visit and
                        r in range(rows) and
                        c in range(cols) and
                        grid[r][c] == "1" ):
                        visit.add((r,c)) 
                        q.append((r,c))
            return
                        
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == "1" and (r,c) not in visit:
                    count += 1
                    bfs(r,c)
                    
        return count

```
