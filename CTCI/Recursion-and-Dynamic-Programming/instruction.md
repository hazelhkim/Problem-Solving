## Recursion and Dynamic Programming

- While there are a large number of recursive problems, many follow **similar patterns**. 
- A good hint that a problem is recursive is that it can be built off of **subproblems**. <br />
- When you hear a problem beginning with the following statements, it's often (though not always) a good candidate for recursion:
  - "Design an algorithm to compute the nth ...," 
  - "Write code to list the first n...," 
  - "Implement a method to compute all ...," 
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
- Indeed, if we implemented this on a computer, we'd see the number of seconds increase exponentially.
  - We should look for a way to optimize this
<img width="335" alt="Screen Shot 2019-09-16 at 10 31 58 AM" src="https://user-images.githubusercontent.com/46575719/64966726-4f00d400-d86d-11e9-861c-6934cce005f9.png">

#### Fibonacci numbers *<Top-Down Dynamic Programming (or Memoization)>*


1. In the recursion tree, there are lots of identical nodes. For example, fib(3) appears twice and fib(2) appears three times. Why should we recompute these from scratch each time?

2. In fact, when we call fib(n), we shouldn't have to do much more than O(n) calls, since there's only O(n) possible values we can throw at fib. Each time we compute fib(i), we should just cache this result and use it later. -> This is exactly what **memoization** is.

3. With just a small modification, we can tweak this function to run in O(n) time. We simply cache the results of fibonacci(i) betweeen calls. 
  
```java

int fibonacci(int n) {
  return fibonacci(n, new int[n+1]);
}

int fibonacci(int i, int[] memo) {
  if (i == 0 || i == 1) return i;
  
  if(memo[i] == 0) {
    memo[i] = fibonacci(i-1, memo) + fibonacci(i-2, memo);
  }

  return memo[i];
}
```
4. Fast! (DP is faster than Recursion.) While the first recursive function may take over a minute to generate the 50th Fibonacci number on a typical computer, the dynamic programming method can generate the 10,000th Fibonacci number in just fractions of a millisecond. (Of course, with this exact code, the int would have overflowed very early on.)

5. Now, if we draw the recursion tree, it looks something like this (the black boxes represent cached calls that returned immediately):

<img width="513" alt="Screen Shot 2019-09-16 at 4 37 28 PM" src="https://user-images.githubusercontent.com/46575719/64991687-52618300-d8a0-11e9-9909-ed4f6027097c.png">


6. How many nodes are in this tree now? We might notice that the tree now just shoots straight down, to a depth of roughly n. Each node of those nodes has one other child, resulting in roughly 2n children in the tree. This gives us a runtime of 0 (n). Often it can be useful to picture the recursion tree as something like this:

<img width="606" alt="Screen Shot 2019-09-19 at 11 49 44 PM" src="https://user-images.githubusercontent.com/46575719/65298100-3710a500-db38-11e9-89a7-0dd02e66dc0f.png">


7. This is not actually how the recursion occurred. However, by expanding the further up nodes rather than the lower nodes, you have a tree that grows wide before it grows deep. (It's like doing this breadth-first rather than depth-first.) Sometimes this makes it easier to compute the number of nodes in the tree. All you're really doing is changing which nodes you expand and which ones return cached values. Try this if you're stuck on computing the runtime of a dynamic programming problem.


#### Fibonacci numbers *<Bottom-Up Dynamic Programming>*

We can also take this approach and implement it with bottom-up dynamic programming. Think about doing the same things as the recursive memoized approach, but in reverse.

First, we compute fib (1) and fib (0), which are already known from the base cases.Then we use those to compute fib (2). Then we use the prior answersto compute fib (3), then fib (4), and so on.

```java
int fibonacci(int n) {
  if ( n == 0 ) return 0;
  
  int[] memo = new int[n];
  memo[0] = 0;
  memo[1] = 1;
  for( int i = 2; i < n ; i++ ) {
    memo [i] = memo [ i - 1 ] + memo [ i - 2 ];
  }
  return memo [ n - 1 ] + memo [ n - 2 ];
}

```

If you really think about how this works, you only use memo[i] for memo[i+l] and memo[i+2].Youdon't need it after that. Therefore, we can get rid of the memo table and just store a few variables.

```java
int fibonacci ( int n ) {

  if ( n == 0 ) return 0;
  int a = 0;
  int b = 1;
  for( int i = 2; i < n ; i ++ ) {
    int c = a + b;
    a = b;
    b = c;
  }
  return a + b;
}

```

This is basically storing the results from the last two Fibonacci values into a and b. At each iteration, we computethenextvalue(c = a + b)andthenmove(b, c = a + b) into (a, b) . < br />
This explanation might seem like overkill for such a simple problem, but truly understanding this process will make more difficult problems much easier. Going through the problems in this chapter, many of which use dynamic programming, will help solidify your understanding.
