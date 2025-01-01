
**Question**:  
Given an unsorted array of integers, find the length of the longest consecutive elements sequence. The sequence must be contiguous, meaning the elements must be consecutive integers, but not necessarily sorted.

**Intuition**:  
The goal is to identify the longest subsequence of consecutive integers. 

A brute force solution could check every possible subsequence and determine if it's consecutive, but this would have a time complexity of $O(n^2)$, which is inefficient for large arrays. 

Instead, we can take advantage of a hash set or sorting to speed up the search. By utilizing a set or map, we can check if consecutive elements exist in constant time, leading to a more efficient solution.

**Solution (all approaches)**:

1. **Using a HashSet** (Optimal Approach):
    
    - Use a HashSet to store all the elements of the array.
    - For each element, check if it's the start of a sequence (i.e., `num-1` is not in the set). If it's the start, keep checking for consecutive numbers (`num+1`, `num+2`, etc.) until no more consecutive numbers are found.
    - The length of the sequence found for each starting element is tracked, and the maximum length is returned.
    
    **Time Complexity**: $O(n)$
    **Space Complexity**: $O(n)$
    
    **Code** (C++):
    
    ```cpp
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> numSet(nums.begin(), nums.end());
        int longest = 0;
    
        for (int num : nums) {
            if (numSet.find(num - 1) == numSet.end()) {  // Check if it's the start of a sequence
                int currentNum = num;
                int length = 1;
    
                while (numSet.find(currentNum + 1) != numSet.end()) {
                    currentNum++;
                    length++;
                }
    
                longest = max(longest, length);
            }
        }
    
        return longest;
    }
    ```
    
2. **Using Sorting**:
    
    - Sort the array first, then iterate through it to find consecutive elements.
    - The time complexity of sorting the array is O(nlog⁡n)O(n \log n), and the iteration to find the longest sequence is O(n)O(n), making this approach less efficient than using a hash set.
    
    **Time Complexity**: $O(n \log n)$
    **Space Complexity**: $O(1)$ (if sorting in-place)
    
    **Code** (C++):
    
    ```cpp
    int longestConsecutive(vector<int>& nums) {
        if (nums.empty()) return 0;
        sort(nums.begin(), nums.end());
        
        int longest = 1, currentLength = 1;
    
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == nums[i - 1]) continue;  // Skip duplicates
            if (nums[i] == nums[i - 1] + 1) {
                currentLength++;
            } else {
                longest = max(longest, currentLength);
                currentLength = 1;
            }
        }
    
        return max(longest, currentLength);
    }
    ```
    

**Edge Cases**:

- Empty array: Return 0.
- Array with all duplicates: The longest sequence length is 1.
- Array with a single element: The longest sequence length is 1.
- Array with multiple non-consecutive elements: Ensure sequences are counted separately.

**Time Complexity and Space Complexity**:

- **Optimal Approach (HashSet)**:
    
    - Time Complexity: $O(n)$, since inserting elements into the set and checking for the next consecutive element takes constant time on average.
    - Space Complexity: $O(n)$, for the hash set storing the elements.
- **Sorting Approach**:
    
    - Time Complexity: $O(n \log n)$ due to sorting.
    - Space Complexity: $O(1)$ if sorting in-place.

**Key Takeaways from this Problem**:

- The most efficient solution uses a hash set to track elements, allowing for quick lookups and ensuring a linear time solution.
- Sorting is a valid alternative, but it's less optimal due to the  $O(n \log n)$ complexity.

**Mistakes and Challenges from this Problem**:

- Forgetting to check for duplicates in the sorted approach can lead to incorrect answers.
- Misunderstanding the difference between sorting the array and using a hash set may cause unnecessary complexity.

**Real-World Application of this Problem**:

- Finding consecutive sequences in datasets like stock prices, where we might want to identify consecutive days with increasing or decreasing prices.
- Analyzing data for patterns, such as streaks in gaming or continuous events.

**Problem Category Type**:  
Arrays, Hashing, Sorting