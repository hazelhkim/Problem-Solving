## 1189. Maximum Number of Balloons

<img width="847" alt="Screen Shot 2019-09-15 at 7 48 23 PM" src="https://user-images.githubusercontent.com/46575719/64929249-11ef0000-d7e1-11e9-955f-13f3a2dd447d.png">

#### My Answer:

```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        //balloon
        int[] check = new int[5];
            
        for(int i = 0; i < text.length() ; i++) {
            if(text.charAt(i) == 'b') {check[0]++;}
            else if(text.charAt(i) == 'a') {check[1]++;}
            else if(text.charAt(i) == 'l') {check[2]++;}
            else if(text.charAt(i) == 'o') {check[3]++;}
            else if(text.charAt(i) == 'n') {check[4]++;}
        }
        int min = check[0];
        if(Math.min(min,check[1]) < min) { min = Math.min(min,check[1]); }
        if(Math.min(min,check[2]/2) < min) { min = Math.min(min,check[2]/2); }
        if(Math.min(min,check[3]/2) < min) { min = Math.min(min,check[3]/2); }
        if(Math.min(min,check[4]) < min) { min = Math.min(min,check[4]); }

        return min;
    }
}

```

#### Inspirational Answer:

```java
class Solution {
public:
    int maxNumberOfBalloons(string text) {
        int cnt[128] = {0};
        for(const auto t: text) {
            cnt[t]++;
        }
        int ret = 1;
        int b = cnt['b'];
        int a = cnt['a'];
        int l = cnt['l']/2;
        int o = cnt['o']/2;
        int n = cnt['n'];
        ret = min(min(a,b), min(min(l,o), n));
        return ret;
    }
};
