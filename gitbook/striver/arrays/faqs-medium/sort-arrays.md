# **Sort Colors**

## **Question**

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.  
Use integers `0`, `1`, and `2` to represent the colors red, white, and blue, respectively.  
You must solve this problem **without using the library's sort function**.

---

## **Intuition**

The problem requires sorting an array with only three distinct values (`0`, `1`, and `2`).  
This can be efficiently solved using the **Dutch National Flag Algorithm** (Three-Pointer Approach).

- Use pointers to segregate `0`s, `1`s, and `2`s in a single pass.
- Leverage swapping to move elements to their correct positions without extra space.

---

## **Solution (All Approaches)**

### **1. Counting Sort**

1. Count the occurrences of `0`, `1`, and `2`.
2. Overwrite the array with the respective counts.

- **Time Complexity**: O(n)O(n)
- **Space Complexity**: O(1)O(1) (count array is constant in size).

### **2. Dutch National Flag Algorithm**

1. Maintain three pointers:
    - `low` for the position of `0`.
    - `mid` for traversal.
    - `high` for the position of `2`.
2. Traverse the array with `mid` and:
    - If `nums[mid] == 0`: Swap with `low` and move `low` and `mid` forward.
    - If `nums[mid] == 1`: Move `mid` forward.
    - If `nums[mid] == 2`: Swap with `high` and move `high` backward.
3. This ensures the array is sorted in a single pass.

- **Time Complexity**: O(n)O(n)
- **Space Complexity**: O(1)O(1).

---

## **Implementation**

### Dutch National Flag Algorithm

```cpp
class Solution {
public:
    void sortZeroOneTwo(vector<int>& nums) {
        // Initialize pointers
        int low = 0, mid = 0, high = nums.size() - 1;

        /*
        Visualization of the state:
           l        m        h
        00000   11111   xxxxx   22222
        low: points at the last sorted 0
        mid: points at the first unsorted element
        high: points at the last unsorted element
        */

        while(mid <= high) {
            switch(nums[mid]) {
                case 0: { // Move 0s to the beginning
                    swap(nums[low], nums[mid]);
                    low++;
                    mid++;
                    break;
                }

                case 1: { // Skip 1s
                    mid++;
                    break;
                }

                case 2: { // Move 2s to the end
                    swap(nums[mid], nums[high]);
                    high--;
                    break;
                }
            }
        }
    }
};

/*
Detailed diagram for understanding the operations:

Initial state:
    l           m             h
00000   11111   xxxxx   22222

case 0:
   Swap(nums[low], nums[mid])
   Increment both low and mid.

case 1:
   Increment mid.

case 2:
   Swap(nums[mid], nums[high])
   Decrement high.
*/

```

---

## **Edge Cases**

1. **Empty Array**: Ensure the function handles an empty array gracefully.
2. **Single Element Array**: Works for arrays like `[0]`, `[1]`, or `[2]`.
3. **All Same Elements**: Arrays with all `0`s, `1`s, or `2`s.
4. **Already Sorted Array**: No unnecessary swaps should occur.

---

## **Time Complexity**

- **Dutch National Flag Algorithm**: O(n)O(n), where nn is the size of the array.

## **Space Complexity**

- **In-place Sorting**: O(1)O(1), no additional data structures are used.

---

## **Key Takeaways from this Problem**

1. The **Dutch National Flag Algorithm** is a powerful technique for sorting arrays with limited distinct values.
2. Optimal solutions often utilize multiple pointers for in-place operations.
3. Understanding the constraints (three unique values) helps design efficient algorithms.

---

## **Mistakes and Challenges from this Problem**

1. **Overlapping Pointers**: Mishandling the movement of `mid` and `high` pointers can lead to incorrect results.
2. **Extra Swaps**: Swapping unnecessarily when values are already in the correct place can increase runtime.
3. **Understanding Constraints**: Misinterpreting the problem constraints can lead to incorrect implementations.

---

## **Real-World Application of this Problem**

1. Sorting or categorizing items with a limited set of distinct values (e.g., product categories).
2. Partitioning problems where elements need to be segregated into groups.

---

## **Problem Category Type**

- **Array**
- **Two-pointer Technique**
- **Sorting**
