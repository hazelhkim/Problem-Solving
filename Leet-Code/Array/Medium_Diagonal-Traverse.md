Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.

<img width="549" alt="Screen Shot 2019-10-09 at 5 02 36 PM" src="https://user-images.githubusercontent.com/46575719/66520153-a255f300-eab6-11e9-9304-d9673bbd645d.png">


Note: The total number of elements of the given matirx will not exceed 10,000.

```java
class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        
        //need this in case the matrix is empty; otherwise, int c would get a boundary error.
        if (matrix.length == 0) return new int[0];
        
        int row= 0, col = 0, r = matrix.length, c = matrix[0].length;
        int[] answer = new int[r*c];
        
          for(int i = 0; i < answer.length; i++) {
            
            answer[i] = matrix[row][col];

            // moving up;
            if( (row+col) %2 == 0 ) {
                //condition order matters in case both conditions are met.
                if (col == c-1) { row++;} 
                else if(row == 0) { col++;} 
                else { col++; row--;}
            // moving down;
            } else {
                //condition order matters in case both conditions are met.
                if(row == r-1) { col++;} 
                else if(col == 0) { row++;} 
                else { col--; row++; }
            }     
        }
        return answer;
    }
}
```
