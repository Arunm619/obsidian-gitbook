### **Question**

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

Assume:

- Each input would have **exactly one solution**, and you may not use the same element twice.
- You can return the answer in any order.

**Example:**  
Input:  
`nums = [2, 7, 11, 15], target = 9`

Output:  
`[0, 1]`

Explanation:  
`nums[0] + nums[1] = 2 + 7 = 9`

---

### **Intuition**

The goal is to find two numbers in the array that sum up to the target. The naive solution is to check all pairs of elements, but this can be optimized by storing the complements of the target in a data structure for faster lookup.

---

### **Solution (All Approaches)**

#### **Approach 1: Brute Force**

- Iterate through all pairs of indices to find two numbers that sum to the target.

**Steps**:

1. Use two nested loops to iterate over all possible pairs.
2. Check if the sum of the pair equals the target.

**Time Complexity**:

- O(n2)O(n^2) due to the nested loops.

**Space Complexity**:

- O(1)O(1), as no extra data structures are used.

---

#### **Approach 2: Hash Map (Optimal)**

- Use a hash map to store the complement of each number with respect to the target.

**Steps**:

1. Traverse the array while maintaining a hash map of seen numbers.
2. For each number, calculate its complement complement=target−nums[i]\text{complement} = \text{target} - \text{nums}[i].
3. Check if the complement exists in the hash map.
    - If yes, return the indices of the current number and its complement.
4. Otherwise, add the current number and its index to the hash map.

**Time Complexity**:

- O(n), as we traverse the array once and perform constant-time hash map operations.

**Space Complexity**:

- O(n), for the hash map storage.

---

### **Implementation**

#### **Approach 1: Brute Force**

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); ++i) {
            for (int j = i + 1; j < nums.size(); ++j) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {};
    }
};
```

---

#### **Approach 2: Hash Map**

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> seen;
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if (seen.count(complement)) {
                return {seen[complement], i};
            }
            seen[nums[i]] = i;
        }
        return {};
    }
};
```

---

### **Edge Cases**

1. **Empty Array**: Return an empty vector as no solution exists.
2. **Single Element Array**: Return an empty vector as no solution exists.
3. **Negative Numbers**: Ensure the solution works with negative integers.
    - Example: `nums = [-3, 4, 3, 90], target = 0`.
4. **Multiple Identical Numbers**: Ensure distinct indices are returned.

---

### **Time Complexity and Space Complexity**

| Approach           | Time Complexity | Space Complexity |
| ------------------ | --------------- | ---------------- |
| Brute Force        | O(n2)           | O(1)             |
| Hash Map (Optimal) | O(n)            | O(n)             |

---

### **Key Takeaways from this Problem**

1. Hash maps are useful for efficiently storing and looking up values in problems involving pairwise sums or complements.
2. The brute force approach is straightforward but inefficient; always look for opportunities to optimize with auxiliary data structures.

---

### **Mistakes and Challenges from this Problem**

1. Forgetting to handle the case where the same element cannot be used twice.
2. Mismanaging hash map operations (e.g., using the wrong key or overwriting existing values).

---

### **Real-World Application of this Problem**

1. **Finance**: Finding pairs of transactions that sum to a specific value.
2. **E-commerce**: Finding combinations of items within a budget.
3. **Gaming**: Identifying pairs of items with specific attribute combinations.

---

### **Problem Category Type**

- **Hashing**
- **Two Pointers**
- **Arrays**

