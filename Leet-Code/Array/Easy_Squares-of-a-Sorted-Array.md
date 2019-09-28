# Squares of a Sorted Array

<img width="701" alt="Screen Shot 2019-09-28 at 12 31 23 AM" src="https://user-images.githubusercontent.com/46575719/65811505-4f5f7000-e187-11e9-883e-11072309d556.png">

#### My Answer:

```java

class Solution {
    public int[] sortedSquares(int[] A) {
        for(int i = 0; i < A.length; i++) {
            A[i] = A[i]*A[i];
        }
        
        Arrays.sort(A);
        return A;
    }
    
}

```

<img width="700" alt="Screen Shot 2019-09-28 at 12 33 08 AM" src="https://user-images.githubusercontent.com/46575719/65811514-93eb0b80-e187-11e9-8c0e-90d8cbd4adda.png">

#### Better Solution:

```java

class Solution {
    public int[] sortedSquares(int[] A) {
        int n = A.length;
        int[] result = new int[n];
        int i = 0, j = n - 1;
        for (int p = n - 1; p >= 0; p--) {
            if (Math.abs(A[i]) > Math.abs(A[j])) {
                result[p] = A[i] * A[i];
                i++;
            } else {
                result[p] = A[j] * A[j];
                j--;
            }
        }
        return result;
    }
}

```

<img width="692" alt="Screen Shot 2019-09-28 at 12 33 55 AM" src="https://user-images.githubusercontent.com/46575719/65811520-abc28f80-e187-11e9-98de-e5f2b16c9450.png">

