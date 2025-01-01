#### **Question**

Given an array of integers `nums`, rearrange its elements such that:

1. The elements at even indices (0, 2, 4, ...) are positive.
2. The elements at odd indices (1, 3, 5, ...) are negative.

Assume the input array contains an equal number of positive and negative numbers.  
Return the rearranged array while maintaining the relative order of positive and negative numbers.

---

#### **Intuition**

To rearrange the array:

1. Separate positive and negative numbers into two lists.
2. Alternate between picking elements from the positive and negative lists to fill the result array.
3. This approach guarantees maintaining the relative order of elements and adheres to the even-odd placement rule.

---

#### **Solution (Using Auxiliary Space)**

Separate the positive and negative elements into two arrays and interleave them into the result.

---

#### **Implementation**

```cpp
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        vector<int> positives, negatives, result(nums.size());
        for (int num : nums) {
            if (num > 0) {
                positives.push_back(num);
            } else {
                negatives.push_back(num);
            }
        }
        
        int posIndex = 0, negIndex = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (i % 2 == 0) {
                result[i] = positives[posIndex++];
            } else {
                result[i] = negatives[negIndex++];
            }
        }
        return result;
    }
};
```


Another solution with smart handling for storing items alternatively:

```cpp

vector<int> rearrangeArrayBySign(const vector<int>& nums) {
    vector<int> positives, negatives;
    
    // Separate the array into positives and negatives
    for (int num : nums) {
        if (num > 0) {
            positives.push_back(num);
        } else {
            negatives.push_back(num);
        }
    }
    
    vector<int> result;
    int n = positives.size();
    
    // Merge positives and negatives alternately
    for (int i = 0; i < n; i++) {
        result.push_back(positives[i]);
        result.push_back(negatives[i]);
    }
    
    return result;
}

```

---

#### **Edge Cases**

1. **Balanced Positive and Negative Numbers**
    
    - Input: `nums = [1, -1, 2, -2, 3, -3]`
    - Output: `[1, -1, 2, -2, 3, -3]`
2. **Large Values**
    
    - Input: `nums = [100000, -100000, 200000, -200000]`
    - Output: `[100000, -100000, 200000, -200000]`
3. **No Need for Rearrangement**
    
    - Input: `nums = [1, -1, 2, -2]`
    - Output: `[1, -1, 2, -2]`

---

#### **Time Complexity and Space Complexity**

- **Time Complexity**:
    
    - Separating positive and negative numbers takes **O(n)**.
    - Merging the two lists into the result takes **O(n)**.
    - Overall: **O(n)**.
- **Space Complexity**:
    
    - The `positives` and `negatives` arrays require **O(n)** space.
    - The result array also requires **O(n)** space.
    - Overall: **O(n)** auxiliary space.

---

#### **Key Takeaways from this Problem**

1. The problem highlights the importance of maintaining relative order while rearranging elements.
2. Separating and merging lists is a common two-pass strategy that simplifies complex problems.
3. Efficient use of indices ensures minimal auxiliary space in variations of the problem.

---

#### **Mistakes and Challenges from this Problem**

1. Misaligning indices between the positive and negative arrays when filling the result.
2. Not considering how to handle arrays with alternate positive and negative values directly.
3. The tough part in the question is to identify that you can't solve it in O(1) space.

---

#### **Real-World Application of this Problem**

1. **Load Balancing**: Assigning tasks alternately between two categories, such as CPU-intensive and I/O-intensive.
2. **Sensor Data**: Alternating between positive and negative readings for better visual representation in graphs.

---

#### **Problem Category Type**

- **Two-Pointer Technique**
- **Array Rearrangement**
- **Greedy Approach**