
# Reverse Linked List

## Problem Description
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

---

## Approach 1: Iterative Solution

### Algorithm
1. **Initialize**:
   - `prev` to `null` (this will point to the reversed portion of the list).
   - `current` to `head` (this traverses the original list).
2. Traverse the list:
   - Store the next node (`nextNode`).
   - Reverse the link by pointing `current.next` to `prev`.
   - Move `prev` to the current node and `current` to `nextNode`.
3. When traversal ends, `prev` is the new head of the reversed list.

---

### Code (Java)
```java
class ListNode {
    int val;
    ListNode next;

    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;

        while (current != null) {
            ListNode nextNode = current.next; // Store the next node
            current.next = prev;             // Reverse the link
            prev = current;                  // Move prev to the current node
            current = nextNode;              // Move to the next node
        }

        return prev; // New head of the reversed list
    }
}
```

---

## Approach 2: Recursive Solution

### Algorithm
1. **Base Case**: If the `head` is `null` or it is the last node, return `head`.
2. **Recursive Step**:
   - Call `reverseList` on the rest of the list (`head.next`).
   - Reverse the link for the current node (`head.next.next = head`).
   - Set `head.next = null` to terminate the original link.
3. Return the new head of the reversed list from the recursion.

---

### Code (Java)
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        // Base case: If the list is empty or has only one node
        if (head == null || head.next == null) {
            return head;
        }

        // Recursive call to reverse the rest of the list
        ListNode reversedHead = reverseList(head.next);

        // Reverse the current node's pointer
        head.next.next = head;
        head.next = null;

        return reversedHead; // Return the new head of the reversed list
    }
}
```

---

## Complexity Analysis

### Iterative Solution
- **Time Complexity**: \(O(n)\), where \(n\) is the number of nodes.
- **Space Complexity**: \(O(1)\), as no additional memory is used.

### Recursive Solution
- **Time Complexity**: \(O(n)\), as each node is visited once.
- **Space Complexity**: \(O(n)\), due to recursive stack space.

---

## Examples

### Example 1
**Input**: `head = [1, 2, 3, 4, 5]`  
**Output**: `[5, 4, 3, 2, 1]`

### Example 2
**Input**: `head = [1, 2]`  
**Output**: `[2, 1]`

### Example 3
**Input**: `head = []`  
**Output**: `[]`

---

## Notes
1. Use the **iterative solution** for optimal space complexity.
2. The **recursive solution** is more elegant but consumes extra stack space.
