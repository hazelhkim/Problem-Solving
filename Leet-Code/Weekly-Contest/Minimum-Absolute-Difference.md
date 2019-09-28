## Minimum Absolute Difference

<img width="822" alt="Screen Shot 2019-09-22 at 12 56 27 AM" src="https://user-images.githubusercontent.com/46575719/65382460-dae28800-dcd3-11e9-81c7-eafe61e84fd5.png">


#### My Answer.

```java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr);
        List<List<Integer>> ans = new ArrayList<>();
        int min = Math.abs(arr[0] - arr[1]); // it can be: int min = Integer.MAX_VALUE; instead. :)
        for(int i = 0; i < arr.length-1; i ++) {
            
            //This can be just like: min = Math.min(min, arr[i] - arr[i-1]);
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


## My Second Try.

```java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr);
        List<List<Integer>> ans = new ArrayList<>();
        int min = Integer.MAX_VALUE;
        for(int i = 1; i < arr.length; i++) {
            int val = arr[i]-arr[i-1];
            if(val < min) {min = val;}
        }
        for(int i = 1; i < arr.length; i++) {
            int val = arr[i]-arr[i-1];
            List<Integer> l = new ArrayList<Integer>();
            if(val == min) {
                l.add(arr[i-1]);
                l.add(arr[i]);
                ans.add(l);
            }
        }
        return ans;
    }
}

```

<img width="799" alt="Screen Shot 2019-09-28 at 7 53 15 PM" src="https://user-images.githubusercontent.com/46575719/65823716-a158d200-e229-11e9-9988-1fe55fe0a034.png">

I took advantage of Arrays.sort() method so that I didn't need to use Math.abs() method; I can substract the element from the previous element. It wil always be a non-negative value. 

#### Other Solutions:

1. It used ** min = Math.min(a, b); ** to assign the min value instead of using if-condition statement. 

```java
    public static List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr); // imp!!! to sort elements 
        int min = Integer.MAX_VALUE;
		//find min diff
        for (int i = 1; i < arr.length; i++) {
            min = Math.min(min, arr[i] - arr[i - 1]);
        }
		//add all element with diff of min
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] - arr[i - 1] == min) {
                List<Integer> list = new ArrayList<>();
                list.add(arr[i - 1]);
                list.add(arr[i]);
                result.add(list);
            }
        }
        return result;
    }

```

2. It used Arrays.asList() method to assign the elemnents into the List<List<Integer>> data structure.

```java

    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        List<List<Integer>> res = new ArrayList();
        //sort elements
        Arrays.sort(arr);
        //init our min difference value
        int min = Integer.MAX_VALUE;
        //start looping over array to find real min element. Each time we found smaller difference
        //we reset resulting list and start building it from scratch. If we found pair with the same
        //difference as min - add it to the resulting list
        List<Integer> minDiffList = new ArrayList();
        for (int i = 0; i < arr.length - 1; i++) {
            int diff = arr[i + 1] - arr[i];
            if (diff < min) {
                min = diff;
                res = new ArrayList();
                res.add(Arrays.asList(arr[i], arr[i + 1]));
            } else if (diff == min) {
                res.add(Arrays.asList(arr[i], arr[i + 1]));
            }
        }
        return res;
    }
```
