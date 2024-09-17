---
tags:
  - reactjs
  - frontend
  - interview
---
# Diffing

The diffing algorithm, also known as the reconciliation algorithm, is a crucial part of React's Virtual DOM (VDOM) system. It is responsible for efficiently updating the real DOM to match the changes in the VDOM. The goal of the diffing algorithm is to minimize the number of operations performed on the real DOM, which can be slow and expensive.

### How the Diffing Algorithm Works

The diffing algorithm compares two VDOM trees: the previous version and the current version. By identifying the differences between these two trees, React can update only the parts of the real DOM that have changed, instead of re-rendering the entire DOM. This process is broken down into several key steps:

1. **Element Type Comparison**:
    
    - If the root elements of the two trees are of different types, React will replace the old tree with the new tree entirely. For example, if a `<div>` is replaced with a `<span>`, the entire subtree under the `<div>` will be unmounted and a new subtree under the `<span>` will be created.
2. **Attribute Comparison**:
    
    - If the root elements are of the same type, React compares their attributes and updates only the attributes that have changed.
3. **Child Element Comparison**:
    
    - React recursively compares the children of the root elements. This comparison is where most of the optimization occurs. React uses several strategies to efficiently compare child elements, particularly when handling lists of elements.

### Handling Lists and Keys

When dealing with lists of elements, React uses the `key` attribute to optimize the diffing process. The `key` attribute helps React identify which items have changed, been added, or been removed. Here’s how it works:

1. **Unique Keys**:
    
    - Each element in a list should have a unique `key` prop. This allows React to distinguish between different elements in the list.
2. **Efficient Updates**:
    
    - With keys, React can determine which elements have moved, been added, or been removed. This minimizes the number of DOM operations required to update the list.

### Example of Diffing Algorithm

Consider the following example where the state of a component changes, causing a re-render:

**Initial VDOM:**

jsx

Copy code

`<ul>   <li key="1">Item 1</li>   <li key="2">Item 2</li>   <li key="3">Item 3</li> </ul>`

**Updated VDOM:**

jsx

Copy code

`<ul>   <li key="1">Item 1</li>   <li key="3">Item 3</li>   <li key="2">Item 2</li>   <li key="4">Item 4</li> </ul>`

Without keys, React would have to re-render the entire list, as it wouldn’t be able to identify the changes efficiently. However, with keys, React can:

- Identify that `Item 1` is unchanged.
- Identify that `Item 2` has moved.
- Identify that `Item 3` is unchanged.
- Identify that `Item 4` has been added.

### Optimizations in Diffing Algorithm

1. **Tree Diffing**:
    
    - React limits the comparison to elements on the same level. It does not compare elements from different levels, which reduces the complexity from `O(n^3)` to `O(n)`.
2. **Component Diffing**:
    
    - If the component type (class or functional) is the same, React compares their props and states. Otherwise, React treats them as completely different and replaces the old component with the new one.
3. **Element Diffing**:
    
    - For elements of the same type, React compares their attributes and updates only the changed attributes.

### Conclusion

The diffing algorithm is a core part of React’s performance optimizations. By comparing two VDOM trees and applying the minimal number of changes to the real DOM, React ensures efficient updates and smooth user experiences. The use of keys in lists further enhances this efficiency, allowing React to handle dynamic data effectively.