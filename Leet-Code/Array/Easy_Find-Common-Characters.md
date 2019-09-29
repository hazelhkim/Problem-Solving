# Find Common Characters

<img width="682" alt="Screen Shot 2019-09-29 at 2 51 43 PM" src="https://user-images.githubusercontent.com/46575719/65837706-aae54700-e2c8-11e9-85c7-a2197fc5da20.png">


#### My Answer:

```java
class Solution {
    public List<String> commonChars(String[] A) {
        
        List<String> ans = new ArrayList<>();
        int[][] count = new int[128][A.length];
        int idx = 0;
        for(String str : A) {
            char[] arr = str.toCharArray();
            for(int i : arr) {
                count[i][idx]++;
            }
            idx ++;
        }
        int[] res = new int[128];
        for(int i = 0; i < count.length; i++) {
            int min = Integer.MAX_VALUE;
            for(int j = 0; j < count[i].length; j++) {
                min = Math.min(min, count[i][j]);
            }
            for(int k = 0; k < min; k++ ){
                String s = Character.toString((char) i);
                ans.add(s);
            }
        }
        return ans;
    }
}

```

<img width="676" alt="Screen Shot 2019-09-29 at 2 53 16 PM" src="https://user-images.githubusercontent.com/46575719/65837730-e253f380-e2c8-11e9-9891-f0d6aca1654d.png">

#### Other Solution

```java


```
