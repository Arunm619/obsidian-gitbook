

### **Cheat Sheet: Prefix Sum Arrays**

---

### **Mental Model**

1. **What is a Prefix Sum Array?**
    
    - A prefix sum array is a precomputed array where each element at index ii represents the sum of elements in the original array from the start up to i−1i-1 (or just ii, depending on implementation).
2. **Why Use It?**
    
    - To quickly calculate the sum of elements in a range.
    - It reduces the time complexity of range sum queries from O(k) to O(1), where kk is the size of the queried range.
3. **How Does It Work?**
    
    - By storing cumulative sums, you can subtract to isolate the sum of any subarray: $\text{Sum of range } [L, R] = \text{prefix}[R+1] - \text{prefix}[L]$
4. **Key Idea:**
    
    - Convert a problem that involves repeated summations into a problem involving subtraction between precomputed values.

---

### **General Intuition**

1. **Think of it as a Bank Statement:**
    
    - The prefix sum array is like a cumulative record of all deposits/withdrawals up to a point.
    - To find the net transaction in a specific period, you subtract the balance at the start of the period from the balance at the end.
2. **Efficient Range Queries:**
    
    - Instead of recalculating the sum every time for a range, imagine having a running tally (prefix sum). Subtraction isolates what you're interested in.
3. **Build Once, Query Many:**
    
    - Construct the prefix sum array once (in O(n)).
    - Perform range queries in O(1).

---

### **Steps to Use a Prefix Sum Array**

#### 1. **Build the Prefix Sum Array**

- Initialise an array `prefix` of size n+1n+1, with $\text{prefix}[0] = 0$
- Populate `prefix`: $\text{prefix}[i] = \text{prefix}[i-1] + \text{original}[i-1]$

#### 2. **Answer Range Queries**

- For a range `[L, R]`: $\text{Sum} = \text{prefix}[R+1] - \text{prefix}[L]$

---

### **Template**

#### **1. Prefix Sum Array Construction**

```cpp
vector<int> buildPrefixSum(const vector<int>& arr) {
    int n = arr.size();
    vector<int> prefix(n + 1, 0); // Prefix array with an extra initial 0
    for (int i = 1; i <= n; i++) {
        prefix[i] = prefix[i - 1] + arr[i - 1];
    }
    return prefix;
}
```

#### **2. Range Sum Query**

```cpp
int rangeSum(const vector<int>& prefix, int L, int R) {
    return prefix[R + 1] - prefix[L]; // Inclusive range [L, R]
}
```

#### **3. Usage**

```cpp
vector<int> arr = {1, 2, 3, 4, 5}; // Original array
vector<int> prefix = buildPrefixSum(arr);

int sum1 = rangeSum(prefix, 1, 3); // Sum of elements in range [1, 3] (2 + 3 + 4)
int sum2 = rangeSum(prefix, 0, 4); // Sum of all elements (1 + 2 + 3 + 4 + 5)
```

---

### **Key Variations**

1. **2D Prefix Sum**
    
    - Used for range queries in a 2D grid.
    - Each cell stores the sum of all elements in the rectangle from the top-left corner to that cell.
2. **Dynamic Prefix Sum**
    
    - If elements in the array change frequently, use a Fenwick Tree (BIT) or Segment Tree instead.

---

### **Examples**

1. **1D Array Example**
    
    - Original: `[2, 3, 5, 8]`
    - Prefix: `[0, 2, 5, 10, 18]`
    - Query `[1, 2]`: `prefix[2+1] - prefix[1] = 10 - 2 = 8`
2. **Binary Array (Count Ones)**
    
    - Original: `[1, 0, 1, 1, 0]`
    - Prefix: `[0, 1, 1, 2, 3, 3]`
    - Query `[2, 4]`: `prefix[4+1] - prefix[2] = 3 - 1 = 2`

---

### **Common Applications**

1. **Range Sum Queries**
    
    - Quickly find the sum of elements in any range.
2. **Frequency Counting**
    
    - Use prefix sums to count the occurrence of specific conditions.
3. **Binary Strings**
    
    - Count the number of `1`s or `0`s in a substring.
4. **2D Range Queries**
    
    - Find the sum of elements in a submatrix.

---

### **Key Takeaways**

- **Precompute and Save Time**: Build the prefix sum array once and enjoy constant-time range queries.
- **Subtraction Is Key**: Isolate the sum of a range by subtracting cumulative sums.
- **Avoid Redundant Work**: Instead of recalculating sums repeatedly, precompute to simplify.



### **Prefix Sum Array Basics**

The prefix sum array `prefix` is constructed such that:

- $\text{prefix}[i]$ represents the sum of the first ii elements in the original array (or the `processed` array in this case).

For an array `processed`:

- $\text{prefix}[i] = \text{prefix}[i-1] + \text{processed}[i-1]$
- $\text{prefix}[0] = 0$, indicating no elements are summed.

For example: If `processed = [1, 1, 0]`, the prefix array `prefix` is:

- $\text{prefix}[0] = 0$
- $\text{prefix}[1] = \text{prefix}[0] + \text{processed}[0] = 0 + 1 = 1$
- $\text{prefix}[2] = \text{prefix}[1] + \text{processed}[1] = 1 + 1 = 2$
- $\text{prefix}[3] = \text{prefix}[2] + \text{processed}[2] = 2 + 0 = 2$

Thus, `prefix = [0, 1, 2, 2]`.

---

### **Why `prefix[end + 1] - prefix[start]` Works**

When we want the sum of elements in the range `[start, end]` (inclusive), we can observe the following:

- The sum of elements from `start` to `end` is: $\text{Sum} = \text{processed}[start] + \text{processed}[start+1] + \dots + \text{processed}[end]$
- In terms of the prefix sum array: 
- $\text{prefix}[end + 1] = \text{Sum of all elements from index 0 to end (inclusive)}$
- $\text{prefix}[start] = \text{Sum of all elements from index 0 to start - 1 (inclusive)}$

By subtracting:

$\text{prefix}[end + 1] - \text{prefix}[start] = \text{Sum of all elements from start to end (inclusive)}.$

### **Efficiency**

This subtraction gives us the sum in $O(1)$ time, as opposed to iterating through the range `[start, end]`, which would take $O(k)$, where  $\text{end} - \text{start} + 1$.

---

### **Example Walkthrough**

#### Input:

`processed = [1, 1, 0]`  
`prefix = [0, 1, 2, 2]`  
Query: `[0, 1]` (sum from index 0 to 1)

#### Steps:

1. **Compute prefix indices**:
    
    - $\text{prefix}[end + 1] = \text{prefix}[1 + 1] = \text{prefix}[2] = 2$
    - $\text{prefix}[start] = \text{prefix}[0] = 0$
2. **Calculate result**:
    
    $\text{result} = \text{prefix}[2] - \text{prefix}[0] = 2 - 0 = 2$

This matches the sum of `processed[0] + processed[1] = 1 + 1 = 2`.

---

### **Why It Works**

This works because the prefix sum array stores cumulative sums, which allows us to isolate any range's sum using subtraction. This approach avoids redundant computations and makes range-sum queries very efficient.