
```cpp
class Solution {
public:
    int linearSearch(const vector<int>& nums, int target) {
        // Use pre-increment for better practice
        for (int i = 0; i < nums.size(); ++i) { 
            if (nums[i] == target) {
                // Early return if target is found
                return i;
            }
        }
        // Return -1 if target is not found
        return -1; 
    }
};

```

### **Time Complexity Analysis**

1. **Best Case**: O(1)
    
    - The target element is found at the first position of the array.
2. **Worst Case**: O(n)
    
    - The target element is at the last position or not in the array, requiring a complete traversal of the array.
3. **Average Case**: O(n)
    
    - On average, the target element is found after traversing half the array, but the order of growth remains linear.

---

### **Space Complexity**

1. **Space Used**: O(1)
    - Linear search operates directly on the input array without using any additional space.

### **Key Takeaway**

Use **linear search** when the data is unsorted, small, or dynamically changing. For large and sorted datasets, binary search is the optimal choice. Always weigh **simplicity vs. efficiency** for the problem at hand.



### **Problem Category Type**:

- **Category**: Searching
- **Subcategory**: Linear Search