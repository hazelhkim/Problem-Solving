## Graphs

TREE
- A tree is actually a type of graph, but not all graphs are trees. 
- A tree is a connected graph without cycles. 
<br />

GRAPH <br />

- A graph is a collectin of nodes with edges between (some of) them. 
- Graphs can be either directed (like the following graph) or undirected. 
- The graph might consist of multiple isolated subgraphs. 
- The graph can also have cycles (or not). 

<br />

- **directed edges** : a one-way street
- **undirected edges** : like a two-way street
- **connected graph** : a graph that has a path between every pair of vertices. 
- **acyclic graph** : a graph that has no cycles. 

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

- In **depth-first search (DFS)**, we start at the root (or another arbitrarily selected node) and explore each branch compeletely before moving on to the next branch. That is, we go deep first (hence thename depth-first search) before we go wide.
- In **bread-first search (BFS)**, we start at the root (or another arbitrarily selected node) and explore each neighbor before going on to any of their children. That is, we go wide (hence the name depth-first search) before we go deep.

See the below depiction of a graph and its depth-first and breadth-first search (assuming neighbors are iterated in numerical order).

<img width="660" alt="Screen Shot 2019-09-12 at 1 31 36 PM" src="https://user-images.githubusercontent.com/46575719/64818797-aea36a80-d561-11e9-81c2-312b652caf31.png">

- Breadth-first search and depth-first search tend to be used in different scenarios. DFS is often preferred if we want to visit every node in the graph. Both will work just fine, but depth-first search is a bit simpler. 
- However, if we want to find the shortest path (or just any path) between two nodes, BFS is generally better.
- Consider representing all the friendships in the entire world in a graph and trying to find a path of firendships between Ash and Vanessa.

### Depth-First Search (DFS)
In DFS, we visit a node a and then iterate through each of a's neighbors. When visiting a node b that is a neighbor of a, we visit all of b's neighbors before going on to a's other neighbors. That is, a exhaustively searches b's branch before any of its other neighbors. <br />

Note that pre-order and other forms of tree traversal are a form of DFS. The key difference is that when implementing this algorithm for a graph, we must check if the node has been visited. If we don't, we ris getting stuck in an infinite loop. <br />

The pseudocode below implementing DFS.
```java 
void search(Node root) {
    if(root == null) return;
    visit(root);
    root.visited = true;
    for each (Node n in root.adjacent) {
        if(n.visited == false) {
            search(n);
        }
    }
}

```

### Breadth-First Search (BFS)
BFS is a bit less intuitive, and many interviewes struggle with the implementation unless they are already familiar with it. The main tripping point is the (false) assumption that BFS is recursive. It's not. Instead, it uses a queue. <br />

In BFS, node a visits each of a's neighbors before visiting any of their neighbors. You can think of this as searching level by level out from a. An alternative solution involving a queue usually works best.
```java
void search (Node root) {
    Queue queue = new Queue();
    root.marked = true; 
    queue.enqueue(root); // Add to the end of queue.
    
    while( !queue.isEmpty() ) {
        Node r = queue.dequeue(); // Remove from the front of the queue.
        visit(r);
        foreach (Node n in r.adjacent) {
            if(n.marked == false) {
                n.marked = true;
                queue.enqueue(n);
            }
        }
    }

}
```
If you are asked to implement BFS, the key thing to remember is the use of the queue. The rest of the algorithm flows from this fact. 

### Bidirectional Search
Bidirectional search is used to find the shortest path between a sorce and destination node. It operates by essentially running two simultaneous breadth-first searches, one from each node. When their searches collide, we have found a path.

<img width="650" alt="Screen Shot 2019-09-13 at 10 36 57 AM" src="https://user-images.githubusercontent.com/46575719/64882668-74de6c80-d612-11e9-9380-a9562f055276.png">

To see why this is faster, consider a graph where every node has at most k adjacent nodes and shortest path from node s to node t has length d. 

- In traditional breadth-first search, we would search up to k nodes in the first "level" of the search. In the second level, we would search up to k nodes for each of those first k nodes, so k^2 nodes total (thus far). We would do this d times, so that's O(K^d) nodes. 
- In bidirectional search, we have two searches that collide after approximately d/2 levels (the midpoint of the path). The search form s visits approximately k^(d/2), as does the search from t. That's approximately 2K^(d/2), or O(K^(d/2)), nodes total.

**This might seem like a minor difference, but it's not. It's huge. Recall that (K^(d/2))* (K^(d/2)) = K^d. The bidirectional search is actually faster by a factor of K^(d/2).**
<br />
*Put another way: if our system could only support searching "friend of friend" paths in breadth-first search, it could not likely support "friend of friend of friend of friend" paths. We can suport paths that are twice as long.*












