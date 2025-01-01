
### **Question**:

Given an array of integers `nums`, return the second-largest element in the array. If the second-largest element does not exist, return `-1`.

### **Intuition**:

To find the second-largest element, we can iterate through the array while keeping track of both the largest and the second-largest elements. We update the largest and second-largest as we encounter larger values. If we find a number larger than the largest, we update the second-largest to be the current largest and then update the largest. If no second-largest element exists (e.g., if the array has fewer than two distinct elements), we return `-1`.

### **Solution (All Approaches)**:

- **Approach 1: Two-Pointer Approach**  
    This approach involves iterating through the array once and maintaining two variables, `largest` and `secondLargest`. As we iterate:
    - If the current number is greater than `largest`, we update `secondLargest` to be `largest`, and then set `largest` to the current number.
    - If the current number is not greater than `largest` but is greater than `secondLargest`, we update `secondLargest`.
- **Approach 2: Sorting**  
    We can also sort the array in descending order and simply pick the second element. However, this is less efficient because sorting the array takes O(nlog⁡n)O(n \log n) time, whereas the two-pointer approach works in O(n)O(n) time.

### **Implementation**:

```cpp
class Solution {
public:
    int secondLargest(vector<int>& nums) {
        int largest = INT_MIN, secondLargest = INT_MIN;

        // Iterate through the array
        for (int num : nums) {
            if (num > largest) {
                secondLargest = largest;  // Update second largest to be the old largest
                largest = num;  // Update largest to the current number
            } else if (num > secondLargest && num < largest) {
                secondLargest = num;  // Update second largest
            }
        }

        // If no second largest element exists
        return (secondLargest == INT_MIN) ? -1 : secondLargest;
    }
};
```

### **Edge Cases**:

- **Array with fewer than two elements**: If the array has fewer than two elements, there's no second-largest element, so we should return `-1`.
- **All elements are the same**: If all elements are identical, there's no second-largest element, so return `-1`.
- **Array with only one distinct value**: If the array has one unique value repeated, we should return `-1`.
- **Array with two distinct elements**: If the array has two distinct elements, the second-largest is the smaller of the two.

### **Time Complexity and Space Complexity**:

- **Time Complexity**:
    - O(n), where n is the number of elements in the array. We only need one pass through the array to find both the largest and second-largest elements.
- **Space Complexity**:
    - O(1), since we only use a few extra variables to store the largest and second-largest values, and we don't use any additional data structures.

### **Key Takeaways from this Problem**:

- **Efficiency**: The two-pointer approach provides an optimal solution with O(n)O(n) time complexity, which is faster than the sorting-based approach.
- **Edge Case Handling**: This problem highlights the importance of handling arrays with fewer than two elements or arrays where all values are the same.
- **Comparison Logic**: It's important to carefully update the second-largest element without overwriting it incorrectly.

### **Mistakes and Challenges from this Problem**:

- **Incorrectly Updating Second-Largest**: One challenge might be failing to correctly track the second-largest element, especially when the largest and second-largest elements are very close in value or repeated.
- **Handling Edge Cases**: Misunderstanding the condition when there are fewer than two distinct elements could lead to incorrect results.

### **Real-World Application of this Problem**:

- **Rankings and Scores**: In competitions or rankings, you might need to find the second-highest score or rank. This is a common scenario in sports, gaming, or competitive exams.
- **Resource Allocation**: In scenarios where you need to allocate resources based on rankings, finding the second-highest value might be necessary.

### **Problem Category Type**:

- **Category**: Arrays
- **Subcategory**: Searching and Comparison