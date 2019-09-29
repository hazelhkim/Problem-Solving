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
Same answer, different result..

<img width="676" alt="Screen Shot 2019-09-29 at 2 53 16 PM" src="https://user-images.githubusercontent.com/46575719/65837730-e253f380-e2c8-11e9-9891-f0d6aca1654d.png">

<img width="687" alt="Screen Shot 2019-09-29 at 3 12 32 PM" src="https://user-images.githubusercontent.com/46575719/65837956-93f42400-e2cb-11e9-81d3-814f86db6f87.png">

#### Other Solution

Method 1. 


```java
    public List<String> commonChars(String[] A) {
        List<String> ans = new ArrayList<>();
        int[] count = new int[26]; 
        Arrays.fill(count, Integer.MAX_VALUE);
        for (String str : A) {
            int[] cnt = new int[26];
            str.chars().forEach(c -> ++cnt[c - 'a']); // count each char's frequency in string str.
            for (int i = 0; i < 26; ++i) { count[i] = Math.min(cnt[i], count[i]); } // update minimum frequency.
        }
        for (char c = 'a'; c <= 'z'; ++c) {
            while (count[c - 'a']-- > 0) { ans.add("" + c); }
        }
        return ans;
    }


```

Method 2.

``` java
    public List<String> commonChars(String[] A) {
        int[] count = new int[26]; 
        Arrays.fill(count, Integer.MAX_VALUE);
        for (String str : A) {
            int[] cnt = new int[26];
            str.chars().forEach(c -> ++cnt[c - 'a']); // count each char's frequency in string str.
            IntStream.range(0, 26).forEach(i ->  count[i] = Math.min(cnt[i], count[i])); // update minimum frequency.
        }
        List<String> ans = new ArrayList<>();
        IntStream.range('a', 'z' + 1).forEach(c ->  ans.addAll(Collections.nCopies(count[c - 'a'], "" + (char)c)));
        return ans;
    }

```
