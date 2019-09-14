## Tree

Tree is a type of graph. <br />

### Types of Trees

A nice way to understand a tree is with a **recursive explanation**. <br />

A tree is a data structure composed of nodes.
1. Each tree has a root node. ( Actually, this isn't strictly necessary in graph theory, but it's usually how we use trees in programming, and especially programming interviews.) <br />
2. The root node has zero or more child nodes. <br />
3. Each child node has zero or more child nodes, and so on. <br />
 <br />
Other Features 
<br />
1. The tree cannot contain cycles.  <br />
2. The nodes may or may not be in a particular order. <br />
3. They could have any data type as values. <br />
4. They may or may not have links back to their parent nodes. <br />

A very simple class definition for Node is:
```java
class Node {
    public String name;
    public Node[] children;
}
```
Tree and graph questions are rife with ambiguous details and incorrect assumptions. Be sure to watch out for the following issues and seek clarification when necessary. <br />

### 1. Trees vs Binary Trees.

- A binary tree is a tree in which each node has up to two children. 
- Not all trees are binary trees. For example, if the tree is not a binary tree and has three children, you could call it a ternary tree.
- You might use a 10-ary tree, with each node having up to 10 children. 
- A node is called a "leaf" node if it has no children. 

### 2. Binary Tree vs. Binary Search Tree

- A binary search tree is a binary tree in which every node fits a specific ordering property: <br />
**all left descendents <= n < all right descendents**. This must be true for each node n. <br />
- The tree might or might not have duplicate values. If it has them, the duplicate values will be on the right or can be on either side. All are valid definitions -- clarify this with interviewer. <br />
- Dont' assume binary tree would be a binary search tree. Be sure to ask. 

<img width="614" alt="Screen Shot 2019-09-11 at 3 08 09 PM" src="https://user-images.githubusercontent.com/46575719/64739117-0086ba80-d4a6-11e9-840c-7e29941b33d5.png">

### 3. Balanced vs. Unbalanced.

- While many trees are balanced, not all are.
 - Note that balancing a tree does not mean the left and right subtrees are exactly the same size (like you see under "perfect binary trees" in the following diagram. )
- "Balanced" tree actually means something not terribly imbalanced. It's balanced enough to ensure O(log n) times for insert and find, but it's not necessarily as balanced as it could be. <br />
- Two common types of balanced trees: 1) red-black trees, 2) AVL trees.

### 4. Complete Binary Trees

A complete binary tree is a binary tree in which every level of the tree is fully filled, except for perhaps the last level. To the extent that the last level is filled, it is filled left to right. 

<img width="637" alt="Screen Shot 2019-09-11 at 3 18 03 PM" src="https://user-images.githubusercontent.com/46575719/64739600-632c8600-d4a7-11e9-90d0-ae04a77e860f.png">

### 5. Full Binary Trees

A full binary tree is a binary tree in which every node has either zero or two children. That is, no nodes have only one child. 

<img width="638" alt="Screen Shot 2019-09-11 at 3 19 12 PM" src="https://user-images.githubusercontent.com/46575719/64739653-8c4d1680-d4a7-11e9-983e-31bcfc805758.png">

### 6. Perfect Binary Trees

A perfect binary tree is one that is both full and complete. All leaf nodes will be at the same level, and this level has the maximum number of nodes. 

<img width="304" alt="Screen Shot 2019-09-11 at 3 20 27 PM" src="https://user-images.githubusercontent.com/46575719/64739713-b9012e00-d4a7-11e9-9e29-143d3fbcdcf2.png">

Note that perfect trees are rare in interviews and in real life, as a perfect tree must have exactly (2^k - 1) nodes (where k is the number of levels). In an interview, do not assume a binary tree is perfect. 

## Binary Tree Traversal

Prior to your interview, it is important to be comfortable implementing in-order, post-order, and pre-order traversal. The most common of these is in-order traversal.

### In-Order Traversal

In-order traversal means to "visit" (often, print) the left branch, then the current node, and finally, the right branch. 
```java
void inOrderTraversal(TreeNode node) {
  if(node != null) {
    inOrderTraversal(node.left);
    visit(node);
    inOrderTraversal(node.left);
  } 
}
```
When performed on a binary search tree, it visits the nodes in **ascending order** (hence the name "in-order").

### Pre-Order Traversal

Pre-order traversal visits the current node before its child nodes (hence the name "pre-order").
```java
void preOrderTraversal (TreeNode node) {
  if(node != null) {
    visit(node);
    preOrderTraversal(node.left);
    preOrderTraversal(node.right);
  }
}
```
In a pre-order traversal, the root is always the first node visited.

### Post-Order Traversal

Post-order traversal visits the current node after its child nodes (hence the name "post-order").
```java
void postOrderTraversal(TreeNode node) {
  if(node != null) {
    postOrderTraversal(node.left);
    postOrderTraversal(node.right);
    visit(node);
  }
}
```
In a post-order traversal, the root is always the last node visited. 






