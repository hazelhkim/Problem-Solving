# Search in a Binary Search Tree

<img width="681" alt="Screen Shot 2019-10-05 at 4 06 04 PM" src="https://user-images.githubusercontent.com/46575719/66260243-0d878880-e78a-11e9-84c6-fcd7ef034c01.png">

#### My Answer:

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        
        if(root == null) {return null;}
        if( root.val == val ) {return root;}
        
        if( root.val > val ) return searchBST(root.left, val);
        else if( root.val < val ) return searchBST(root.right, val);        

        return null;
    }
}
```

#### Other Solutions:

1. Recursion
```java
public TreeNode searchBST(TreeNode root, int val) {
        if(root == null) return root;
        if(root.val == val){
            return root;
        }
        else{
            return val<root.val? searchBST(root.left,val):searchBST(root.right,val);
        }
    }
```

2. Iteration
```java
public TreeNode searchBST(TreeNode root, int val) {
        while(root != null && root.val != val){
            root = val<root.val? root.left:root.right;
        }
        return root;
    }
```
