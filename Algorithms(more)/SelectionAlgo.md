# Selection

### Selection Algorithms
- Selection algorithm is an algorithm **for finding the k-th smallest / largest number** in a list / array such a number is called the k-th order statistic.
    - For example: finding maximum, minimum or median.
- The aim is **to achieve O(N) linear time complexity** for this particular operation!
- Methods: quickselect, median of medians method...

### Sorting
- Intuition: let’s sort the array in which we want to find the given item.
- After sorting -> we can access the item **with the help of the index**.
    - For example: if we sort an array in descending order, the array[0] yields the maximum item 
- Inefficient approach: if we want to find just a single item ( maximum, minimum or median )
- Efficient approach: if we want to find several items at the same time 
    - Why?  O(N*logN) versus O(N)
    - Intuition: selection can be reduced to sorting and vice versa.
    
### Data Structures
- We can use a data structure in order to find items.
- Sublinear time can be reached: O(logN).
    - For example: construct a balanced binary search tree or a heap.
- Problem: it has some memory complexity, we have to construct the data structure first!
- So overall, not the best solution.

### Online Selection
- Online algorithm: we want to find a given item ( maximum, minimum or median ) of a stream.
- We keep downloading data and we want to find items at runtime.
- Problem: we do not know all the values in advance.
- We will not be able to construct an algorithm that finds the best solution: we can have a good guess ... a value that *probably* are looking for.
- "**secretary problem**"

## QuickSelect
- It is a selection algorithm to find the k-th smallest / largest item in an **unordered array**
- Hoare constructed the algorithm -> "Hoare algoithm"
- It has a very good average case running time: **O(N)**
    - Worst case scenario: O(N)
- In-place algorithm
- Concept is similar to quicksort
    - Choose a pivot element at random
    - Partition the array
    - Instead of recursing into both sides, we just take one side
    - **O(N*logN) -> O(N)**
    

### Hoare Algorithm
1) Partition
The partition method is just for partitioning the array according to the pivot.
  - Choose a pivot value at random: we generate a random number in the range [firstIndex, lastIndex]
  - Rearranges the list in a way that all elements less than pivot are on the left side of pivot and others on the right.
  It then returns index of the pivot element.

2) Select

  
  
  
  
  
  
