## Binary Heaps (Min-Heaps and Max-Heaps)

1) We'll just discuss min-heaps here. Max-heaps are essentially equivalent, but the elements are in descending order rather than ascending order. <br />

2) A min-heap is a **complete binary tree** (that is, totally filled other than the rightmost elements on the last level) where each node is smaller than its children. The root, therefore, is the minimum element in the tree. <br />

3) We have two key operations on a min-heap: **insert** and **extract_min**.

**Insert**
1) When we insert into a min-heap, we always start by inserting the element at the bottom. We insert at the rightmost spot so as to maintain the complete tree property. <br />
2) Then, we "fix" the tree by swapping the new element with its parent, until we find an appropriate spot for the element. We essentially bubble up the minimum element. 

<img width="787" alt="Screen Shot 2019-09-11 at 3 44 15 PM" src="https://user-images.githubusercontent.com/46575719/64740706-177bdb80-d4ab-11e9-9c84-08aaff387526.png">
This takes O(log n) time, where n is the number of nodes in the heap. <br />

**Extract Minimum Element** <br />
Finding the minimum element of a min-heap is easy: it's always at the top. The trickier part is how to remove it. (In fact, this isn't that tricky.) <br />

1) We remove the minimum element and swap it with the last element in the heap (the bottommost, rightmost element). 
2) Then, we bubble down this element, swapping it with one of its children until the min-heap property is restored. 

-> Do we swap it with the left child or the right child? That depends on their values. There's no inherent ordering between the left and right element, but you'll need to take the smaller one in order to maintain the min-heap ordering. 
<img width="761" alt="Screen Shot 2019-09-11 at 3 59 00 PM" src="https://user-images.githubusercontent.com/46575719/64741374-1b106200-d4ad-11e9-84c9-81a179155e0b.png">

This algorithm wil also take O(log n) time.
