# Relative Sort Array

<img width="802" alt="Screen Shot 2019-09-28 at 7 08 27 PM" src="https://user-images.githubusercontent.com/46575719/65823393-60f65580-e223-11e9-8f05-7c7ea519b787.png">

#### My Answer:

```java

class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        
        int[] ans = new int[arr1.length];
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i : arr2) {
            map.put(i,0);
        }
        for(int i : arr1){
            if(map.containsKey(i)){
                map.put(i, map.get(i)+1);
            }
        }
        Arrays.sort(arr1);
        int idx = 0;
        for(int j = 0; j < map.size(); j ++ ) {
            int val = arr2[j];
            for(int k = 0; k < map.get(val); k++){
                ans[idx] = val;
                idx ++;
            }
        }
        for(int i : arr1) {
            if( !map.containsKey(i) && idx < arr1.length ){
                ans[idx] = i;
                idx++;
            }
        }
        return ans;
    }
}

```

<img width="809" alt="Screen Shot 2019-09-28 at 7 35 42 PM" src="https://user-images.githubusercontent.com/46575719/65823593-2c849880-e227-11e9-87d6-597c13442133.png">

#### Another Solution:

```java
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int k = 0;
        int[] cnt = new int[1001], ans = new int[arr1.length];
        for (int i : arr1)                      // Count each number in arr1.
            ++cnt[i];
        for (int i : arr2)                      // Sort the common numbers in both arrays by the order of arr2.
            while (cnt[i]-- > 0)
                ans[k++] = i;
        for (int i = 0; i < 1001; ++i)          // Sort the numbers only in arr1.
            while (cnt[i]-- > 0)
                ans[k++] = i;
        return ans;
    }

```
<img width="803" alt="Screen Shot 2019-09-28 at 7 36 40 PM" src="https://user-images.githubusercontent.com/46575719/65823601-4faf4800-e227-11e9-8020-24e0e83677a6.png">

