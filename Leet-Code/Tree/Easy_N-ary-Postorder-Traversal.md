# N-ary Tree Postorder Traversal


<img width="668" alt="Screen Shot 2019-10-05 at 6 48 25 PM" src="https://user-images.githubusercontent.com/46575719/66261733-bb059680-e7a0-11e9-95d5-0635f503a482.png">



### 1. Recursive Implementation

#### My Solution.
```java

class Solution {
    public List<Integer> postorder(Node root) {
        List<Integer> ans = new ArrayList<>();
        dfs(root, ans);
        return ans;
    }
    
    private void dfs(Node node, List<Integer> ans){
        
        if(node != null){  
            for(int i = 0; i < node.children.size(); i++){
                dfs(node.children.get(i), ans);
            }
            ans.add(node.val);
        }     
    }
}

```

#### Other Solution from the Discussion.
```java
class Solution {
    List<Integer> list = new ArrayList<>();
    public List<Integer> postorder(Node root) {
        if (root == null)
            return list;
        
        for(Node node: root.children)
            postorder(node);
        
        list.add(root.val);
        
        return list;
    }
}
```

### 2. Iterative Implementation

```java


```
