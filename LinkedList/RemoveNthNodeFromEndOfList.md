
# Remove Nth Node From End of List

## Problem Description

Given the `head` of a linked list, remove the `n`th node from the end of the list and return its head.

### Example 1:
**Input:**
```
head = [1,2,3,4,5], n = 2
```
**Output:**
```
[1,2,3,5]
```

### Example 2:
**Input:**
```
head = [1], n = 1
```
**Output:**
```
[]
```

### Example 3:
**Input:**
```
head = [1,2], n = 1
```
**Output:**
```
[1]
```

## Constraints
- The number of nodes in the list is `sz`.
- \( 1 \leq sz \leq 30 \)
- \( 0 \leq \text{Node.val} \leq 100 \)
- \( 1 \leq n \leq sz \)

### Follow-up:
Could you solve this in one pass?

---

## Solution in Java

```java
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // Create a dummy node to handle edge cases
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;

        // Move the fast pointer n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }

        // Move both pointers until fast reaches the end
        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }

        // Remove the nth node
        slow.next = slow.next.next;

        return dummy.next;
    }
}
```

---

## Explanation

### Algorithm
1. **Dummy Node**:
   - Add a dummy node before the head to simplify edge cases (e.g., removing the first node).
2. **Two Pointers**:
   - Use two pointers, `slow` and `fast`. Move `fast` \( n+1 \) steps ahead, maintaining a gap of \( n \) nodes between them.
   - Move both pointers one step at a time until `fast` reaches the end. Now, `slow` is positioned right before the target node.
3. **Node Removal**:
   - Update `slow.next` to skip the target node, effectively removing it.

### Complexity Analysis
- **Time Complexity**: \( O(L) \), where \( L \) is the length of the linked list. The list is traversed once.
- **Space Complexity**: \( O(1) \), no additional space is used.

---

## Notes
- Handles edge cases such as:
  - Removing the first node of the list.
  - Removing the only node in a single-node list.
- Efficient solution with a single traversal using the two-pointer technique.

---

## Related Problems
- Reverse a linked list
- Detect a cycle in a linked list
- Merge two sorted linked lists
