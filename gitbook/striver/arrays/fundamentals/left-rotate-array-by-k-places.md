

### **Question**:

Given an array `nums` and an integer `K`, left rotate the array by `K` places. This means each element of the array should shift to the left by `K` positions, and the first `K` elements should move to the end of the array. If `K` is larger than the size of the array, perform the rotation for `K % nums.size()` places.

### **Intuition**:

Left rotation by `K` places means that the first `K` elements of the array should be moved to the end, and the remaining elements should shift to the left by `K` positions. We can approach this problem by using a combination of array slicing and reversing:

- Reverse the first `K` elements.
- Reverse the remaining elements (from `K` to the end).
- Reverse the entire array to get the desired order.

Alternatively, a simpler approach is to treat the array as two parts and rearrange them using slicing.

### **Solution (All Approaches)**:

- **Approach 1: Using Extra Space (Slicing)**
    
    - First, take the first `K` elements and store them in a temporary array.
    - Then, shift the remaining elements to the left by `K` positions.
    - Finally, append the first `K` elements from the temporary array to the end.
- **Approach 2: Optimized (Reverse Approach)**  
    This approach involves using the array itself and performing in-place rotations using reversing:
    
    - Reverse the first `K` elements.
    - Reverse the remaining elements (from `K` to end).
    - Reverse the entire array to achieve the desired result.
- **Approach 3: Using a Queue or Linked List**  
    For larger datasets, another way could be to use a queue or linked list, where you enqueue the elements and perform the necessary rotations. This approach, however, may not be optimal in terms of time and space complexity.
    

### **Implementation**:

```cpp
class Solution {
public:
    void rotateArrayByK(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0) return;  // Handle empty array
        
        k = k % n;  // In case K is larger than the array size
        
        // Step 1: Reverse the first K elements
        reverse(nums.begin(), nums.begin() + k);
        
        // Step 2: Reverse the remaining elements
        reverse(nums.begin() + k, nums.end());
        
        // Step 3: Reverse the entire array to get the final result
        reverse(nums.begin(), nums.end());
    }
};
```


```cpp

class Solution {
    // Helper function to reverse a portion of the array
    void reverse(vector<int>& nums, int start, int end) {
        while (start < end) {  // Reverse elements until start is less than end
            swap(nums[start], nums[end]);
            start++;
            end--;
        }
    }

public:
    void rotateArray(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0) return;  // Early return if the array is empty

        k = k % n;  // Handle cases where k is greater than the array size

        // Reverse the first k elements
        reverse(nums, 0, k - 1);
        // Reverse the remaining elements
        reverse(nums, k, n - 1);
        // Reverse the entire array to get the final result
        reverse(nums, 0, n - 1);
    }
};

```
### **Edge Cases**:

- **Empty Array**: If the array is empty, no rotation should occur.
- **K Greater Than Array Size**: If `K` is greater than the size of the array, rotating by `K % n` ensures no unnecessary full rotations are performed.
- **Array with a Single Element**: If the array has only one element, any rotation will result in the same array.
- **All Identical Elements**: If all elements are the same, rotating the array will result in the same array.

### **Time Complexity and Space Complexity**:

- **Time Complexity**:
    - O(n), where nn is the number of elements in the array. Reversing the array and its parts takes linear time.
- **Space Complexity**:
    - O(1), since we are performing in-place operations without using any extra space, except for a few temporary variables for the reversal process.

### **Key Takeaways from this Problem**:

- **Array Manipulation**: This problem emphasizes efficient in-place manipulation of an array without using extra space.
- **Modular Arithmetic**: Using `K % n` ensures that we handle cases where `K` is larger than the array size efficiently.
- **Efficient Rotation**: The reverse-based approach is efficient and avoids the need for extra space or repeated iterations.

### **Mistakes and Challenges from this Problem**:

- **Handling Large K Values**: A common mistake is forgetting to reduce `K` by taking `K % n`, leading to unnecessary full rotations.
- **Edge Case Handling**: Misunderstanding the behavior when the array is empty or when `K` is zero.

### **Real-World Application of this Problem**:

- **Circular Buffers**: In data structures like circular buffers, elements are rotated or wrapped around, and this problem is a direct representation of such operations.
- **Scheduler or Job Queueing**: In systems where tasks or jobs are scheduled in a circular manner, left rotating the queue can simulate such a process.
- **Time Series Data Shifting**: In some time-series data models, we might need to shift data points left or right as part of a calculation or to prepare data for further analysis.

### **Problem Category Type**:

- **Category**: Arrays
- **Subcategory**: Array Manipulation