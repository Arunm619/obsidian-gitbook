
### **Question**:

Given an array of integers and an integer `K`, the task is to find the length of the longest contiguous subarray whose sum is exactly `K`.

### **Intuition**:

The naive approach would involve checking every possible subarray and calculating the sum, which would be inefficient. Instead, we can optimize the solution using a **hashmap** to store the cumulative sums encountered so far and their corresponding indices. This approach leverages the fact that if the difference between the current cumulative sum and `K` has been encountered before, it means there exists a subarray with sum `K`.

The basic idea is:

1. Traverse through the array and keep a running cumulative sum.
2. At each step, check if the cumulative sum minus `K` is present in the hashmap.
3. If it exists, it means a subarray with sum `K` has been found, and you can calculate the length of this subarray.
4. Keep track of the maximum length of such subarrays.

### **Solution (all approaches)**:

#### 1. **Optimal approach using HashMap**:

- Maintain a hashmap that stores the first occurrence of each cumulative sum.
- For each element, update the cumulative sum and check if the current cumulative sum minus `K` has been encountered before.
- If it has, update the maximum length of the subarray.

#### 2. **Naive approach** (less efficient):

- For each possible subarray, calculate the sum and compare it to `K`. This approach has a time complexity of O(n²) and is inefficient for large arrays.

Time Complexity: O(n²) Space Complexity: O(1)

### **Implementation**:

```cpp
#include <unordered_map>
#include <vector>
#include <iostream>
using namespace std;

class Solution {
public:
    int longestSubarrayWithSumK(vector<int>& nums, int K) {
        unordered_map<int, int> prefixSumMap;
        int cumulativeSum = 0;
        int maxLength = 0;
        
        // Iterate through the array
        for (int i = 0; i < nums.size(); ++i) {
            cumulativeSum += nums[i];
            
            // Check if cumulativeSum equals K
            if (cumulativeSum == K) {
                maxLength = i + 1;  // Subarray from index 0 to i
            }
            
            // If cumulativeSum - K exists in the map, update maxLength
            if (prefixSumMap.find(cumulativeSum - K) != prefixSumMap.end()) {
                maxLength = max(maxLength, i - prefixSumMap[cumulativeSum - K]);
            }
            
            // Store the first occurrence of cumulativeSum
            if (prefixSumMap.find(cumulativeSum) == prefixSumMap.end()) {
                prefixSumMap[cumulativeSum] = i;
            }
        }
        
        return maxLength;
    }
};
```

### **Edge Cases**:

1. The array is empty (no subarray exists).
2. There is no subarray with sum `K`.
3. The entire array is the subarray with sum `K`.
4. The array contains negative numbers, as the sum can still be valid with negative values.

### **Time Complexity and Space Complexity**:

- **Time Complexity**: O(n), where `n` is the length of the array. We iterate through the array once, and each operation with the hashmap (insert, find) takes constant time on average.
- **Space Complexity**: O(n), as we store at most `n` different cumulative sums in the hashmap.

### **Key Takeaways from this Problem**:

- The use of a hashmap (or hash table) helps optimize the search for a subarray with a given sum. The key insight is that the cumulative sum up to any point can be leveraged to detect subarrays efficiently.
- The running cumulative sum approach allows us to calculate the sum of any subarray in constant time by comparing cumulative sums.

### **Mistakes and Challenges from this Problem**:

- A common mistake is not handling negative numbers properly or failing to initialize the hashmap correctly.
- Some may also forget to handle the case when the entire subarray from the start has the sum `K` (i.e., `cumulativeSum == K`).

### **Real World Application of this Problem**:

- This problem is useful in financial applications where you need to find the longest period in a sequence of transactions or profits that adds up to a certain target value.
- It can also be applied in various data processing scenarios where subarrays with specific conditions are needed, such as signal processing or time-series analysis.

### **Problem Category Type**:

- Arrays
- HashMap (or Hashing)
- Prefix Sum