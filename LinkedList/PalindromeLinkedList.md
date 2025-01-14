
# Palindrome Linked List

## Problem Description

Given the `head` of a singly linked list, determine whether it is a palindrome.

### Examples:

**Example 1:**
```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:**
```
Input: head = [1,2]
Output: false
```

### Constraints:
- The number of nodes in the list is in the range `[1, 10^5]`.
- `0 <= Node.val <= 9`

---

## Approach

### Method 1: Using Stack (Space O(n))

1. Traverse the linked list and push all node values onto a stack.
2. Traverse the linked list again, popping elements from the stack and comparing them with the current node value.
3. If all values match, the linked list is a palindrome.

---

### Method 2: In-Place Reversal (Space O(1))

1. Use the slow and fast pointer technique to find the middle of the list.
2. Reverse the second half of the list.
3. Compare the first half with the reversed second half.
4. Optionally, restore the original list structure.

---

## Code Implementation

### Java Solution Using In-Place Reversal:

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }

        // Step 1: Find the middle of the linked list
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Step 2: Reverse the second half of the linked list
        ListNode reversedHead = reverse(slow);

        // Step 3: Compare the first and second halves
        ListNode p1 = head;
        ListNode p2 = reversedHead;
        while (p2 != null) { // Compare until the end of the second half
            if (p1.val != p2.val) {
                return false;
            }
            p1 = p1.next;
            p2 = p2.next;
        }

        // Step 4: Optional - Restore the original list structure
        reverse(reversedHead);

        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode nextNode = head.next;
            head.next = prev;
            prev = head;
            head = nextNode;
        }
        return prev;
    }
}
```

---

## Complexity Analysis

### Time Complexity:
- **Finding the Middle:** \(O(n)\)
- **Reversing the Second Half:** \(O(n)\)
- **Comparing Both Halves:** \(O(n)\)
- **Overall:** \(O(n)\)

### Space Complexity:
- The in-place reversal approach uses \(O(1)\) extra space.

---

## Notes
- This solution satisfies the \(O(n)\) time and \(O(1)\) space constraints.
- Use simpler stack-based or array-based solutions if \(O(1)\) space isn't required.

---

## Related Problems
- Reverse a Linked List
- Find Middle of a Linked List
- Merge Two Sorted Lists
