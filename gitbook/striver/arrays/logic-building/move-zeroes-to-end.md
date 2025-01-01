### Question

**Move all zeros in the given array to the end while maintaining the order of non-zero elements.**

### Intuition

- **Two-pointer approach**: The strategy involves two pointers:
    1. `nzp` (non-zero pointer) - this pointer iterates over the array and finds non-zero elements.
    2. `zp` (zero pointer) - this pointer keeps track of the position where the next non-zero element should be placed.
- As we iterate through the array with `nzp`, we move non-zero elements to the position of `zp`, and after all elements have been processed, we set the remaining positions (from `zp` to the end) to zero.

### Solution (all approaches)

#### Approach 1: Two Pointers (Implemented)

- Use the two-pointer technique:
    - Iterate with `nzp` from left to right.
    - If `nums[nzp] != 0`, place `nums[nzp]` at `nums[zp]` and increment both pointers.
    - If `nums[nzp] == 0`, just increment `nzp`.
- After moving all non-zero elements, fill the rest of the array with zeros starting from `zp`.

#### Approach 2: Swap-based approach

- Another approach could be to swap elements when a zero is encountered with a non-zero element. However, this might introduce unnecessary swaps when the non-zero elements are already in the right place, which can make it less efficient.

### Implementation

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        if (nums.empty()) return;
        int n = nums.size();
        int nzp = 0, zp = 0;

        while (nzp < n) {
            if (nums[nzp] != 0) {
                nums[zp] = nums[nzp];  // Move non-zero element to the 'zp' index
                zp++;  // Increment the 'zp' pointer
            }
            nzp++;  // Move the 'nzp' pointer forward
        }

        // After moving non-zero elements, fill remaining positions with zeros
        while (zp < n) {
            nums[zp] = 0;
            zp++;
        }
    }
};
```

### Edge Cases

1. **Empty array**: If the array is empty (`nums.empty()`), return immediately.
2. **All zeroes**: If the array consists entirely of zeroes, it will correctly leave the array unchanged (since there are no non-zero elements to move).
3. **No zeroes**: If there are no zeroes, the array will remain unchanged.
4. **Single element array**: If the array has only one element (zero or non-zero), it will handle it correctly.

### Time Complexity and Space Complexity

- **Time Complexity**: `O(n)`, where `n` is the length of the array. We are iterating through the array twice—once with `nzp` and once to fill the remaining zeros.
- **Space Complexity**: `O(1)`, because we are modifying the array in place without using extra space.

### Key Takeaways from this Problem

- The two-pointer approach is efficient for problems like this where elements need to be rearranged but without changing the relative order.
- The idea of moving elements as you traverse the array is useful when elements must be processed based on specific conditions (in this case, moving zeros to the end).

### Mistakes and Challenges from this Problem

- A potential mistake could be over-complicating the logic, such as using unnecessary swaps. This implementation avoids that, keeping the logic straightforward.
- Another challenge would be handling edge cases like an array full of zeroes or an empty array, which is efficiently handled here.

### Real-World Application of this Problem

- This kind of problem can be found in applications where you need to maintain a list or queue of items but want to shift certain items (e.g., "empty" values) to the end without disrupting the order of others. For example, in memory management or managing elements in a data stream, this approach can help optimize resource allocation by efficiently grouping non-empty entries.

### Problem Category Type

- Arrays

