

### **Question**

Given a sorted array `nums`, find the smallest index i such that $\text{nums}[i] \geq x$. 
If no such index exists, return `nums.size()`.

---

### **Intuition**

The goal is to find the **lower bound**, the smallest index where the value is greater than or equal to xx. By using binary search, we iteratively narrow down the range to find the desired index:

1. If the middle element satisfies $\text{nums[mid]} \geq x$, we record this index and move left to check for smaller indices.
2. Otherwise, we shift right to find a valid value.

This ensures we find the smallest possible index efficiently.

---

### **Solution (Iterative Binary Search)**

We maintain a result variable initialized to `nums.size()` to handle cases where no valid index exists. We then use binary search to minimize the potential result.

---

### **Implementation**

```cpp
class Solution {
public:
    int lowerBound(vector<int> &nums, int x) {
        int low = 0, high = nums.size() - 1;
        int result = nums.size(); // Default value if no index satisfies the condition
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] >= x) {
                result = mid;     // Update result with the current valid index
                high = mid - 1;   // Search the left half
            } else {
                low = mid + 1;    // Search the right half
            }
        }
        return result;
    }
};
```

---

### **Edge Cases**

1. **Empty Array**: `nums = []` → Return `nums.size() = 0`.
2. **All Elements Smaller**: xx greater than all elements → Return `nums.size()`.
3. **All Elements Greater or Equal**: xx smaller than all elements → Return `0`.
4. **Exact Match**: If xx exists, return the first occurrence index.

---

### **Time Complexity and Space Complexity**

1. **Time Complexity**: $O(\log N)$, due to the binary search approach.
2. **Space Complexity**: $O(1)$, as no additional space is used.

---

### **Key Takeaways from this Problem**

- Understand the concept of **lower bound** and its utility in binary search.
- Handle edge cases gracefully to ensure robustness.
- This approach generalizes well to finding ranges or solving related search problems.

---

### **Mistakes and Challenges from this Problem**

- Forgetting to update `result` when $\text{nums[mid]} \geq x$.
- Incorrectly handling the bounds (`low` and `high`), leading to infinite loops or incorrect results.

---

### **Real-World Application of this Problem**

- **Databases**: Efficiently find a record with a value greater than or equal to a given key.
- **Competitive Programming**: Problems involving ranges and constraints often leverage this concept.

---

### **Problem Category Type**

- Arrays, Binary Search, Searching

