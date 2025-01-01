#### **Question**

Given an M×NM \times N matrix, print its elements in a clockwise spiral manner. Return an array containing the elements in the order of their appearance when printed in a spiral manner.

---

#### **Intuition**

To traverse a matrix in a spiral manner:

1. Start from the top-left corner and move in the following order:
    - **Top row →**
    - **Right column ↓**
    - **Bottom row ←**
    - **Left column ↑**
2. After completing a boundary traversal, narrow down the matrix bounds by incrementing the top and left bounds, and decrementing the bottom and right bounds.
3. Repeat until the entire matrix is traversed.

---

#### **Solution (Iterative Approach)**

We can achieve this by maintaining four boundaries (`top`, `bottom`, `left`, `right`) and iteratively collecting elements in the spiral order.

---

#### **Implementation**

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        vector<int> result;
        int n = matrix.size();
        int m = matrix[0].size();
        int top = 0, bottom = n - 1;
        int left = 0, right = m - 1;
        int direction = 0;

        while (left <= right && top <= bottom) {
            switch (direction) {
                case 0: {
                    // Traverse left to right along the top row
                    for (int i = left; i <= right; i++) {
                        result.push_back(matrix[top][i]);
                    }
                    top++;
                    break;
                }
                case 1: {
                    // Traverse top to bottom along the right column
                    for (int i = top; i <= bottom; i++) {
                        result.push_back(matrix[i][right]);
                    }
                    right--;
                    break;
                }
                case 2: {
                    // Traverse right to left along the bottom row
                    for (int i = right; i >= left; i--) {
                        result.push_back(matrix[bottom][i]);
                    }
                    bottom--;
                    break;
                }
                case 3: {
                    // Traverse bottom to top along the left column
                    for (int i = bottom; i >= top; i--) {
                        result.push_back(matrix[i][left]);
                    }
                    left++;
                    break;
                }
            }
            direction = (direction + 1) % 4;
        }
        return result;
    }
};

```

---

#### **Edge Cases**

1. **Empty Matrix**
    
    - Input: `matrix = []`
    - Output: `[]`
    - Explanation: No elements to traverse.
2. **Single Row Matrix**
    
    - Input: `matrix = [[1, 2, 3, 4]]`
    - Output: `[1, 2, 3, 4]`
    - Explanation: The entire row is traversed as a single spiral.
3. **Single Column Matrix**
    
    - Input: `matrix = [[1], [2], [3], [4]]`
    - Output: `[1, 2, 3, 4]`
    - Explanation: The entire column is traversed as a single spiral.
4. **Square Matrix**
    
    - Input: `matrix = [[1, 2], [4, 3]]`
    - Output: `[1, 2, 3, 4]`
    - Explanation: A square matrix is traversed in layers.

---

#### **Time Complexity and Space Complexity**

- **Time Complexity**:
    
    - Each element of the matrix is visited exactly once.
    - For an M×NM \times N matrix, the time complexity is **O(M × N)**.
- **Space Complexity**:
    
    - The result array stores all elements of the matrix, requiring **O(M × N)** space.
    - No additional data structures are used, so the auxiliary space complexity is O(1)O(1).

---

#### **Key Takeaways from this Problem**

1. **Boundary Management**: Efficiently narrowing down the matrix boundaries while ensuring all elements are visited once.
2. **Layer Traversal**: Spiral traversal is essentially traversing a matrix layer by layer, which can be generalized to similar problems.
3. **Optimization**: The iterative approach avoids recursion and unnecessary stack usage.

---

#### **Mistakes and Challenges from this Problem**

1. Handling edge cases like single row or single column matrices.
2. Ensuring the conditions `top <= bottom` and `left <= right` are checked before each traversal to avoid redundant iterations.

---

#### **Real-World Application of this Problem**

1. **Image Processing**: Traversing pixels in a spiral order for image transformations.
2. **Robot Navigation**: Path planning for robots moving in a spiral trajectory to cover a surface.

---

#### **Problem Category Type**

- **Matrix Traversal**
- **Two-Pointer Technique**
- **Boundary Conditions**