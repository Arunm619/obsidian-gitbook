
### **Question**

Given an integer array `nums`, find all elements that appear **more than** $\lfloor n / 3 \rfloor$ times.

You must solve the problem in **O(n)** time and **O(1)** space.

---

### **Intuition**

The problem extends the concept of finding a majority element (>n/2> n / 2) to finding all elements that occur more than n/3n / 3 times.

Key Observations:

1. There can be at most **two majority elements** with a frequency > n/3n / 3.
2. Use the **Boyer-Moore Voting Algorithm** generalized to track two candidates.

---

### **Solution (All Approaches)**

#### **Approach 1: Hash Map (Counting Frequency)**

Count occurrences of each element using a hash map.

**Steps**:

1. Traverse the array and count occurrences using a hash map.
2. Traverse the map to collect elements with frequency > n/3n / 3.

**Time Complexity:** O(n)O(n).  
**Space Complexity:** O(n)O(n) for the hash map.

---

#### **Approach 2: Boyer-Moore Voting Algorithm (Optimal)**

Track two candidates and their counts.

**Steps**:

1. First pass:
    - Maintain two candidates and their counts.
    - Adjust counts as follows:
        - If either candidate matches, increment its count.
        - If neither matches, decrement both counts.
        - If any count becomes zero, replace that candidate with the current element.
2. Second pass:
    - Verify the two candidates to ensure their frequencies exceed n/3n / 3.

**Time Complexity:** O(n)O(n).  
**Space Complexity:** O(1)O(1).

---

### **Implementation**

#### **Boyer-Moore Algorithm**

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int candidate1 = 0, candidate2 = 0, count1 = 0, count2 = 0;

        // First pass: Identify potential candidates
        for (int num : nums) {
            if (num == candidate1) {
                count1++;
            } else if (num == candidate2) {
                count2++;
            } else if (count1 == 0) {
                candidate1 = num;
                count1 = 1;
            } else if (count2 == 0) {
                candidate2 = num;
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }

        // Second pass: Verify the candidates
        count1 = count2 = 0;
        for (int num : nums) {
            if (num == candidate1) count1++;
            else if (num == candidate2) count2++;
        }

        vector<int> result;
        int n = nums.size();
        if (count1 > n / 3) result.push_back(candidate1);
        if (count2 > n / 3) result.push_back(candidate2);

        return result;
    }
};
```

---

### **Edge Cases**

1. **Empty array:** `[]` → Output: `[]`.
2. **Single element:** `[1]` → Output: `[1]`.
3. **No element > n/3n / 3:** `[1, 2, 3, 4]` → Output: `[]`.
4. **Multiple majorities:** `[1, 1, 2, 2, 3, 1, 2]` → Output: `[1, 2]`.

---

### **Time Complexity and Space Complexity**

|**Approach**|**Time Complexity**|**Space Complexity**|
|---|---|---|
|Hash Map|O(n)O(n)|O(n)O(n)|
|Boyer-Moore Voting|O(n)O(n)|O(1)O(1)|

---

### **Key Takeaways from this Problem**

1. The Boyer-Moore Voting Algorithm can be extended for majority elements beyond n/2n / 2.
2. Always verify candidates in a second pass for correctness.
3. Hash maps are simpler but do not meet space constraints.

---

### **Mistakes and Challenges**

1. Forgetting to verify candidates in the second pass.
2. Incorrectly updating both candidates when the current element matches neither.
3. Handling edge cases like arrays with fewer than 3 elements.
4. What happens when all the elements are 0? so choose arbitary candidates as 0 and 1. They shouldn't be same like 0 as they will contribute twice in input like $[0,0,0,]$ o/p will be like $[0,0]$

---

### **Real-World Application of this Problem**

1. Detecting dominant elements in large datasets where memory constraints exist.
2. Identifying trends or patterns in streaming data.

---

### **Problem Category Type**

Arrays, Greedy, Hashing.



