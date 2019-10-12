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
<img width="549" alt="Screen Shot 2019-10-12 at 6 50 49 PM" src="https://user-images.githubusercontent.com/46575719/66708622-607cb500-ed21-11e9-8fa3-d406d8c1034e.png">


# Longest Continuous Increasing Subsequence

<img width="650" alt="Screen Shot 2019-10-12 at 6 53 15 PM" src="https://user-images.githubusercontent.com/46575719/66708632-9457da80-ed21-11e9-9f65-ee18f7422cd9.png">


#### Solution: Sliding Window Approach.
[Intuition and Algorithm]
Every (continuous) increasing subsequence is disjoint, and the boundary of each such subsequence occurs whenever nums[i-1] >= nums[i]. When it does, it marks the start of a new increasing subsequence at nums[i], and we store such i in the variable anchor.

For example, if nums = [7, 8, 9, 1, 2, 3], then anchor starts at 0 (nums[anchor] = 7) and gets set again to anchor = 3 (nums[anchor] = 1). Regardless of the value of anchor, we record a candidate answer of i - anchor + 1, the length of the subarray nums[anchor], nums[anchor+1], ..., nums[i]; and our answer gets updated appropriately.

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int ans = 0, anchor = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (i > 0 && nums[i-1] >= nums[i]) anchor = i;
            ans = Math.max(ans, i - anchor + 1);
        }
        return ans;
    }
}
```
[Complexity Analysis]
- Time Complexity : O(N), where N is the length of `nums`. We perform one loop through `nums`.
- Space Complexity : O(1), the space used by `anchor` and `ans`.
