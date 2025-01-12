
# Longest Common Prefix

## Problem Description

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

**Examples**:

**Example 1**:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

**Example 2**:
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Constraints**:
- 1 <= strs.length <= 200
- 0 <= strs[i].length <= 200
- strs[i] consists of only lowercase English letters if it is non-empty.

---

## Approach

To find the longest common prefix:
1. Identify the shortest string in the array, as the common prefix cannot be longer than this string.
2. Compare each character of the shortest string against the corresponding characters in all other strings.
3. Stop when a mismatch is found or all characters of the shortest string have been compared.

### Algorithm
1. **Find the Shortest String**:
    - Iterate through the array to determine the shortest string.
2. **Compare Characters**:
    - Traverse each character of the shortest string.
    - For each character, compare it with the corresponding character in all other strings.
3. **Return Result**:
    - Append matching characters to the result.
    - Stop and return the result when a mismatch is found.

---

## Code Implementation

### Java Code:
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }

        // Find the shortest string
        String shortest = strs[0];
        for (String str : strs) {
            if (str.length() < shortest.length()) {
                shortest = str;
            }
        }

        // Compare character by character
        StringBuilder sb = new StringBuilder();
        char[] arr = shortest.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            for (String str : strs) {
                if (str.charAt(i) != arr[i]) {
                    return sb.toString();
                }
            }
            sb.append(arr[i]);
        }

        return sb.toString();
    }
}
```

---

## Complexity Analysis

- **Time Complexity**: \(O(S)\), where \(S\) is the sum of all characters in all strings.
  - Each character is compared at most once.
- **Space Complexity**: \(O(1)\), as only a `StringBuilder` and a few variables are used.

---

## Edge Cases

1. Empty array or null input:
   - Input: `[]`
   - Output: `""`
2. Single string in the array:
   - Input: `["hello"]`
   - Output: `"hello"`
3. No common prefix:
   - Input: `["dog", "racecar", "car"]`
   - Output: `""`
4. All strings identical:
   - Input: `["repeat", "repeat", "repeat"]`
   - Output: `"repeat"`

---

## Notes

1. Using the shortest string reduces unnecessary comparisons.
2. This approach ensures correctness and efficiency for both small and large inputs.
