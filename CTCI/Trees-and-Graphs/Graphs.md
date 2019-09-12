## Graphs

TREE
- A tree is actually a type of graph, but not all graphs are trees. 
- A tree is a connected graph without cycles. 
<br />
GRAPH <br />
- A graph is a collectin of nodes with edges between (some of) them. 
- Graphs can be either directed (like the following graph) or undirected. 

**directed edges**
a one-way street

**undirected edges**
like a two-way street

- The graph might consist of multiple isolated subgraphs. 
- The graph can also have cycles (or not). 

**connected graph**
A graph that has a path between every pair of vertices. 

**acyclic graph**
A graph that has no cycles. 

<br />
Visually, a graph is like this:

<img width="604" alt="Screen Shot 2019-09-12 at 3 43 42 PM" src="https://user-images.githubusercontent.com/46575719/64825997-237fa000-d574-11e9-9323-f425e2d782f5.png">

### Adjacent List

- This is the most common way to represent a graph. 
- Every vertex (or node) stores a list of adjacent vertices. 

In an undirected graph, an edge like (a, b) would be stored twice: once in a's adjacent vertices and once in b's adjacent vbertices. 
<br />
A simple class definition for a graph node could look essentially the same as a tree node. 

```java
class Graph {
    public Node[] nodes;
}

class Node {
    public String name; 
    public Node[] children;
}

```
The Graph class is used beacuse, unlike in a tree, you can't necessarily reach all the nodes from a single node. 
<br />

You don't necessarily need any additional classes to represent a graph. An array (or a hash table) of lists ( arrays, arraylists, linked lists, etc.) can store the adjacency list. The graph above could be represented as: <br />
0: 1 <br />
1: 2 <br />
2: 0,3 <br />
3: 2 <br />
4: 6 <br />
5: 4 <br />
6: 5 <br />

This is a bit more compact, but it isn't quite as clean. We tend to use node classes unless there's a compelling reason not to. 

### Adjacency Matrices

An adjacency matrix is an NxN boolean matrix (where N is the number of nodes), where a true value at matrix[i][j] indicates an edge from node i to node j.
(You can also use an integer matrix with 0s and 1s.)
<br />
- In an **undirected graph**, an adjacency matrix will be **symmetric**. 
- In a **directed graph**, it will **not (necessarily) be**. 

<img width="663" alt="Screen Shot 2019-09-12 at 3 45 01 PM" src="https://user-images.githubusercontent.com/46575719/64826042-51fd7b00-d574-11e9-9f01-a389a938cae9.png">

<Supplemental Explanation> <br />
The same graph algorithms that are used on adjacency lists (breadth-first search, etc.) can be performed with adjacency matrices, but they may be somewhat less efficient. In the adjacency list representation, you can easily iterate through the neighbors of a node. In the adjacency matrix representation, you will need to iterate through all the nodes to identify a node's neighbors. 

### Graph Search 

The two most common ways to search a graph are depth-frist search and breadth-first search. <br />

- In depth-first search (DFS), we start at the root (or another arbitrarily selected node) and explore each branch compeletely before moving on to the next branch. That is, we go deep first (hence thename depth-first search) before we go wide.
- In bread-first search (BFS), we start at the root (or another arbitrarily selected node) and explore each neighbor before going on to any of their children. That is, we go wide (hence the name depth-first search) before we go deep.

See the below depiction of a graph and its depth-first and breadth-first search (assuming neighbors are iterated in numerical order).

<img width="660" alt="Screen Shot 2019-09-12 at 1 31 36 PM" src="https://user-images.githubusercontent.com/46575719/64818797-aea36a80-d561-11e9-81c2-312b652caf31.png">

