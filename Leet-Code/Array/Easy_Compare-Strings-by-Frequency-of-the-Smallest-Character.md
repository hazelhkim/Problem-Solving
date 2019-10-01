# Compare Strings by Frequency of the Smallest Character
 
<img width="795" alt="Screen Shot 2019-10-01 at 12 53 25 AM" src="https://user-images.githubusercontent.com/46575719/65935509-4ff64180-e3e7-11e9-9ff7-b3c077926a58.png">

#### My Answer:
(NOT WORKING.. LOL)

```java
class Solution {
    public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] count = new int[words.length];
        HashMap<Integer, Integer> map = new HashMap<Integer,Integer>();
        for(String str : queries) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            int i = 1, j = 1;
            while(chars[0]==chars[i]){
                i++;
                j++;
            }
            map.put(i, j);
        }
        
        for(String str : words) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            count[chars[0] - 'a'] = 1;
            int i = 0, j = 0;
            while(chars[0] == chars[i]){
                count[j]++;
                i++;
            }
            j++;
        }
        int[] ans = new int[map.size()];
        for(int i = 0; i < map.size(); i++){
            for(int j = 0; j < count.length; j++) {
                if(map.get(i) < count[j]) {
                    ans[i] ++;
                }
            }
        } 
        return ans;
    }
}
```

#### Other Solutions from Discussions:


```java
public int[] numSmallerByFrequency(String[] queries, String[] words) {
        
        int[] q = new int[queries.length];
        int[] w = new int[words.length];
        
        for (int i = 0; i < q.length; i++) {
            q[i] = getFunc(queries[i]);
        }
        for (int i = 0; i < w.length; i++) {
            w[i] = getFunc(words[i]);
        }
       
        Arrays.sort(w);
        int[] res = new int[q.length];
        for (int i = 0; i < q.length; i++) {
            int l = 0, r = w.length - 1;
            while (l <= r) {
                int m = (r + l) / 2;
                if (w[m] <= q[i]) {
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            }
            res[i] = w.length - l;
        }
        return res;
    }
    
    int getFunc(String s) {
        char chr = 'z';
        int count = 0;
        
        for (char ch : s.toCharArray()) {
            if (ch < chr) {
                count = 1;
                chr = ch;
            } else if (chr == ch) {
                count++;
            }
        }
        return count;
    }
```
OR

```java
public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] q = new int[queries.length], w = new int[words.length];
        for (int i = 0; i < q.length; i++) {
            q[i] = jisuan(queries[i]);
        }
        for (int i = 0; i < w.length; i++) {
            w[i] = jisuan(words[i]);
        }
        Arrays.sort(w);
        int[] ans = new int[q.length];
        for (int i = 0; i < q.length; i++) {
            int l = 0, r = w.length - 1;
            while (l <= r) {
                int mid = (l + r) / 2;
                if (w[mid] <= q[i]) {
                    l = mid + 1;
                }
                else {
                    r = mid - 1;
                }
            }
            ans[i] = w.length - l;
        }
        return ans;
    }
    
    private int jisuan(String str) {
        int[] arr = new int[26];
        for (char ch : str.toCharArray())
            arr[ch - 'a']++;
        for (int i = 0; i < 26; i++) {
            if (arr[i] != 0)
                return arr[i];
        }
        return 0;
    }
```


