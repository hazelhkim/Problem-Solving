
# Word Break

<img width="698" alt="Screen Shot 2019-10-12 at 8 06 49 PM" src="https://user-images.githubusercontent.com/46575719/66709163-db4acd80-ed2b-11e9-8504-f263237a6c18.png">

#### Solutions From Discussion.

```java
public boolean wordBreak(String s, List<String> wordDict) {
    boolean[] dp = new boolean[s.length() + 1];
    Set<String> set = new HashSet<>();
    set.addAll(wordDict);

    dp[0] = true;
    for (int i = 1; i <= s.length(); i++) {
        for (int j = i - 1; j >= 0; j--) {
            dp[i] = dp[j] && set.contains(s.substring(j, i));
            if(dp[i]) break;
        }
    }
    return dp[s.length()];
}
```

#### Trie Tree Search Solution to Assist the DP (Faster)
```java

public class Solution {
    public class TrieNode {
        boolean isWord;
        TrieNode[] c;
        
        public TrieNode(){
            isWord = false;
            c = new TrieNode[128];
        }
    }
    
    public void addWord(TrieNode t, String w) {
        for (int i = 0; i < w.length(); i++) {
            int j = (int)w.charAt(i); 
            if (t.c[j] == null) t.c[j] = new TrieNode();
            t = t.c[j];
        }
        t.isWord = true;
    }
    
    public boolean wordBreak(String s, Set<String> wordDict) {
        TrieNode t = new TrieNode(), cur;
        for (String i : wordDict) addWord(t, i);
        char[] str = s.toCharArray();
        int len = str.length;
        boolean[] f = new boolean[len + 1];
        f[len] = true;
        
        for (int i = len - 1; i >= 0; i--) {
            //System.out.println(str[i]);
            cur = t;
            for (int j = i; cur != null && j < len ; j++) {
                cur = cur.c[(int)str[j]];
                if (cur != null && cur.isWord && f[j + 1]) {
                    f[i] = true;
                    break;
                }
            }
        }
        return f[0];
    }
}

```
