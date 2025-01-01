
### **Question**:

Given an integer array `nums` sorted in non-decreasing order, remove all duplicates in-place so that each unique element appears only once. Return the number of unique elements in the array. The remaining elements, as well as the size of the array, do not matter in terms of correctness.

### **Intuition**:

Since the array is already sorted in non-decreasing order, duplicates must be adjacent. Therefore, we can use a two-pointer technique:

1. One pointer (`i`) will traverse the array from left to right to check for unique elements.
2. The second pointer (`k`) will keep track of where to place the next unique element.
3. If an element is different from the previous one, it is unique and should be placed at the position pointed to by `k`.

This approach allows us to modify the array in-place without using extra space.

### **Solution (All Approaches)**:

- **Approach 1: Two-Pointer Technique (Optimal)**
    
    - The first pointer will iterate over the array to find unique elements.
    - The second pointer will track the position to place the next unique element.
    - Time complexity will be O(n)O(n), where nn is the length of the array, and space complexity will be O(1)O(1) since the solution is in-place.
- **Approach 2: Using a Set (Extra Space)**
    
    - We could use a set to keep track of the unique elements and store them in an array. This would require O(n)O(n) space but is unnecessary as the array is sorted.

### **Implementation**:

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0; // Handle empty array
        
        int k = 1; // Start with the second element as the first element is always unique
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] != nums[i - 1]) {
                nums[k] = nums[i];  // Place the unique element at the kth position
                k++;  // Move the kth pointer
            }
        }
        return k;  // Return the number of unique elements
    }
};
```

### **Edge Cases**:

- **Empty Array**: If the array is empty, the return value should be 0, and the array remains unchanged.
- **All Elements Identical**: If all elements are the same, the result should be 1, as only one unique element remains in the array.
- **Array with One Element**: If there is only one element, it is inherently unique, so the result should be 1.
- **Multiple Duplicates**: The algorithm should correctly place the unique elements in the array while removing duplicates.

### **Time Complexity and Space Complexity**:

- **Time Complexity**:
    - O(n), where nn is the length of the array. We iterate through the array once and perform constant time operations for each element.
- **Space Complexity**:
    - O(1), since we are modifying the array in-place and using only a few extra variables (`i` and `k`).

### **Key Takeaways from this Problem**:

- **Two-Pointer Technique**: This problem emphasizes using two pointers to perform operations in-place, avoiding unnecessary space usage.
- **Sorted Arrays**: Leveraging the fact that the array is sorted allows us to efficiently identify duplicates and remove them without additional comparisons.
- **In-Place Modifications**: Being able to modify the array without using extra space is a crucial concept in optimizing for both time and space.

### **Mistakes and Challenges from this Problem**:

- **Handling Empty Arrays**: It’s important to handle edge cases like an empty array where the return value should be 0.
- **Incorrectly Counting Elements**: Mismanaging the index `k` or not correctly shifting the unique elements in place could lead to incorrect results.

### **Real-World Application of this Problem**:

- **Data Deduplication**: In many systems, we might need to deduplicate sorted data, such as removing duplicate records from a database.
- **Unique Element Extraction**: Similar operations occur in applications where we want to extract unique identifiers, such as user IDs, product IDs, or transaction IDs from sorted logs or datasets.

### **Problem Category Type**:

- **Category**: Arrays
- **Subcategory**: Two-Pointer Technique, In-place Modification