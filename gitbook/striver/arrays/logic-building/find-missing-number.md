### **Question**:

Given an integer array `nums` of size nn, containing distinct values in the range from 00 to nn (inclusive), return the only number missing from the array within this range.

---

### **Intuition**:

The problem can be approached in multiple ways:

1. Using the **sum formula**, calculate the expected sum and subtract the actual sum.
2. Using **XOR**, cancel out all existing numbers to find the missing one.
3. Using an **unordered set**, store all elements in the array and check which number from 0 to n is not in the set.

The unordered set is particularly useful when fast lookups are required. By storing all numbers in the set and iterating through 0 to n, we can identify the missing number efficiently.

---

### **Solution (All Approaches)**:

#### **Approach 1: Sum Formula**

- Compute the expected sum of 0 to n using the formula Sum=n(n+1)/2
- Subtract the actual sum of the array to find the missing number.
- **Time Complexity**: O(n)O(n)
- **Space Complexity**: O(1)O(1)

#### **Approach 2: XOR Method**

- XOR all numbers from 0 to n and XOR all numbers in the array.
- The result of these XORs will be the missing number.
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

#### **Approach 3: Unordered Set**

- Insert all elements of the array into an unordered set.
- Iterate through numbers 0 to n, checking for the first number not present in the set.
- **Time Complexity**: O(n) (insertion and lookup in unordered set are O(1) on average)
- **Space Complexity**: O(n) (to store the elements in the set)

---

### **Implementation**:

#### Approach 1: Sum Formula

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int expectedSum = (n * (n + 1)) / 2;
        int actualSum = 0;
        for (int num : nums) {
            actualSum += num;
        }
        return expectedSum - actualSum;
    }
};
```

#### Approach 2: XOR Method

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int xorAll = 0, xorArray = 0;
        
        for (int i = 0; i <= n; ++i) {
            xorAll ^= i;
        }
        
        for (int num : nums) {
            xorArray ^= num;
        }
        
        return xorAll ^ xorArray;
    }
};
```

#### Approach 3: Unordered Set

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        unordered_set<int> s;
        int n = nums.size();
        for (int num : nums) {
            s.insert(num); // Insert all elements into the set
        }

        for (int i = 0; i <= n; ++i) {
            if (s.find(i) == s.end()) {
                return i; // The missing number is not in the set
            }
        }
        return -1;
    }
};
```

---

### **Edge Cases**:

1. **Array with Single Element**: `nums = [0]` or `nums = [1]`, should return `1` or `0` respectively.
2. **Missing First Number**: `nums = [1, 2, 3]` should return `0`.
3. **Missing Last Number**: `nums = [0, 1, 2]` should return `3`.
4. **Empty Array**: Technically invalid but can return n=1n = 1.

---

### **Time Complexity and Space Complexity**:

| Approach          | Time Complexity | Space Complexity |
| ----------------- | --------------- | ---------------- |
| **Sum Formula**   | O(n)            | O(1)             |
| **XOR Method**    | O(n)            | O(1)             |
| **Unordered Set** | O(n)            | O(n)             |

---

### **Key Takeaways from this Problem**:

1. Utilize problem constraints (distinct values and known ranges) to simplify logic.
2. The sum formula and XOR methods are efficient for problems involving sequences.
3. Hashing techniques (e.g., unordered set) provide flexibility for dynamic checks but consume additional space.

---

### **Mistakes and Challenges from this Problem**:

1. Forgetting that the range is 00 to nn, leading to off-by-one errors.
2. Assuming array size equals nn and missing edge cases where n+1n + 1 is the expected range.
3. Overcomplicating with sorting or extra loops when simpler methods suffice.

---

### **Real-World Application of this Problem**:

1. **Data Integrity Checks**: Finding missing or duplicate entries in databases or logs.
2. **Packet Loss Detection**: Identifying missing packets in network communications.
3. **Inventory Management**: Detecting missing items in sequentially numbered inventories.

---

### **Problem Category Type**:

- **Category**: Arrays
- **Subcategory**: Mathematical, Hashing, XOR

---