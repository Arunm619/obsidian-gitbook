
### **Question**

Find the maximum product subarray in a given integer array `nums`.

A subarray is a contiguous segment of the array. The goal is to find the contiguous subarray that produces the largest product.

---

### **Intuition**

This problem leverages dynamic programming-like ideas combined with greedy traversal:

1. Keep track of both the **maximum product so far** and the **minimum product so far** at each step since a negative number can turn the smallest product into the largest and vice versa.
2. Use two traversal techniques:
    - The conventional Kadane's algorithm for the product-based problem.
    - A prefix and suffix traversal to reset products when zeros are encountered.

The idea of prefix and suffix traversal handles cases where zeros divide the array into multiple independent subarrays.

---

### **Solution**

#### **First Approach (Kadane's Algorithm for Products)**

#### **Steps**:

1. Traverse the array while maintaining:
    - `maxProductSoFar`: The maximum product ending at the current index.
    - `minProductSoFar`: The minimum product ending at the current index.
    - `result`: The overall maximum product across all subarrays.
2. For each element:
    - Update `maxProductSoFar` and `minProductSoFar` considering:
        - Current element alone.
        - Product of the current element with the previous `maxProductSoFar`.
        - Product of the current element with the previous `minProductSoFar`.
3. Reset `maxProductSoFar` and `minProductSoFar` to the current element if the current element is `0` (acting as a reset point).
4. Track the global maximum in `result`.

---

#### **Code**:

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxProductSoFar = nums[0];
        int minProductSoFar = nums[0];
        int result = nums[0];

        for (int i = 1; i < nums.size(); i++) {
            int tempMax = maxProductSoFar;

            maxProductSoFar = max({nums[i], maxProductSoFar * nums[i], minProductSoFar * nums[i]});
            minProductSoFar = min({nums[i], tempMax * nums[i], minProductSoFar * nums[i]});
            
            result = max(result, maxProductSoFar);
        }

        return result;
    }
};
```

---

### **Second Approach (Prefix and Suffix Traversal)**

#### **Steps**:

1. Traverse the array from both ends simultaneously.
2. Maintain two products:
    - `prefixProduct`: Product of elements from left to right.
    - `suffixProduct`: Product of elements from right to left.
3. Reset the product to `1` whenever a `0` is encountered.
4. Keep track of the maximum product (`best`) throughout the traversal.

---

#### **Code**:

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int best = INT_MIN;
        int prefixProduct = 1;
        int suffixProduct = 1;
        int n = nums.size();

        for (int i = 0; i < n; i++) {
            int front = nums[i];
            int back = nums[n - 1 - i];

            prefixProduct *= front;
            suffixProduct *= back;

            best = max(best, max(prefixProduct, suffixProduct));

            // Reset products if zero is encountered
            if (prefixProduct == 0) prefixProduct = 1;
            if (suffixProduct == 0) suffixProduct = 1;
        }

        return best;
    }
};
```

---

### **Edge Cases**

1. **Single Element**:  
    Input: `[3]` → Output: `3`  
    Explanation: Only one element is present.
2. **All Negative Numbers**:  
    Input: `[-2, -3, -4]` → Output: `12`  
    Explanation: Multiplication of all negatives yields the highest product.
3. **Zeros in the Array**:  
    Input: `[0, -1, 2]` → Output: `2`  
    Explanation: Subarray `[2]` yields the maximum product.

---

### **Time Complexity and Space Complexity**

- **Time Complexity**:
    - First Approach: O(n)O(n) for a single traversal of the array.
    - Second Approach: O(n)O(n) for prefix and suffix traversal.
- **Space Complexity**:
    - Both approaches use O(1)O(1) space.

---

### **Key Takeaways from this Problem**

1. Kadane’s algorithm for the maximum product is a flexible extension of the max-sum problem with minor modifications for product cases.
2. The prefix and suffix traversal ensures zeros do not interfere with the calculations.

---

### **Mistakes and Challenges from this Problem**

1. Forgetting to reset the product when encountering zeros.
2. Ignoring the need to compute the suffix product alongside the prefix product in certain cases.

---

### **Real-World Application of this Problem**

- **Stock Price Analysis**: Finding maximum profit in a series of daily stock price fluctuations (adjusting for percentages).
- **Signal Processing**: Identifying peaks in oscillating data streams.

---

### **Problem Category Type**

- **Dynamic Programming**
- **Greedy Approach**
- **Arrays**


```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int prefixProduct = 1;
        int suffixProduct = 1;
        int maxi = INT_MIN;
        for (int i = 0, n = nums.size(); i < n; i++) {
            int front = nums[i];
            int back = nums[n - i - 1];
            prefixProduct *= front;
            suffixProduct *= back;
            maxi = max(max(prefixProduct, suffixProduct), maxi);
            if (prefixProduct == 0)
                prefixProduct = 1;
            if (suffixProduct == 0)
                suffixProduct = 1;
        }
        return maxi;
    }
};
```

_Key Explanation_ and proof for this algorithm:  
let n be the # of negative numbers.  
If n is even it obviously works.  
If n is odd, then the answer is some subarray without one of the negative numbers, i.e. to the right or to the left of that negative number.  
Take a look at any negative number in the array.  
Consider the subarrays to the left of this number and to the right of this number. they both have an even # of negative numbers,  
Then, when we take max products from the right and from the left, we encounter these arrays` product too.  
And this is true for every negative number in the array, so for sure we will encounter the answer.