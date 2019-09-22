## Minimum Absolute Difference

<img width="822" alt="Screen Shot 2019-09-22 at 12 56 27 AM" src="https://user-images.githubusercontent.com/46575719/65382460-dae28800-dcd3-11e9-81c7-eafe61e84fd5.png">


#### My Answer.

```java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr);
        List<List<Integer>> ans = new ArrayList<>();
        int min = Math.abs(arr[0] - arr[1]);
        for(int i = 0; i < arr.length-1; i ++) {
            if( min > Math.abs(arr[i] - arr[i+1])) {
                    min = Math.abs(arr[i] - arr[i+1]); 
            }
        }
        
        for(int i = 0; i < arr.length-1; i ++) {
            if( Math.abs(arr[i]-arr[i+1]) == min ) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(arr[i]);
                list.add(arr[i+1]);
                ans.add(list);
            }
        }
        return ans;
    }
}
```

#### Detail.

<img width="644" alt="Screen Shot 2019-09-22 at 12 58 13 AM" src="https://user-images.githubusercontent.com/46575719/65382471-1aa96f80-dcd4-11e9-9dd0-d470062d1a2b.png">
