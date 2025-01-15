### Recipe: Find Maximum Depth of a Binary Tree

#### Problem Description:
Write a function to determine the maximum depth of a binary tree. The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

#### Solution:
The problem can be solved efficiently using either Depth-First Search (DFS) or Breadth-First Search (BFS). Below, we provide implementations for both methods in Java.

---

#### Approach 1: Recursive DFS
This approach uses recursion to traverse the tree and calculate the maximum depth.

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
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```

---

#### Approach 2: Iterative DFS (Using a Stack)
This approach avoids recursion and uses an explicit stack to traverse the tree iteratively.

```java
import java.util.*;

class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Stack<Pair<TreeNode, Integer>> stack = new Stack<>();
        stack.push(new Pair<>(root, 1));
        int maxDepth = 0;

        while (!stack.isEmpty()) {
            Pair<TreeNode, Integer> current = stack.pop();
            TreeNode node = current.getKey();
            int depth = current.getValue();

            maxDepth = Math.max(maxDepth, depth);

            if (node.left != null) {
                stack.push(new Pair<>(node.left, depth + 1));
            }
            if (node.right != null) {
                stack.push(new Pair<>(node.right, depth + 1));
            }
        }

        return maxDepth;
    }
}
```

---

#### Approach 3: BFS (Level Order Traversal)
This approach calculates the maximum depth by traversing the tree level by level.

```java
import java.util.*;

class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int level = 0;

        while (!queue.isEmpty()) {
            int size = queue.size(); // Number of nodes at the current level
            for (int i = 0; i < size; i++) {
                TreeNode current = queue.poll();

                if (current.left != null) {
                    queue.add(current.left);
                }
                if (current.right != null) {
                    queue.add(current.right);
                }
            }
            level++;
        }

        return level;
    }
}
```

---

#### Complexity Analysis:
| Approach            | Time Complexity | Space Complexity |
|---------------------|-----------------|------------------|
| Recursive DFS       | O(n)            | O(h)             |
| Iterative DFS       | O(n)            | O(h)             |
| BFS (Level Order)   | O(n)            | O(w)             |

- **n**: Number of nodes in the tree.
- **h**: Height of the tree.
- **w**: Maximum width of the tree (number of nodes at the widest level).

---

#### Notes:
- Recursive DFS is simpler and more intuitive but can lead to stack overflow for deep trees.
- Iterative DFS avoids recursion and is robust for deep or skewed trees.
- BFS is useful for level-order traversal and guarantees the shortest path in unweighted graphs.

---

Choose the implementation based on your specific use case or constraints.
