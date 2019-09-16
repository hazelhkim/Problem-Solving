## Recursion and Dynamic Programming

- While there are a large number of recursive problems, many follow **similar patterns**. 
- A good hint that a problem is recursive is that it can be built off of **subproblems**. <br />

When you hear a problem beginning with the following statements, it's often (though not always) a good candidate for recursion: 
    - "Design an algorithm to compute the nth ...," <br />
    - "Write code to list the first n...," <br />
    - "Implement a method to compute all ...," <br />
    - and so on.

**Tip**
- People typtically have about 50% accuracy in their "this sounds like a recursive problem" instinct. Use that instict, since that 50% is valuable. But don't be afraid to look at the problem in a different way, even if you initially thought it seemed recursive. There's also a 50% chance that you were wrong. 
- Practice makes perfect! The more problems you do, the easier it will be to recognize recursive problems. 

**Outline**
1. How to Apprach
2. Recursion vs. Iterative Solutions
3. Dynamic Programming & Memoization

### 1. How to Approach
- Recursive solution, by definition, are built off of solutions to subproblems.
- Many times, this will mean simply to compute f(n) by adding sth, removing sth, or otherwise changing the solution for f(n-1).
- In other cases, you might solve the problem for the first half of the data set, then the second half, and then merge those results.

There are many ways you might divide a problem into subproblems. *Three* of the most common approaches to develop an algorithm are bottom-up, top-down, and half-and-half.

#### 1) Bottom-Up Approach
The bottom-up approach is often the most intuitive. 
- We start with knowing how to solve the problem for a simple case, like a list with only one element. 
- Then we figure out how to solve the problem for two elements, then for three elemtns, and so on. 
- The key here is to think about how you can *build* the solution for one case off of the previous case (or multiple previous cases).

#### 2) Top-Down Approach
The top-down approach can be more complex since it's less concrete. But sometimes, it's the best way to think about the problem.
- In these problems, we think about how we can divide the problem for case N into subproblems. 
- Be careful of overlap between the cases.

#### 3) Half-and-Half Approach
In addition to top-down and bottom-up approaches, it's often effective to divide the data set in half.<br />
For example:
  - Binary search works with a "half-and-half" approach. When we look for an element in a sorted array, we first figure out which half of the array contains the value. Then we recurse and search for it in that half.
  - Merge sort is also a "half-and-half" approach. We sort each half of the array and then merge together the sorted halves.
  
### 2. Recursive vs. Iterative Solutions
- Recursive algorithms can be very space inefficient. Each recursive call adds a new layer to the stack, which means that if your algorithm recurses to a depth of n, it uses at least O(n) memory.
- For this reason, it's often better to implement a recursive algorithm **iteratively**. All recursive algorithms can be implemented iteratively, although sometimes the code to do so is much more complex. 
- Before diving into recursive code, ask yourself how hard it would be to implement it iteratively, and discuss the tradeoffs with your interviewer. 

### 3. Dynamic Programming & Memoization
Although people make a big deal about how scary dynamic programming problems are, there's really no need to be afraid of them. In fact, once you get the hang of them, these can actually be very easy problems.
- Dynamic programming is mostly just a matter of taking a recursive algorithm and finding the overlapping subproblems (that is, the repeated calls). You then cache those results for future recursive calls. 
- Alternatively, you can study the pattern of the recursive calls and implement something iterative. You still "cache' previous work. 
- A note on terminology
  - Some people call top-down dynamic programming "memoization" 
  - Some people only use "dynamic programming" to refer to bottom-up work.
  - we do not make such a distinction here --> we call both dynamic programming.
  
One of the simplest example of dynamic programming is computing the nth Fibonacci number. A good way to approach such a problem is often to implement it as a normal recursive solution, and then add the caching part. 

#### Fibonacci Numbers.
Let's walk through an approach to compute **nth** Fibonacci number. **->good candidate for recursion!** <br />

<Recursive>
  
```java
  
int fibonacci(int i) {
  if( i == 0 ) return 0;
  if( i == 1 ) return 1;
  return fibonacci(i-1) + fibonacci(i-2);

}

```

What is the **runtime** of this function?

- If you think O(n) or O(n^2) (as many people do), think again.
- We'll have roughly O(2^n) nodes. This gives us runtime of roughly **O(2^n)**.
    - How many nodes are in the tree? Until we get down to the base cases (leaves), each node has two children. Each node brancesh out twice.
    - Observe that the leaves on the tree are all fib(1) and fib(0). Those signify the base cases. 
    - The root node has two children. Each of those children has two children (so four children total in the "grand children" level). Each of those grandchildren has two children, and so on. 
  
- Study the code path that the code takes. Draw the code paths as a tree (that is, the recursion tree) is useful on this and many recursive problems.

<img width="584" alt="Screen Shot 2019-09-16 at 1 35 49 AM" src="https://user-images.githubusercontent.com/46575719/64936126-6ff00780-d822-11e9-9d5c-acf1911f736a.png">

- Actually, it's slightly better than O(2^n). 
    - If you look at the subtree, you might notice that (excluding the leaf nodes and those immediately above it) the right subtree of any node is always smaller than the left subtree. 
    - If they were the same size, we'd have an O(2^n) runtime. But since the right and left subtrees are not the same size, the tru runtime is closer to (1.6^n). 
    - Saying O(2^n) is still technically correct though as it describes an upper bound on the runtime. Either way, we still have an exponential runtime. 
  
  





