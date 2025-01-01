# **Maximum Sum Subarray (Kadane's Algorithm)**

## **Question**

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.  
The subarray must be contiguous within the original array.

---

## **Intuition**

The goal is to find a subarray with the maximum sum efficiently. Generating all subarrays using brute force is computationally expensive. Instead, **Kadane's Algorithm** solves this in **linear time** by maintaining two variables:

1. **Current Sum (`sum`)**: The maximum sum of a subarray ending at the current index.
2. **Global Maximum (`best`)**: The maximum sum across all subarrays encountered so far.

Key observations:

- At each element, you either:
    - Start a new subarray from the current element.
    - Continue the previous subarray by adding the current element.
- This decision is made using `sum = max(nums[i], sum + nums[i])`.
- Update the global maximum (`best`) after processing each element.

---

## **Solution (All Approaches)**

### **1. Brute Force**

1. Generate all possible subarrays using nested loops.
2. Compute the sum of each subarray and track the maximum sum.

- **Time Complexity**: O(n2)O(n^2).
- **Space Complexity**: O(1)O(1).

### **2. Kadane's Algorithm**

1. Traverse the array while maintaining:
    - `sum`: Maximum sum ending at the current index.
    - `best`: Global maximum sum seen so far.
2. Update `sum` at each step: `sum = max(nums[i], sum + nums[i])`.
3. Update `best` as the maximum of `best` and `sum`.
4. Return `best` as the result.

- **Time Complexity**: O(n)O(n).
- **Space Complexity**: O(1)O(1).

---

## **Implementation**

### Alternative Implementation

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int best = INT_MIN, sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            // Start a new subarray or continue the previous one
            sum = max(nums[i], sum + nums[i]);  
            // Update the global maximum
            best = max(best, sum);
        }
        return best;
    }
};
```

### Original Kadane’s Algorithm

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int currentSum = 0;
        int maxSum = INT_MIN; // Initialize to the smallest integer
        
        for (int num : nums) {
            currentSum += num; // Add the current element to the current subarray sum
            maxSum = max(maxSum, currentSum); // Update the global maximum sum
            
            // Reset currentSum if it becomes negative
            if (currentSum < 0) {
                currentSum = 0;
            }
        }
        
        return maxSum;
    }
};
```

---

## **Edge Cases**

1. **All Negative Numbers**: For arrays like `[-3, -2, -5]`, the maximum subarray is the least negative number.
2. **Single Element Array**: The result is the single element, e.g., `[5]` → `5`.
3. **Large Arrays**: Efficiently handles arrays with millions of elements.
4. **All Positive Numbers**: The sum of the entire array is the maximum subarray sum.

---

## **Time Complexity**

- **Kadane’s Algorithm**: O(n)O(n), where nn is the size of the array.

## **Space Complexity**

- O(1)O(1), as the algorithm uses constant space.

---

## **Key Takeaways from this Problem**

1. **Kadane's Algorithm** is optimal for solving maximum sum subarray problems in linear time.
2. Resetting `sum` ensures subarrays with negative sums don't affect the global maximum.
3. Understanding the recurrence relation `sum = max(nums[i], sum + nums[i])` simplifies the implementation.
4. Initialization of `best` to `INT_MIN` ensures correctness for negative-only arrays.

---

## **Mistakes and Challenges from this Problem**

1. **Resetting the sum**: Forgetting to reset `sum` properly can lead to incorrect results.
2. **Initialization of `best`**: Setting `best` to 0 instead of `INT_MIN` may fail for arrays with all negative numbers.
3. Overcomplicating the problem by trying to maintain indices for the subarray instead of focusing on sums.

---

## **Real-World Application of this Problem**

1. **Stock Market Analysis**: Finding the maximum profit for a given period.
2. **Peak Traffic Analysis**: Determining the maximum traffic load during a continuous timeframe.
3. **Productivity Tracking**: Identifying the most productive streaks in data logs.

---

## **Problem Category Type**

- **Greedy Algorithms**
- **Dynamic Programming (1D)**


```cpp

class Solution {
public:
    vector<int> maxSubArray(vector<int>& nums) {
        int best = INT_MIN, sum = 0;
        int start = 0, end = 0, tempStart = 0; // Variables to track indices of the subarray

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > sum + nums[i]) {
                sum = nums[i];
                tempStart = i; // Start a new subarray
            } else {
                sum += nums[i]; // Extend the current subarray
            }

            if (sum > best) {
                best = sum;
                start = tempStart; // Update start index
                end = i;           // Update end index
            }
        }

        // Extract the subarray
        vector<int> result(nums.begin() + start, nums.begin() + end + 1);
        return result;
    }
};


```


### Explanation:

1. **Track Start and End Indices**:
    
    - Use `tempStart` to track the start of a new potential subarray when the current element is greater than `sum + nums[i]`.
    - Update `start` and `end` when a new best sum is found.
2. **Extract Subarray**:
    
    - Once the loop completes, use `start` and `end` to extract the maximum subarray from `nums`.


### **The Core Idea**

Kadane's Algorithm makes two key observations:

1. At each index iii, there are two possibilities:
    
    - The maximum subarray sum ending at index iii includes the element $nums[i]$ _only_.
    - The maximum subarray sum ending at index iii extends a subarray ending at $i−1$.
2. The maximum subarray sum ending at iii is given by:
    
    $$\text{current\_sum} = \max(nums[i], \text{current\_sum} + nums[i])
    $$
    This ensures that we either:
    
    - Start a new subarray at iii (when $nums[i]$ is greater than the sum so far), or
    - Extend the previous subarray by including $nums[i]$.