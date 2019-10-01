# Reshape the Matrix

<img width="700" alt="Screen Shot 2019-10-01 at 1 47 19 AM" src="https://user-images.githubusercontent.com/46575719/65937280-699a8780-e3ed-11e9-9261-469055a8a408.png">
<img width="696" alt="Screen Shot 2019-10-01 at 1 47 30 AM" src="https://user-images.githubusercontent.com/46575719/65937285-6f906880-e3ed-11e9-86f0-58c61105bf6c.png">

#### My Answer:
```java
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int n_r = nums.length, n_c = nums[0].length;
        if(n_r * n_c != r * c) {return nums;}
        int[][] ans = new int[r][c];
        int count = 0;
        for(int i = 0; i < n_r; i++) {
            for(int j = 0; j < n_c; j++) {
                ans[count/c][count%c] = nums[i][j];
                count++;
            }
        }
        return ans;
    }
}
```

#### Other Solutions:
1. Using Queue <br />

```java

public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length)
            return nums;
        int count = 0;
        Queue < Integer > queue = new LinkedList < > ();
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                queue.add(nums[i][j]);
            }
        }
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                res[i][j] = queue.remove();
            }
        }
        return res;
    }
}
```
Time Complexity: O(M*N). We traverse over M*N elements twice. <br />
Space Complexity: O(M*N). The queue formed will be of size M*N.

<img width="660" alt="Screen Shot 2019-10-01 at 1 55 21 AM" src="https://user-images.githubusercontent.com/46575719/65937657-90a58900-e3ee-11e9-8f86-0d86395e7890.png">

2. Without using extra space. <br />

```java
public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length)
            return nums;
        int rows = 0, cols = 0;
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                res[rows][cols] = nums[i][j];
                cols++;
                if (cols == c) {
                    rows++;
                    cols = 0;
                }
            }
        }
        return res;
    }
}
```
Time Complexity: O(M*N) <br />
Space Complexity O(M*N). The resultant matrix of size M*N is used.

<img width="664" alt="Screen Shot 2019-10-01 at 1 55 05 AM" src="https://user-images.githubusercontent.com/46575719/65937667-9ac78780-e3ee-11e9-9124-febb9b611ef5.png">


3. Using Division and Modulus <- WHAT I'VE DONE. <br />

```java

public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length)
            return nums;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                res[count / c][count % c] = nums[i][j];
                count++;
            }
        }
        return res;
    }
}
```
Timce Complexity: O(M*N). <br />
Space Complexity: O(M*N).

<img width="659" alt="Screen Shot 2019-10-01 at 1 54 42 AM" src="https://user-images.githubusercontent.com/46575719/65937827-0dd0fe00-e3ef-11e9-86b8-0867389f80fb.png">
