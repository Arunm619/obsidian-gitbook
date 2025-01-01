```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        // Initialize a result vector to hold all rows of Pascal's Triangle
        vector<vector<int>> result(numRows);

        // Iterate through each row
        for (int i = 0; i < numRows; i++) {
            // Resize the current row to hold the appropriate number of elements
            result[i].resize(i + 1);

            // The first and last elements of each row are always 1
            result[i][0] = 1;
            result[i][i] = 1;

            // Fill the internal elements of the row
            for (int j = 1; j < i; j++) {
                // Each element is the sum of the two elements directly above it
                result[i][j] = result[i - 1][j - 1] + result[i - 1][j];
            }
        }

        return result;
    }
};

```


Learning is that create n Rows and resize them based on len of the row. 
its a 2d array. so resize has to happen on the 1d array.

diagonal + up is the formula.
