### **Question**

Given an array `nums` of size nn, return the majority element. The majority element is the element that appears **more than** ⌊n/2⌋\lfloor n / 2 \rfloor times. You may assume that the majority element always exists in the array.

---

### **Intuition**

The problem involves finding an element that appears more than half the time in the array.  
Key observations:

1. If an element is the majority, it will outnumber all other elements combined.
2. This allows efficient identification through counting or clever algorithms like the **Boyer-Moore Voting Algorithm**.

---

### **Solution (All Approaches)**

#### **Approach 1: Hash Map (Counting Frequency)**

- Use a hash map to count occurrences of each element.
- Identify the element with frequency > ⌊n/2⌋\lfloor n / 2 \rfloor.

**Steps**:

1. Traverse the array, storing counts of each element in a hash map.
2. Return the element with count > n/2n / 2.

**Time Complexity:** O(n) (one pass to count, one pass to find the majority).  
**Space Complexity:** O(n) (for the hash map).

---

#### **Approach 2: Sorting**

- Sort the array, and the majority element will always be at index $⌊n/2⌋$

**Steps**:

1. Sort the array.
2. Return the element at $nums[⌊n/2⌋]$

**Time Complexity:** O(nlog⁡n)(due to sorting).  
**Space Complexity:** O(1) if sorting in-place.

---

#### **Approach 3: Boyer-Moore Voting Algorithm (Optimal)**

- Utilize the observation that the majority element will always have a net count > 0 if paired with any non-majority element.

**Steps**:

1. Initialize a `count` and a `candidate`.
2. Traverse the array:
    - If `count == 0`, set the current element as the candidate.
    - Increment `count` if the current element matches the candidate, else decrement `count`.
3. The candidate at the end of traversal is the majority element.

**Time Complexity:** O(n)O(n).  
**Space Complexity:** O(1)O(1).

---

### **Implementation**

#### **Boyer-Moore Algorithm**

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = 0, count = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
};
```

---

### **Edge Cases**

1. Single element array: `[1]` → Majority is `1`.
2. All elements the same: `[2, 2, 2, 2]` → Majority is `2`.
3. Random array with clear majority: `[3, 3, 4, 3, 5, 3, 3]` → Majority is `3`.

---

### **Time Complexity and Space Complexity**

| **Approach**       | **Time Complexity** | **Space Complexity** |
| ------------------ | ------------------- | -------------------- |
| Hash Map           | O(n)                | O(n)                 |
| Sorting            | O(nlog⁡n)           | O(1)                 |
| Boyer-Moore Voting | O(n)                | O(1)                 |

---

### **Key Takeaways from this Problem**

1. The Boyer-Moore Algorithm is a powerful way to solve majority-related problems in O(n) time and O(1) space.
2. Sorting can simplify the problem but may not be optimal.
3. Hash maps are versatile but require extra space.

---

### **Mistakes and Challenges**

1. Forgetting to validate that the candidate is indeed the majority (not needed here due to problem constraints but essential in variations).
2. Misunderstanding the $⌊n/2⌋$ threshold, which is critical for correctness.

---

### **Real-World Application of this Problem**

1. Finding the most common preference in surveys or polls.
2. Detecting the dominant signal in noisy data.

---

### **Problem Category Type**

Arrays, Greedy, Hashing.
