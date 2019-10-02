# Partition Array Into Three Parts With Equal Sum

<img width="681" alt="Screen Shot 2019-10-01 at 10 25 16 PM" src="https://user-images.githubusercontent.com/46575719/66013752-5abdde80-e49a-11e9-9832-c2850dcc001f.png">

#### Solution
```java

class Solution {
    public boolean canThreePartsEqualSum(int[] A) {
        int total = Arrays.stream(A).reduce(0, Integer::sum);
        if (total % 3 != 0) return false;
        int count = 0, sum = 0;
        for (int i = 0; i < A.length; i++) {
            sum += A[i];
            if (sum == (total / 3)) {
                sum = 0;
                count++;
            }
        }
        return count >= 3;
    }
}

```
OR

```java
    public boolean canThreePartsEqualSum(int[] A) {
        int sum = Arrays.stream(A).sum(), part = 0, cnt = 0;
        if (sum % 3 != 0) { return false; }
        for (int a : A) {
            part += a;
            if (part != sum / 3) { continue; } // not the average: sum / 3
            if (++cnt == 3) { return true; } // find an average, increase the counter.
            part = 0; // reset part.
        }
        return false;
    }

```
