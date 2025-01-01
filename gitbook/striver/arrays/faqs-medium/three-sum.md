
### **Question**

Given an integer array `nums`, return all unique triplets [nums[i],nums[j],nums[k]][nums[i], nums[j], nums[k]] such that:

- $$ i \neq j, i \neq k, and j \neq k.
	 $$
- $$
- nums[i] + nums[j] + nums[k] = 0.
- $$

The solution set must not contain duplicate triplets, but an element can be part of multiple triplets.

---

### **Example**

**Input:**  
`nums = [2, -2, 0, 3, -3, 5]`

**Output:**  
`[[-2, 0, 2], [-3, -2, 5], [-3, 0, 3]]`

**Explanation:**

- nums[1]+nums[2]+nums[0]=−2+0+2=0nums[1] + nums[2] + nums[0] = -2 + 0 + 2 = 0.
- nums[4]+nums[1]+nums[5]=−3+−2+5=0nums[4] + nums[1] + nums[5] = -3 + -2 + 5 = 0.
- nums[4]+nums[2]+nums[3]=−3+0+3=0nums[4] + nums[2] + nums[3] = -3 + 0 + 3 = 0.

---

### **Intuition**

The goal is to find all unique triplets that sum to zero.

- A **brute force approach** would involve iterating over all triplets and checking the sum, but this is inefficient.
- Sorting the array and using a **two-pointer technique** allows us to efficiently find triplets while avoiding duplicates.

---

### **Solution (All Approaches)**

#### **Approach 1: Brute Force (Inefficient)**

- Generate all possible triplets and check if the sum is zero.

**Steps:**

1. Use three nested loops to iterate over all unique triplets.
2. Check if the sum of the triplet equals zero.
3. Add the triplet to the result list, ensuring no duplicates.

**Time Complexity:**

- O(n3)O(n^3), where nn is the size of the array.

**Space Complexity:**

- O(k)O(k), where kk is the number of unique triplets.

---

#### **Approach 2: Sorting + Two-Pointer Technique (Optimal)**

- Sort the array, then for each element nums[i]nums[i], use two pointers to find pairs that sum to −nums[i]-nums[i].

**Steps:**

1. **Sort the array**: Sorting helps avoid duplicates easily.
2. Fix the first element nums[i]nums[i] and find pairs nums[j]nums[j] and nums[k]nums[k] such that nums[i]+nums[j]+nums[k]=0nums[i] + nums[j] + nums[k] = 0.
    - Use two pointers:
        - Left pointer at j=i+1j = i+1.
        - Right pointer at k=nums.size()−1k = \text{nums.size()} - 1.
3. If the sum is less than zero, increment the left pointer.
4. If the sum is greater than zero, decrement the right pointer.
5. Skip duplicate values for nums[i]nums[i], nums[j]nums[j], and nums[k]nums[k].

**Time Complexity:**

- O(n2)O(n^2): The outer loop runs O(n)O(n) times, and the two-pointer search runs O(n)O(n) in the worst case.

**Space Complexity:**

- O(k)O(k): For storing the unique triplets.

---

### **Implementation**

#### **Approach 1: Brute Force**

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        set<vector<int>> uniqueTriplets;
        for (int i = 0; i < nums.size(); ++i) {
            for (int j = i + 1; j < nums.size(); ++j) {
                for (int k = j + 1; k < nums.size(); ++k) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        vector<int> triplet = {nums[i], nums[j], nums[k]};
                        sort(triplet.begin(), triplet.end());
                        uniqueTriplets.insert(triplet);
                    }
                }
            }
        }
        return vector<vector<int>>(uniqueTriplets.begin(), uniqueTriplets.end());
    }
};
```

---

#### **Approach 2: Sorting + Two-Pointer Technique**

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 2; ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates for nums[i]
            int target = -nums[i];
            int left = i + 1, right = nums.size() - 1;
            while (left < right) {
                int sum = nums[left] + nums[right];
                if (sum == target) {
                    result.push_back({nums[i], nums[left], nums[right]});
                    while (left < right && nums[left] == nums[left + 1]) ++left; // Skip duplicates for nums[left]
                    while (left < right && nums[right] == nums[right - 1]) --right; // Skip duplicates for nums[right]
                    ++left;
                    --right;
                } else if (sum < target) {
                    ++left;
                } else {
                    --right;
                }
            }
        }
        return result;
    }
};
```

---

### **Edge Cases**

1. **Empty Array**: Return an empty list.
2. **Array with Less Than 3 Elements**: Return an empty list.
3. **No Triplets Exist**: Return an empty list.
4. **All Zeros**: Ensure duplicates are handled (e.g., `[0, 0, 0, 0]` should return `[[0, 0, 0]]`).

---

### **Time Complexity and Space Complexity**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Brute Force|O(n3)O(n^3)|O(k)O(k)|
|Two-Pointer (Optimal)|O(n2)O(n^2)|O(k)O(k)|

---

### **Key Takeaways from this Problem**

1. Sorting the array simplifies duplicate handling and enables efficient pair searches.
2. Two-pointer techniques are extremely effective for pair or triplet-sum problems.

---

### **Mistakes and Challenges from this Problem**

1. Forgetting to skip duplicates after finding a triplet.
2. Mismanaging pointers or target values during the two-pointer traversal.

---

### **Real-World Application of this Problem**

1. **Finance**: Finding sets of transactions with a specific net sum.
2. **Gaming**: Identifying groups of items with specific attribute combinations.
3. **Data Analysis**: Finding groups of data points meeting a specific condition.

---

### **Problem Category Type**

- **Two Pointers**
- **Sorting**
- **Arrays**

Let me know if you have questions or need further clarification!



Learnings
Dont forget to consider the two pointer approach when you calculate the sum 
there are three conditions sum is reached or smaller or larger

Also instead of simply moving pointers by one. Move it to a while loop and keep repeating until the condition is met.

Also simply skip the `first element` by checking for previous element `nums[i] == nums[i-1]` whenever i becomes atleast 1.



