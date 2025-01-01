

### **Question**

Given an array `nums`, an **inversion** is a pair of indices $(i,j)$ such that $i<j$ and $nums[i]>nums[j]$

Return the total number of inversions in the array.

---

### **Intuition**

To count inversions, the naive solution is to compare every pair of elements, but this results in $O(n^2)$ complexity. Instead, we can use **merge sort**, a divide-and-conquer approach, to count inversions while sorting the array.

Key Idea:

- During the merge step of merge sort, whenever we place an element from the right subarray before an element in the left subarray, it contributes to the inversion count.

---

### **Solution (All Approaches)**

#### **Approach 1: Brute Force**

Iterate through every pair of elements (i,j) where i<j, and count pairs where $nums[i]>nums[j]$

**Steps**:

1. Use two nested loops to check all pairs.
2. Increment the inversion count when nums[i]>nums[j]

**Time Complexity:** $O(n^2)$.  
**Space Complexity:** $O(1)$.

---

#### **Approach 2: Merge Sort (Optimal)**

Count inversions during the merge step of merge sort.

**Steps**:

1. Divide the array recursively into two halves.
2. Merge the two halves while counting the inversions:
    - If $nums[i] > nums[j]$, all elements from $nums[i]$ to the end of the left subarray form inversions with $nums[j]$
3. Return the total count of inversions.

**Time Complexity:** $O(n \log n)$.  
**Space Complexity:** $O(n)$ for temporary arrays during merging.

---

### **Implementation**

#### **Merge Sort Solution**

```cpp
class Solution {
public:
    long long int numberOfInversions(vector<int>& arr) {
        long long int inversions = 0;
        mergeSort(arr, 0, arr.size()-1, inversions);
        return inversions;
    }
    
private:
    void mergeSort(vector<int>& arr, int left, int right, long long int& inversions) {
        if (left < right) {
            int mid = left + (right - left)/2;
            
            mergeSort(arr, left, mid, inversions);
            mergeSort(arr, mid + 1, right, inversions);
            
            merge(arr, left, mid, right, inversions);
        }
    }
    
    void merge(vector<int>& arr, int left, int mid, int right, long long int& inversions) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        vector<int> leftArr(n1), rightArr(n2);
        
        // Copy data to temporary arrays
        for(int i = 0; i < n1; i++)
            leftArr[i] = arr[left + i];
        for(int i = 0; i < n2; i++)
            rightArr[i] = arr[mid + 1 + i];
        
        int i = 0, j = 0, k = left;
        
        while(i < n1 && j < n2) {
            if(leftArr[i] <= rightArr[j]) {
                arr[k] = leftArr[i];
                i++;
            }
            else {
                arr[k] = rightArr[j];
                // Key line for counting inversions
                inversions += n1 - i;
                j++;
            }
            k++;
        }
        
        // Copy remaining elements
        while(i < n1) {
            arr[k] = leftArr[i];
            i++; k++;
        }
        while(j < n2) {
            arr[k] = rightArr[j];
            j++; k++;
        }
    }
};
```

---

### **Edge Cases**

1. **Empty array:** `[]` → Output: `0`.
2. **Single element:** `[1]` → Output: `0`.
3. **Sorted array:** `[1, 2, 3, 4]` → Output: `0`.
4. **Reverse sorted array:** `[4, 3, 2, 1]` → Output: 66.

---

### **Time Complexity and Space Complexity**

| **Approach** | **Time Complexity** | **Space Complexity** |
| ------------ | ------------------- | -------------------- |
| Brute Force  | $O(n^2)$            | $O(1)$               |
| Merge Sort   | $O(n \log n)$       | $O(n)$               |

---

### **Key Takeaways from this Problem**

1. Merge sort is a powerful tool for counting inversions efficiently.
2. Understanding the merge step and how it contributes to inversion counting is crucial.
3. Divide-and-conquer is an effective strategy for solving problems that involve comparing subsets of elements.

---

### **Mistakes and Challenges**

1. Forgetting to count inversions for all remaining elements in the left subarray during the merge step.
2. Mishandling the indices during merging and copying.

---

### **Real-World Application of this Problem**

1. **Comparing rankings:** Determining how far one ranking is from another (e.g., Kendall Tau distance).
2. **Inversion analysis:** Inversions can represent disruptions or anomalies in datasets, such as market data or preferences.

---

### **Problem Category Type**

Arrays, Divide-and-Conquer.

```cpp
class Solution {
public:
    long long int numberOfInversions(vector<int>& arr) {
        long long int inversions = 0;
        mergeSort(arr, 0, arr.size()-1, inversions);
        return inversions;
    }
    
private:
    void mergeSort(vector<int>& arr, int left, int right, long long int& inversions) {
        if (left < right) {
            int mid = left + (right - left)/2;
            
            mergeSort(arr, left, mid, inversions);
            mergeSort(arr, mid + 1, right, inversions);
            
            merge(arr, left, mid, right, inversions);
        }
    }
    
    void merge(vector<int>& arr, int left, int mid, int right, long long int& inversions) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        vector<int> leftArr(n1), rightArr(n2);
        
        // Copy data to temporary arrays
        for(int i = 0; i < n1; i++)
            leftArr[i] = arr[left + i];
        for(int i = 0; i < n2; i++)
            rightArr[i] = arr[mid + 1 + i];
        
        int i = 0, j = 0, k = left;
        
        while(i < n1 && j < n2) {
            if(leftArr[i] <= rightArr[j]) {
                arr[k] = leftArr[i];
                i++;
            }
            else {
                arr[k] = rightArr[j];
                // Key line for counting inversions
                inversions += n1 - i;
                j++;
            }
            k++;
        }
        
        // Copy remaining elements
        while(i < n1) {
            arr[k] = leftArr[i];
            i++; k++;
        }
        while(j < n2) {
            arr[k] = rightArr[j];
            j++; k++;
        }
    }
};
```

## Core Intuition

The algorithm leverages merge sort's divide-and-conquer strategy to count inversions efficiently:

1. **Divide**: Split array into two halves
2. **Conquer**: Recursively count inversions in both halves
3. **Combine**: Count split inversions during merge

The key insight is during the merge step:
- When an element from right subarray is smaller than left subarray element
- It forms inversions with all remaining elements in left subarray
- We can count these inversions in O(1) using `n1 - i`

## Time and Space Complexity

**Time Complexity**: $O(n log n)$
- Divide: $O(1)$
- Recursive calls: T(n) = 2T(n/2)
- Merge: O(n)
- Overall recurrence: T(n) = 2T(n/2) + O(n)
- Solves to O(n log n)

**Space Complexity**: O(n)
- Temporary arrays in merge: O(n)
- Recursion stack: O(log n)
- Maximum space used: O(n)

## Example Walkthrough
```
Original array: [5, 2, 3, 1]

Step 1: Divide [5, 2] [3, 1]
Step 2: Divide [5] [2] and [3] [1]
Step 3: Merge [2, 5] (1 inversion) and [1, 3] (1 inversion)
Step 4: Final merge [2, 5] and [1, 3]
        - 1 < 2: Add 2 inversions (1,2), (1,5)
        - 3 > 2: No inversions
        Final: [1, 2, 3, 5] with 4 total inversions
```

## Key Points
1. Uses `<=` in comparison to handle duplicates correctly
2. Maintains stability of merge sort
3. Counts each inversion exactly once
4. Works with both positive and negative numbers
5. Handles duplicates correctly