# Sum of Even Numbers After Queries

<img width="761" alt="Screen Shot 2019-09-30 at 4 52 53 PM" src="https://user-images.githubusercontent.com/46575719/65916112-c0c73a80-e3a2-11e9-8692-b789b79934e7.png">


#### My Answer:

```java
class Solution {
    public int[] sumEvenAfterQueries(int[] A, int[][] queries) {
        
        int[] ans = new int[queries.length];
        int sum = 0, count = 0;
        for(int i : A) {
            if(i%2 == 0) { sum += i; }
        }
        //System.out.print(sum);
        //while adding up the elements from the queries.
        for(int i = 0; i < queries.length; i++) {
            
            int val = queries[i][0];
            int idx = queries[i][1];
            int prev_val = A[idx];
            A[idx] += val;
            int new_val = A[idx];
            if(new_val%2 == 0 ) {
                if(prev_val %2 == 0 ){
                    sum = sum - prev_val + new_val;
                } else {
                    sum = sum + new_val;
                }
            } else {
                if(prev_val %2 == 0) {
                    sum -= prev_val;
                } else {
                    sum = sum;
                }
            }
            ans[count] = sum;
            count++;
        }
        return ans;
    }
}
```

<img width="772" alt="Screen Shot 2019-09-30 at 4 55 44 PM" src="https://user-images.githubusercontent.com/46575719/65916338-26b3c200-e3a3-11e9-9fcb-d11c50fd58c9.png">


#### Other Solutions:
Time Complexity: O(N+Q), where N is the length of `A` and Q is the number of `queries`. <br />
Space Complexity: O(Q), though we only allocate O(1) additional space. 

```java
class Solution {
    public int[] sumEvenAfterQueries(int[] A, int[][] queries) {
        int S = 0;
        for (int x: A)
            if (x % 2 == 0)
                S += x;

        int[] ans = new int[queries.length];

        for (int i = 0; i < queries.length; ++i) {
            int val = queries[i][0], index = queries[i][1];
            if (A[index] % 2 == 0) S -= A[index];
            A[index] += val;
            if (A[index] % 2 == 0) S += A[index];
            ans[i] = S;
        }

        return ans;
    }
}
```

<img width="745" alt="Screen Shot 2019-09-30 at 4 56 23 PM" src="https://user-images.githubusercontent.com/46575719/65916395-3e8b4600-e3a3-11e9-8df2-c467f1311f8a.png">


