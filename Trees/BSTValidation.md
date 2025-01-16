# Binary Search Tree (BST) Validation

## Problem Description

Write a function to determine if a given binary tree is a valid binary search tree (BST). A BST is defined as a binary tree in which, for each node:

- All the nodes in the left subtree have values less than the node's value.
- All the nodes in the right subtree have values greater than the node's value.

**Constraints:**
- Duplicate values are not allowed in the BST.

---

## Approach

### Recursive Solution
The recursive approach leverages a helper function to pass the valid range for each node:
- The left child must have a value strictly less than the current node's value.
- The right child must have a value strictly greater than the current node's value.

**Algorithm:**
1. Use a helper function `validate(TreeNode node, long min, long max)`.
2. For each node:
    - Return `false` if the node's value is not within the range `(min, max)`.
    - Recursively validate the left subtree with the updated range `(min, node.val)`.
    - Recursively validate the right subtree with the updated range `(node.val, max)`.
3. Return `true` if all nodes satisfy the BST property.

---

## Code Implementation

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean validate(TreeNode node, long min, long max) {
        // Base case: an empty node is a valid BST
        if (node == null) {
            return true;
        }

        // Check the current node's value
        if (node.val <= min || node.val >= max) {
            return false;
        }

        // Recursively validate the left and right subtrees
        return validate(node.left, min, node.val) && validate(node.right, node.val, max);
    }
}
```

---

## Complexity Analysis

### Time Complexity
- Each node is visited once, so the time complexity is **O(n)**, where `n` is the number of nodes in the tree.

### Space Complexity
- The space complexity is **O(h)**, where `h` is the height of the tree, due to the recursive stack. In the worst case (unbalanced tree), `h = O(n)`.

---

## Edge Cases
1. **Empty Tree:** An empty tree is a valid BST.
2. **Single Node Tree:** A tree with one node is a valid BST.
3. **Negative Values:** Ensure that the tree handles negative values correctly.
4. **Large Values:** Use `long` for the range to handle edge cases with very large or very small integers.

---

## Testing

### Test Case 1: Balanced BST
**Input:**
```
    2
   / \
  1   3
```
**Output:** `true`

### Test Case 2: Invalid BST
**Input:**
```
    5
   / \
  1   4
     / \
    3   6
```
**Output:** `false`

### Test Case 3: Single Node Tree
**Input:**
```
    1
```
**Output:** `true`

### Test Case 4: Empty Tree
**Input:** `null`
**Output:** `true`

---

## Notes

- Avoid common pitfalls such as not updating the valid range properly when traversing subtrees.
- This solution ensures that all nodes are within the correct range, satisfying the BST property for all possible inputs.
