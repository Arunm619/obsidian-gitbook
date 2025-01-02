

### **Question**

Given a sorted array of integers `nums` with 0-based indexing, find the index of a specified target integer `X`. If the target is found in the array, return its index. If the target is not found, return `-1`.

---

### **Intuition**

Binary search leverages the sorted property of the array to reduce the search space by half at each step. It compares the middle element of the current range with the target:

- If the middle element equals the target, return its index.
- If the middle element is smaller, the target must be in the right half.
- If the middle element is larger, the target must be in the left half.

This divide-and-conquer strategy ensures an efficient search.

---

### **Solution (All Approaches)**

#### **1. Iterative Binary Search**

Iteratively update the bounds of the search space.

#### **2. Recursive Binary Search**

Implement binary search recursively by reducing the problem size at each step.

Comparison:

- Iterative is often preferred due to its simplicity and lack of function call overhead.
- Recursive is more elegant but may run into stack overflow for very large arrays.

---

### **Implementation**

#### Iterative Approach

```cpp
#include <vector>
using namespace std;

int binarySearch(const vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid; // Target found
        } else if (nums[mid] < target) {
            left = mid + 1; // Search right half
        } else {
            right = mid - 1; // Search left half
        }
    }

    return -1; // Target not found
}
```

#### Recursive Approach

```cpp
#include <vector>
using namespace std;

int binarySearchRecursive(const vector<int>& nums, int target, int left, int right) {
    if (left > right) return -1; // Base case: Target not found

    int mid = left + (right - left) / 2;
	// Target found
    if (nums[mid] == target) return mid; 
    else if (nums[mid] < target) return binarySearchRecursive(nums, target, mid + 1, right); // Search right half
    else return binarySearchRecursive(nums, target, left, mid - 1); // Search left half
}
```

---

### **Edge Cases**

1. Empty array (`nums = []`) → Return `-1`.
2. Single element (`nums = [5]`, `target = 5` or `3`) → Handle properly.
3. Target not in array (`nums = [1, 2, 3, 4]`, `target = 10`) → Return `-1`.
4. Target at boundaries (`nums = [1, 3, 5]`, `target = 1` or `5`).

---

### **Time Complexity and Space Complexity**

1. **Time Complexity**: $O(\log N)$
    Each step reduces the search space by half.
    
2. **Space Complexity**:
    
    - Iterative: $O(1)$ (constant space).
    - Recursive: $O(\log N)$(stack space for recursion).

---

### **Key Takeaways from this Problem**

- Binary search is efficient for searching in sorted datasets.
- Always calculate `mid` as `left + (right - left) / 2` to avoid overflow.
- Understand both iterative and recursive approaches to suit different scenarios.

---

### **Mistakes and Challenges from this Problem**

- Forgetting to update `left` and `right` correctly, leading to infinite loops.
- Not handling edge cases like an empty array or single-element arrays.

---

### **Real-World Application of this Problem**

- Searching in sorted datasets, like finding records in a sorted database or log files.
- Used in optimization problems where a sorted structure can be binary-searched for efficient solutions.

---

### **Problem Category Type**

- Arrays, Searching, Divide-and-Conquer

---

