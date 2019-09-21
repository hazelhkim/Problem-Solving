## Reverse Substrings Between Each Pair of Parentheses

<img width="988" alt="Screen Shot 2019-09-21 at 1 58 07 PM" src="https://user-images.githubusercontent.com/46575719/65377272-f455e680-dc77-11e9-9d7c-004860dd5003.png">


#### Simple Stack and Queue Solution

```java

    public String reverseParentheses(String s) {
        Stack<Character> st = new Stack<>();
        for(char c: s.toCharArray()){
            if( c == ')'){
                Queue<Character> p = new LinkedList<>();
                while(!st.isEmpty() && st.peek() != '(') p.add(st.pop());
                if(!st.isEmpty()) st.pop();
                while(!p.isEmpty()) st.push(p.remove());
            } else {
                st.push(c);
            }
        }
        StringBuilder sb = new StringBuilder();
        while(!st.isEmpty()) sb.append(st.pop());
        
        return sb.reverse().toString();
    }


```
