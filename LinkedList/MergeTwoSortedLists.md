
# Merge Two Sorted Lists

## Problem Description

You are given the heads of two sorted linked lists, `list1` and `list2`.  
Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.  

**Return the head of the merged linked list.**

---

## Approach

The approach involves merging the two lists in place by reusing the existing nodes, rather than creating new ones.  
We use a **dummy node** to simplify the process, and then iterate through both lists, comparing their values to merge them in sorted order.

### Key Steps:

1. **Initialize a Dummy Node**:
   - Use a dummy node as the starting point for the merged list.
   - Maintain a pointer (`current`) to track the current end of the merged list.

2. **Iterate Through Both Lists**:
   - Compare the current nodes of `list1` and `list2`.
   - Attach the smaller node to the merged list by updating `current.next`.
   - Move the pointer of the chosen list (`list1` or `list2`) forward.

3. **Attach Remaining Nodes**:
   - Once one of the lists is exhausted, attach the remaining nodes of the other list to the merged list.

4. **Return the Merged List**:
   - Return `dummy.next` as the head of the merged list.

---

## Code Implementation

### Java Solution:
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // Create a dummy node to simplify the merging process
        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        // Traverse both lists until one is exhausted
        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                current.next = list1;
                list1 = list1.next;
            } else {
                current.next = list2;
                list2 = list2.next;
            }
            current = current.next;
        }

        // Attach the remaining nodes from the non-empty list
        if (list1 != null) {
            current.next = list1;
        } else {
            current.next = list2;
        }

        // Return the merged list, starting from the next node of dummy
        return dummy.next;
    }
}
```

---

## Complexity Analysis

- **Time Complexity**: \(O(n + m)\), where \(n\) and \(m\) are the lengths of `list1` and `list2`.
- **Space Complexity**: \(O(1)\), as the merge is done in place without using additional memory.

---

## Edge Cases

1. Both `list1` and `list2` are empty (`[]`).
2. One list is empty, and the other is non-empty (e.g., `list1 = [], list2 = [0]`).
3. Both lists have the same elements (e.g., `list1 = [1, 1, 1]`, `list2 = [1, 1]`).

---

## Why This Works

- The solution reuses the existing nodes in `list1` and `list2` by updating their `next` pointers.
- No new nodes are created; the process involves linking the nodes in sorted order, making it efficient in terms of both time and space.

---

## Notes

- This problem is fundamental for understanding **linked list manipulation** and is commonly used in interviews.
- The dummy node simplifies edge cases (e.g., empty lists) and eliminates the need for special conditions when initializing the merged list.

---
