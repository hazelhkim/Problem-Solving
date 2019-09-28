# Height Checker


<img width="674" alt="Screen Shot 2019-09-28 at 1 56 03 AM" src="https://user-images.githubusercontent.com/46575719/65812288-22b15580-e193-11e9-8a8c-ceb73069a64a.png">

#### My Answer:
```java
class Solution {
    public int heightChecker(int[] heights) {
        int size = heights.length;
        int count = 0;
        int[] position = new int[size];
        for(int i = 0; i < size; i++) {
            position[i] = heights[i];
        }
        Arrays.sort(heights);
        for(int i = 0; i < size; i++ ) {
            if(heights[i] != position[i]) { count ++; }
        }
        return count;
    }
}

```

<img width="556" alt="Screen Shot 2019-09-28 at 1 57 03 AM" src="https://user-images.githubusercontent.com/46575719/65812298-46749b80-e193-11e9-8d59-a142991d2a30.png">


#### Another Solution:
( Without Sort: O(N) )

```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] heightToFreq = new int[101];
        
        for (int height : heights) {
            heightToFreq[height]++;
        }
        
        int result = 0;
        int curHeight = 0;
        
        for (int i = 0; i < heights.length; i++) {
            while (heightToFreq[curHeight] == 0) {
                curHeight++;
            }
            
            if (curHeight != heights[i]) {
                result++;
            }
            heightToFreq[curHeight]--;
        }
        
        return result;
    }
}

```
<img width="550" alt="Screen Shot 2019-09-28 at 1 59 04 AM" src="https://user-images.githubusercontent.com/46575719/65812311-8d629100-e193-11e9-875d-f05a541b9067.png">
