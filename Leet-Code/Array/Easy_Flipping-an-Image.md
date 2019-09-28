# Flipping an Image


<img width="688" alt="Screen Shot 2019-09-28 at 12 06 27 AM" src="https://user-images.githubusercontent.com/46575719/65811275-f04c2c00-e183-11e9-9f1f-545f73880f1b.png">

####My Answer:

```java

class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int size = A.length;
        Stack<Integer> stack = new Stack<Integer>();
        for(int i = 0; i < size; i++) {
            for(int j : A[i]) {
                stack.push(j);
            }
            int index = 0;
            while(!stack.isEmpty()) {
                int val = stack.pop();
                if(val == 0) {val = 1;}
                else {val = 0;}
                A[i][index] = val;
                index ++;
            }
        }
        return A;
    }
}

```

####Better Solution:

```java

class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int n = A.length;
        for (int[] row : A)
            for (int i = 0; i * 2 < n; i++)
                if (row[i] == row[n - i - 1])
                    row[i] = row[n - i - 1] ^= 1;
        return A;
        
    }
}




```
