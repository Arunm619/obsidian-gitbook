### **Question**:

Given an array of integers and an integer `K`, the task is to count the number of subarrays whose sum is exactly `K`.

### **Intuition**:

The problem can be solved efficiently using the **prefix sum technique** combined with a **hashmap**. The idea is similar to the "longest subarray with sum K" problem, but instead of finding the longest subarray, we need to count how many subarrays sum up to `K`.

We maintain a running cumulative sum and track how many times each cumulative sum has been seen in a hashmap. The key observation is that if the cumulative sum at some index minus `K` has been encountered before, there exists a subarray with sum `K` ending at the current index.

### **Solution (all approaches)**:

#### 1. **Optimal approach using HashMap**:

- Maintain a hashmap that stores the frequency of each cumulative sum encountered so far.
- For each element in the array, update the cumulative sum.
- If `cumulativeSum - K` exists in the hashmap, it means there is a subarray ending at the current index with sum `K`. Increment the count by the frequency of `cumulativeSum - K`.
- Additionally, store the current cumulative sum in the hashmap to keep track of its occurrences.

#### 2. **Naive approach** (less efficient):

- A brute-force approach would be to check all possible subarrays and calculate their sum. This approach has a time complexity of O(n²) and is inefficient for large arrays.

Time Complexity: O(n²) Space Complexity: O(1)

### **Implementation**:

```cpp
#include <unordered_map>
#include <vector>
#include <iostream>
using namespace std;

class Solution {
public:
    int countSubarraysWithSumK(vector<int>& nums, int K) {
        unordered_map<int, int> prefixSumMap;
        int cumulativeSum = 0;
        int count = 0;
        
        // Initialize the map with cumulative sum 0 to handle cases where subarray starts from index 0
        // or use a simple if check for sum k within the loop and increment by 1.
        prefixSumMap[0] = 1;
        
        // Iterate through the array
        for (int num : nums) {
            cumulativeSum += num;
            
            // If cumulativeSum - K exists in the map, it means there are subarrays with sum K
            if (prefixSumMap.find(cumulativeSum - K) != prefixSumMap.end()) {
                count += prefixSumMap[cumulativeSum - K];
            }
            
            // Store the current cumulative sum in the map
            prefixSumMap[cumulativeSum]++;
        }
        
        return count;
    }
};
```

### **Edge Cases**:

1. The array is empty (no subarray exists).
2. There are no subarrays with sum `K`.
3. There are multiple subarrays with sum `K`.
4. The array contains negative numbers, and subarrays with negative values may also sum to `K`.

### **Time Complexity and Space Complexity**:

- **Time Complexity**: $O(n)$, where `n` is the length of the array. We iterate through the array once, and each operation with the hashmap (insert, find) takes constant time on average.
- **Space Complexity**: $O(n)$, as we store at most `n` different cumulative sums in the hashmap.

### **Key Takeaways from this Problem**:

- Hashmaps can be used effectively to store cumulative sums and efficiently count subarrays that meet a particular sum condition.
- This problem demonstrates how prefix sums and hashmaps can be combined to transform a seemingly complex problem into a more manageable one.

### **Mistakes and Challenges from this Problem**:

- A common mistake is not initializing the hashmap with `prefixSumMap[0] = 1`, which is necessary to handle cases where a subarray starting at index 0 has the sum `K`.
- Some may overlook handling negative numbers and ensure the cumulative sum calculation handles all cases, including those that involve negative values.

### **Real World Application of this Problem**:

- This problem can be applied in scenarios where you need to analyze sequences of events or transactions that sum up to a specific target, such as finding contiguous periods of a particular value in time series data (e.g., stock prices, temperature fluctuations).
- It is useful in various algorithmic challenges and interview scenarios where efficient counting is required.

### **Problem Category Type**:

- Arrays
- HashMap (or Hashing)
- Prefix Sum