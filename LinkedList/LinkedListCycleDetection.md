
# Linked List Cycle Detection

## Problem Description

Given the head of a linked list, determine if the linked list contains a cycle.  
A cycle exists if there is a node that can be visited more than once while traversing the list.

**Example Scenarios:**

1. **Input:** `head = [3, 2, 0, -4], pos = 1`  
   **Output:** `true`  
   **Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

2. **Input:** `head = [1, 2], pos = 0`  
   **Output:** `true`  
   **Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

3. **Input:** `head = [1], pos = -1`  
   **Output:** `false`  
   **Explanation:** There is no cycle in the linked list.

---

## Approach

We can solve this problem using the **Floyd’s Cycle Detection Algorithm** (also known as the two-pointer technique).

### Algorithm

1. **Edge Case Check:**
   - If the list is empty (`head == null`) or has only one node (`head.next == null`), there cannot be a cycle. Return `false`.

2. **Two Pointers:**
   - Use two pointers, `slow` and `fast`.
   - `slow` moves one step at a time, while `fast` moves two steps at a time.

3. **Cycle Detection:**
   - If there is a cycle, the `fast` pointer will eventually "lap" the `slow` pointer, causing them to meet.
   - If `fast` reaches the end (`null`), there is no cycle.

---

## Implementation

### Java Code

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;       // Move slow pointer by 1 step
            fast = fast.next.next; // Move fast pointer by 2 steps

            if (slow == fast) {
                return true;       // Cycle detected
            }
        }

        return false; // No cycle detected
    }
}
```

---

## Complexity Analysis

### Time Complexity

- **O(n):** Both `slow` and `fast` traverse the linked list. In the worst case, they visit each node once.

### Space Complexity

- **O(1):** The algorithm uses constant space.

---

## Edge Cases

1. **Empty List:** `head = null`.
2. **Single Node without Cycle:** `head = [1], pos = -1`.
3. **Single Node with Cycle:** `head = [1], pos = 0`.
4. **Large List with a Cycle.**

---

## Notes

- This approach is optimal for detecting cycles in a linked list as it uses constant space and linear time.
- It does not modify the original linked list, preserving its structure.

---

## Follow-Up

Can you extend this solution to **find the starting node of the cycle**?  
(Hint: Use a two-pointer approach after detecting the cycle.)

---
