---
tags:
  - dsa
  - tree
  - bst
documentations: https://www.geeksforgeeks.org/segment-tree-data-structure/?ref=header_search
---
# What is this - [Read more](https://www.geeksforgeeks.org/segment-tree-data-structure/?ref=header_search)

It is also as special type of BST but this is used on arrays to answer range queries easily and faster
- Range or segments given eg [0, 2] and queries such as **sum(0, 2)**, **update(2, 10)**
- Brute force will takt O(r - I) or O(n) and O(1) respectively.
- some nodes of the tree storing the sum of some nodes of the array.
- Height al always log n. So space complexity O(n)- n nodes at leaves and approx n non leaf nodes.
- Like Heap, the segment tree is also represented as an array.
- Time complexity for tree construction is O(n).
- Sum [0, 4] = 12 from array - 5 accesses.
- From tree [0 - 3] and [4 - 4] - 2 accesses
- Update - change in lead node and all the path till root changes O(log n)
- For any sum (l, r) max n in the interval we need only O(log n) accesses max.

![[segment-tree1.png]]