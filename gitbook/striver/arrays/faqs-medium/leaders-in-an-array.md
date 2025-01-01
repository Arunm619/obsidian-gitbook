#### **Question**

Given an integer array `nums`, return a list of all the leaders in the array.

- A leader in an array is an element whose value is strictly greater than all elements to its right in the given array.
- The rightmost element is always a leader.
- The output must retain the order of appearance of leaders in the input array.

---

#### **Intuition**

To find leaders in an array:

- Start iterating from the **rightmost element** since the rightmost element is always a leader.
- Maintain a variable `max_from_right` to track the maximum value encountered so far while traversing the array in reverse.
- Compare each element with `max_from_right`. If it is greater, it is a leader.
- Insert the leader into the result list in reverse order since we are traversing backward.

---

#### **Solution (Optimal Approach)**

We traverse the array once in reverse to find all leaders. Then reverse the result list to retain the original order of leaders.

---

#### **Implementation**

```cpp
class Solution {
public:
    vector<int> findLeaders(vector<int>& nums) {
        vector<int> leaders; 
        int max_from_right = INT_MIN;

        // Traverse the array from right to left
        for (int i = nums.size() - 1; i >= 0; --i) {
            if (nums[i] > max_from_right) {
                leaders.push_back(nums[i]);
                max_from_right = nums[i];
            }
        }

        // Reverse the list to maintain the original order of leaders
        reverse(leaders.begin(), leaders.end());
        return leaders;
    }
};
```

---

#### **Edge Cases**

1. **Single Element Array**
    - Input: `nums = [7]`
    - Output: `[7]`
    - Explanation: The only element is the leader.
2. **Array with All Identical Elements**
    - Input: `nums = [5, 5, 5, 5]`
    - Output: `[5]`
    - Explanation: Only the rightmost element qualifies as a leader.
3. **Array with Decreasing Elements**
    - Input: `nums = [10, 9, 8, 7]`
    - Output: `[10, 9, 8, 7]`
    - Explanation: Every element is a leader as each element is greater than all elements to its right.

---

#### **Time Complexity and Space Complexity**

- **Time Complexity**:
    
    - We traverse the array once in reverse order.
    - Reversing the result list also takes O(k), where k is the number of leaders.
    - Thus, the overall time complexity is **O(n)**.
- **Space Complexity**:
    
    - We use a vector to store the leaders, which takes O(k) space, where kk is the number of leaders.
    - Therefore, the space complexity is **O(k)**.

---

#### **Key Takeaways from this Problem**

1. **Reverse Traversal**: Useful when decisions are based on elements to the right.
2. **Order Maintenance**: Handle the order of results when traversing backward by reversing the result.
3. **Efficient Updates**: Use a single variable to track the maximum on-the-fly during traversal.

---

#### **Mistakes and Challenges from this Problem**

1. Forgetting to reverse the result list to maintain the original order of leaders.
2. Assuming all elements can be leaders without properly verifying with `max_from_right`.

---

#### **Real-World Application of this Problem**

1. **Stock Market Analysis**: Identify peak days (leaders) in a list of stock prices.
2. **Game Scores**: Find all instances where a player's score is higher than all subsequent scores in a game log.

---

#### **Problem Category Type**

- **Arrays**
- **Reverse Traversal**
- **Greedy Approach**

