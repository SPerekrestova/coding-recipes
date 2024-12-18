# First Unique Character

## Problem Description

Find the index of the first non-repeating character in a string. Return `-1` if no unique character exists.

**Example:**

**Input:** `"leetcode"`  
**Output:** `0` (The first unique character is `'l'`.)

**Input:** `"aabb"`  
**Output:** `-1` (No unique characters.)

---

## Approach

The solution involves analyzing the frequency of each character and determining the first one with a frequency of 1.

---

## Algorithm

### Step 1: Count Frequencies

- Use a frequency map (or array for limited character sets) to count occurrences of each character.

### Step 2: Find the First Unique Character

- Iterate through the string to find the first character with a frequency of 1.

---

## Code Implementation

### Optimized Java Solution
```java
class Solution {
    public int firstUniqChar(String s) {
        // Step 1: Count frequency of each character
        int[] charCount = new int[26];
        for (char c : s.toCharArray()) {
            charCount[c - 'a']++;
        }

        // Step 2: Find the first character with frequency 1
        for (int i = 0; i < s.length(); i++) {
            if (charCount[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }

        return -1; // No unique character found
    }
}
```

---

## Complexity Analysis

### Time Complexity

- **Counting Frequencies:** Requires \(O(n)\).
- **Finding the First Unique Character:** Requires \(O(n)\).
- **Overall:** \(O(n)\).

### Space Complexity

- Uses a fixed-size array for frequencies, so the space complexity is \(O(1)\).

---

## Edge Cases

1. **Empty string (`""`)**: Return `-1`.
2. **Single character string (`"a"`)**: Return `0`.
3. **All characters are identical (`"aaaa"`)**: Return `-1`.

---

## Related Problems

1. **Longest substring without repeating characters.**
2. **Find the most frequent character in a string.**
3. **Sort characters by frequency.**

---

## Notes

This solution is efficient and works well for input restricted to lowercase English letters. For more general cases, a `HashMap` can be used to store frequencies, supporting Unicode and mixed-case inputs.

