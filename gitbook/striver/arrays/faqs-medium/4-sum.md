Apologies for not following your structure earlier. Here's the **4 Sum** solution presented using your preferred structure:

---

# **4 Sum Problem**

## **Question**

Given an integer array `nums` and an integer `target`, return all unique quadruplets [nums[a],nums[b],nums[c],nums[d]][nums[a], nums[b], nums[c], nums[d]] such that:

1. a≠b≠c≠da \neq b \neq c \neq d
2. nums[a]+nums[b]+nums[c]+nums[d]=targetnums[a] + nums[b] + nums[c] + nums[d] = \text{target}

The solution set must not contain duplicate quadruplets.

---

## **Intuition**

1. Sorting the array simplifies duplicate handling and allows efficient two-pointer traversal.
2. Fix two numbers and find the remaining two using a two-pointer approach.
3. Avoid duplicates by skipping over repeated elements during iteration.

---

## **Solution (All Approaches)**

### **1. Brute Force**

Generate all possible quadruplets, check their sums, and filter duplicates.

- **Time Complexity**: O(n4)O(n^4)
- **Space Complexity**: O(k)O(k) (for storing results).

### **2. Optimal Approach**

1. **Sort the array**.
2. Use nested loops for the first two numbers (nums[a],nums[b]nums[a], nums[b]).
3. Use a **two-pointer** approach for the remaining two numbers (nums[c],nums[d]nums[c], nums[d]).
4. Skip duplicates and adjust pointers to explore all valid combinations.

---

## **Implementation**

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        sort(begin(nums), end(nums));
        vector<vector<int>> result;
        for(int i = 0; i < n; i ++) {
            int first = nums[i];
            // Skipping duplicates for first.
            if(i > 0 and nums[i] == nums[i-1]) continue;

            for(int j = i+1; j < n; j ++) {
                int second = nums[j];
                // Skipping duplicates for second.
                if(j > i + 1 and nums[j] == nums[j-1]) continue;

                int left = j + 1, right = n - 1;

                while(left < right) {
                    int third = nums[left];
                    int fourth = nums[right];
                    long long sum = first + second + third + fourth;
                    if(sum == target) {
                        // Process the quadruplet.
                        result.push_back({first, second, third, fourth});
                        left++, right--;

                        // Skip all the duplicates for third.
                        while(left < right and third == nums[left]) left++;

                        // Skip all the duplicates for fourth.
                        while(left < right and fourth == nums[right]) right--;

                    } else if(sum < target) {
                        // Look for a bigger number.
                        left++;
                    } else {
                        // Look for a smaller number.
                        right--;
                    }
                }
            }
        }
        return result;
    }
};

```

---

## **Edge Cases**

1. **Empty Array**: Return an empty list if fewer than 4 elements are present.
2. **Duplicate Elements**: Skip repeated numbers during traversal.
3. **Large Integers**: Use `long long` to prevent overflow during summation.

---

## **Time Complexity**

- **Sorting**: $O(n \log n)$
- **Outer Loops**: $O(n^2)$
- **Two-pointer Search**: O(n)
    **Overall**: $O(n^3)$

## **Space Complexity**

- $O(k)$, where k is the number of unique quadruplets stored in the result.

---

## **Key Takeaways from this Problem**

1. Sorting helps simplify duplicate handling and allows efficient traversal techniques.
2. Multi-pointer techniques can optimize nested loops for problems involving sums.
3. Always consider potential overflow for problems involving large numbers.

---

## **Mistakes and Challenges from this Problem**

1. **Handling Duplicates**: Forgetting to skip duplicate numbers can lead to redundant results.
2. **Overflow Issues**: Summing four numbers may exceed the integer limit; using `long long` is crucial.
3. Missed to sort the array!


---

## **Real-World Application of this Problem**

1. Financial systems to identify groups of transactions that sum to a specific value.
2. Combination problems in logistics or inventory optimization.

---

## **Problem Category Type**

- **Array**
- **Two-pointer**
- **Sorting**

