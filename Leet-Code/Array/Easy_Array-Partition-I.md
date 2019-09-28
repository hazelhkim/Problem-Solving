# Array Partition I

<img width="548" alt="Screen Shot 2019-09-28 at 12 51 20 AM" src="https://user-images.githubusercontent.com/46575719/65811673-17a5f780-e18a-11e9-8b58-72b2d5010774.png">


#### My Answer:

```java
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int sum = 0;
        for(int i = 0; i < nums.length; i += 2 ) {
            sum += Math.min(nums[i], nums[i+1]);
        }
        return sum;
    }
}
```

<img width="534" alt="Screen Shot 2019-09-28 at 12 52 17 AM" src="https://user-images.githubusercontent.com/46575719/65811679-399f7a00-e18a-11e9-8dea-35b5d0ea4e9c.png">

#### Better Solution:

여기서의 오답노트: 중요한건, 이미 sorted array이기 때문에 그냥 둘중 첫번째 element를 sum에 더하면 되는거였다..ㅡㅡ.

```java

class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int sum = 0;
        for(int i = 0; i < nums.length; i += 2 ) {
            sum +=nums[i];
        }
        return sum;
    }
}

```
<img width="542" alt="Screen Shot 2019-09-28 at 12 54 09 AM" src="https://user-images.githubusercontent.com/46575719/65811699-7cf9e880-e18a-11e9-96ac-378017beba23.png">
