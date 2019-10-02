# Fair Candy Swap


<img width="747" alt="Screen Shot 2019-10-01 at 9 21 42 PM" src="https://user-images.githubusercontent.com/46575719/66011518-78d31100-e491-11e9-937c-fbf401087ef9.png">
<img width="747" alt="Screen Shot 2019-10-01 at 9 21 52 PM" src="https://user-images.githubusercontent.com/46575719/66011523-7e305b80-e491-11e9-804e-0ebabbc52bdd.png">


#### My Answer:

```java

class Solution {
    public int[] fairCandySwap(int[] A, int[] B) {
        int sum_A = 0, sum_B = 0;
        int[] ans = new int[2];
        
        for(int i : A) {
            sum_A += i;
        }
        for(int i : B) {
            sum_B += i;
        }

        for(int a : A) {
            for(int b : B) {
                if(sum_A - a + b == sum_B - b + a) {
                    ans[0] = a;
                    ans[1] = b;
                    break;
                }
            }
        }
        return ans;
        
    }
}
```
<img width="672" alt="Screen Shot 2019-10-01 at 9 22 34 PM" src="https://user-images.githubusercontent.com/46575719/66011551-9902d000-e491-11e9-99c3-c05397b99f9a.png">

#### Other Solutions:

```java
class Solution {
    public int[] fairCandySwap(int[] A, int[] B) {
        int sa = 0, sb = 0;  // sum of A, B respectively
        for (int x: A) sa += x;
        for (int x: B) sb += x;
        int delta = (sb - sa) / 2;
        // If Alice gives x, she expects to receive x + delta

        Set<Integer> setB = new HashSet();
        for (int x: B) setB.add(x);

        for (int x: A)
            if (setB.contains(x + delta))
                return new int[]{x, x + delta};

        throw null;
    }
}

```
