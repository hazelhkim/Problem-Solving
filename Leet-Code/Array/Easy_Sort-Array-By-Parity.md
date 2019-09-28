
# Sort Array By Parity

<img width="706" alt="Screen Shot 2019-09-28 at 12 21 40 AM" src="https://user-images.githubusercontent.com/46575719/65811410-f3481c00-e185-11e9-90a3-9c47fc1c7528.png">





#### My Answer:

```java

class Solution {
    public int[] sortArrayByParity(int[] A) {
        int[] ans = new int[A.length];
        int index_even = 0, index_odd = A.length-1;
        for(int i : A) {
            if(i%2 == 0) {
                ans[index_even] = i;
                index_even++;
            } else {
                ans[index_odd] = i;
                index_odd--;
            }
        }
        return ans;
    }
}

```



#### Better Solution:

```java

    public int[] sortArrayByParity(int[] A) {
        for (int i = 0, j = 0; j < A.length; j++)
            if (A[j] % 2 == 0) {
                int tmp = A[i];
                A[i++] = A[j];
                A[j] = tmp;;
            }
        return A;
    }

```
