---
Topic: Balanced binary search tree
tags:
  - dsa
  - bst
  - avltree
---
# What is AVL tree !
> An ****AVL tree**** defined as a self-balancing [****Binary Search Tree****](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) (BST) where the difference between heights of left and right subtrees for any node cannot be more than one.

The difference between the heights of the left subtree and the right subtree for any node is known as the ****balance factor**** of the node.

The AVL tree is named after its inventors, Georgy Adelson-Velsky and Evgenii Landis, who published it in their 1962 paper “An algorithm for the organization of information”.

---
# Balance Factor!
The balance factor is the main factor which lets the tree decide that when its time to just balance the whole tree again.
> Balance factor = Height(Left subtree) - Height(Right subtree)

---

#  What to do if a AVL tree is not balanced
First of all we have to get the balance factor of the tree and if its not balanced then we have to perform some rotations based on the balance factor.

**Rotations can be:**
- Left rotation (single rotation)
- Right rotation (single rotation)
- Left-right rotation (double rotation, RR followed by LL)
- Right-left rotation (double rotation, LL followed by RR)
