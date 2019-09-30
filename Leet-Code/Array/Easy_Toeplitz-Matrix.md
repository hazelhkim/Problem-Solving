# Toeplitz Matrix


<img width="770" alt="Screen Shot 2019-09-30 at 3 41 33 PM" src="https://user-images.githubusercontent.com/46575719/65910533-e7807380-e398-11e9-93bd-caada8c347af.png">
<img width="770" alt="Screen Shot 2019-09-30 at 3 41 43 PM" src="https://user-images.githubusercontent.com/46575719/65910536-e8190a00-e398-11e9-83bb-a25727acdc79.png">


#### My Answer:
```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        int n_row = matrix.length, n_col = matrix[0].length;
        List<List<Integer>> start = new ArrayList<>();
        int[] dig_dir = new int[] {1,1};
        
        for(int i = 0; i < matrix[0].length; i++) {
            //List<Integer> place = new ArrayList<>();
            start.add(Arrays.asList(0, i));
        }
        for(int i = 1; i < matrix.length; i++) {
            start.add(Arrays.asList(i, 0));
        }
        int count = 0;
        for(List<Integer> l : start){
            int row = l.get(0), col = l.get(1);
            for(int r = row, c = col; r<n_row && c<n_col; r += dig_dir[0], c += dig_dir[1]) {
                if(matrix[r][c] != matrix[row][col]) {return false;}
            }
        }
        return true;
    }
}
```
<img width="760" alt="Screen Shot 2019-09-30 at 3 52 21 PM" src="https://user-images.githubusercontent.com/46575719/65911226-4c889900-e39a-11e9-8c7f-1d524ffd77ff.png">

#### Other Solution: 

1. Group by Category <br />
Time Complexity: O(M*N) <br />
Space Complexity: O(M+N)

```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        for (int r = 0; r < matrix.length; ++r)
            for (int c = 0; c < matrix[0].length; ++c)
                if (r > 0 && c > 0 && matrix[r-1][c-1] != matrix[r][c])
                    return false;
        return true;
    }
}

```
<img width="772" alt="Screen Shot 2019-09-30 at 3 51 29 PM" src="https://user-images.githubusercontent.com/46575719/65911174-2d8a0700-e39a-11e9-8294-1146b1e8a977.png">


2. Compare With Top-Left Neighbor <br />
Time Complexity: O(M*N) <br />
Space Complexity: O(1)

```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        for (int r = 0; r < matrix.length; ++r)
            for (int c = 0; c < matrix[0].length; ++c)
                if (r > 0 && c > 0 && matrix[r-1][c-1] != matrix[r][c])
                    return false;
        return true;
    }
}
```
<img width="772" alt="Screen Shot 2019-09-30 at 3 49 29 PM" src="https://user-images.githubusercontent.com/46575719/65911023-e6037b00-e399-11e9-829e-14663f651643.png">

#### From Discussion : 

```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        for (int i = 0; i < matrix.length - 1; i++) {
            for (int j = 0; j < matrix[i].length - 1; j++) {
                if (matrix[i][j] != matrix[i + 1][j + 1]) return false;
            }
        }
        return true;
    }
}
```
<img width="764" alt="Screen Shot 2019-09-30 at 3 50 02 PM" src="https://user-images.githubusercontent.com/46575719/65911067-f9aee180-e399-11e9-9171-cea74c53745b.png">

