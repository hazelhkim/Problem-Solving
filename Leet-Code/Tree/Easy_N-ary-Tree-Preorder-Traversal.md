# N-ary Tree Preorder Traversal

<img width="663" alt="Screen Shot 2019-10-05 at 4 49 46 PM" src="https://user-images.githubusercontent.com/46575719/66260704-27c46500-e790-11e9-911e-5a62cf5d4386.png">

#### My Answer #1. 

<Iterative Implementation>

```java

/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> ans = new ArrayList<>();
        Stack<Node> stack = new Stack();
        if(root!=null) {
            stack.push(root);
        } else {return ans;}
        while(!stack.isEmpty()){
            Node node = stack.pop();
            Stack<Node> child_order_stack = new Stack();
            for( Node child_node : node.children ){
                child_order_stack.push(child_node);
            }
            while(!child_order_stack.isEmpty()){
                stack.push(child_order_stack.pop());
            }
            ans.add(node.val);
        }
        return ans;
    }
}
```

<img width="679" alt="Screen Shot 2019-10-05 at 4 49 10 PM" src="https://user-images.githubusercontent.com/46575719/66260695-11b6a480-e790-11e9-8515-9d5ef47d9746.png">

#### My Answer #2. 

<Recursive Implementation>

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> ans = new ArrayList<>();
        dfs(root, ans);
        return ans;
    }
    
    private void dfs(Node root, List<Integer> ans){
        
        if(root != null) {
            ans.add(root.val);
            if(root.children != null) {
                for(int i = 0; i < root.children.size(); i++){
                    dfs(root.children.get(i), ans);
                }
            }
        }
    } 
}

```
<img width="680" alt="Screen Shot 2019-10-05 at 5 04 07 PM" src="https://user-images.githubusercontent.com/46575719/66260855-285dfb00-e792-11e9-87d8-274cb50acc5b.png">





