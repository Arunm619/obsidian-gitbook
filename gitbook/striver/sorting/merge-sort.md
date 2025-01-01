

### Merge Sort: A Divide and Conquer Algorithm

Merge Sort is a popular **divide and conquer** sorting algorithm with a time complexity of $O(n \log n)$. Here's a breakdown:

---

### **How It Works**

1. **Divide**: Split the array into two halves until each subarray contains one element (base case of recursion).
2. **Conquer**: Recursively sort each half.
3. **Combine**: Merge the sorted halves to produce a single sorted array.

---

### **Algorithm Steps**

1. **Split the Array**:
    
    - Divide the array into two halves using the midpoint.
    - Recursively call merge sort on each half.
2. **Merge the Arrays**:
    
    - Compare elements from the two halves.
    - Place the smaller element into the resulting array.
    - Repeat until all elements are merged.

---

### **Time Complexity**

- **Best Case**: O(nlog⁡n) (even when the array is already sorted, merge step takes linear time).
- **Worst Case**: O(nlog⁡n) (splitting and merging dominate the cost).
- **Average Case**: O(nlog⁡n).

**Space Complexity**: O(n) (additional space is required for the temporary arrays during merging).

```cpp

class Solution {
public:
    // Merges two subarrays of 'nums'
    // First subarray is nums[left..mid]
    // Second subarray is nums[mid+1..right]
    void merge(vector<int>& nums, int left, int mid, int right) {
        int leftSubarraySize = mid - left + 1;
        int rightSubarraySize = right - mid;

        // Temporary arrays to hold the two halves
        vector<int> leftSubarray(leftSubarraySize), rightSubarray(rightSubarraySize);

        // Copy data into temporary arrays
        for (int i = 0; i < leftSubarraySize; i++) {
            leftSubarray[i] = nums[left + i];
        }
        for (int i = 0; i < rightSubarraySize; i++) {
            rightSubarray[i] = nums[mid + 1 + i];
        }

        // Merging the temporary arrays back into 'nums'
        int leftIndex = 0, rightIndex = 0, mergedIndex = left;
        while (leftIndex < leftSubarraySize && rightIndex < rightSubarraySize) {
            if (leftSubarray[leftIndex] <= rightSubarray[rightIndex]) {
                nums[mergedIndex++] = leftSubarray[leftIndex++];
            } else {
                nums[mergedIndex++] = rightSubarray[rightIndex++];
            }
        }

        // Copy remaining elements from left subarray (if any)
        while (leftIndex < leftSubarraySize) {
            nums[mergedIndex++] = leftSubarray[leftIndex++];
        }

        // Copy remaining elements from right subarray (if any)
        while (rightIndex < rightSubarraySize) {
            nums[mergedIndex++] = rightSubarray[rightIndex++];
        }
    }

    // Sorts the array using merge sort
    void mergeSort(vector<int>& nums, int left, int right) {
        if (left < right) {
            // Find the middle point to divide the array
            int mid = left + (right - left) / 2;

            // Recursively sort the two halves
            mergeSort(nums, left, mid);
            mergeSort(nums, mid + 1, right);

            // Merge the two sorted halves
            merge(nums, left, mid, right);
        }
    }

    // Main function to sort the array
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }
};

```

### **Time Complexity**

1. **Divide Step**:
   - In each recursive call, the array is split into two halves, which takes constant time \( O(1) \).
   - The depth of the recursion is \( log(n) \) because the array is divided in half at each level of recursion (e.g., dividing 8 elements takes 3 levels of recursion: 8 -> 4 -> 2 -> 1).
   - Thus, the divide step contributes \( O(log n) \) levels.

2. **Merge Step**:
   - In each level of recursion, the algorithm merges two sorted halves. Merging two sorted arrays of size \( n \) requires \( O(n) \) time.
   - At each level of recursion, the algorithm merges subarrays of size \( 1, 2, 4, 8, \dots \), summing to \( O(n) \) at each level.

3. **Total Time Complexity**:
   - The total time complexity is the time taken for the divide step \( O(\log n) \) multiplied by the time taken for the merge step \( O(n) \).
   - Thus, the total time complexity is:

   \[
   O(n \log n)
   \]

---

### **Space Complexity**

1. **Auxiliary Space**:
   - Merge Sort requires extra space for the temporary arrays (i.e., `leftSubarray` and `rightSubarray`) that hold the two halves during the merge step.
   - For each merge operation, you need additional space proportional to the size of the array being merged. In the worst case, this space is \( O(n) \).

2. **Recursive Call Stack**:
   - The depth of the recursion is \( O(\log n) \), as each recursive call divides the array into two halves.
   - However, each recursive call does not require additional space beyond the call stack, since the merging happens in-place after the recursion unwinds.

3. **Total Space Complexity**:
   - The primary contributor to space complexity is the temporary arrays used for merging, which require \( O(n) \) space.
   - Therefore, the total space complexity is:   \[O(n)\]

---

### **Summary**
- **Time Complexity**: $( O(n log n) )$
- **Space Complexity**: $O(n)$

This makes Merge Sort very efficient in terms of time, though it does require extra space for the temporary arrays during the merge process.
