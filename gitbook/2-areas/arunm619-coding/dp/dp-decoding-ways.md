
```cpp
class Solution {

public:

int numDecodings(string s) {

return decoding(s, 0);

}


int decoding(string& s, int idx) {

// we have reached the end and therefore this decoding

// contributes to 1.

if (idx == s.size())

return 1;

int totalDecodings = 0;

for (int i = 1; i <= 2 and i + idx <= s.size(); i++) {

string segment = s.substr(idx, i);

if (isValid(segment)) {

totalDecodings += decoding(s, idx + i);

}

}

return totalDecodings;

}

bool isValid(string& s) {

if (s.empty())

return false;

if (s[0] == '0')

return false;

int value = stoi(s);

return value >= 1 and value <= 26;

}

};
```

TLE in LC


Memoization

```cpp
class Solution {

public:

int numDecodings(string s) {

int n = s.size();

vector<int> dp(n+1, -1);

return decoding(s, 0, dp);

}

  

int decoding(string& s, int idx, vector<int>& dp) {

// we have reached the end and therefore this decoding

// contributes to 1.

  

if(dp[idx] != -1) return dp[idx];

if (idx == s.size())

return 1;

int totalDecodings = 0;

for (int i = 1; i <= 2 and i + idx <= s.size(); i++) {

string segment = s.substr(idx, i);

if (isValid(segment)) {

totalDecodings += decoding(s, idx + i, dp);

}

}

return dp[idx] = totalDecodings;

}

bool isValid(string& s) {

if (s.empty())

return false;

if (s[0] == '0')

return false;

int value = stoi(s);

return value >= 1 and value <= 26;

}

};
```


The problem is about decoding a string of digits into letters using the mapping (1 -> 'A', 2 -> 'B', ..., 26 -> 'Z'). The goal is to find the total number of ways to decode the string.

The intuition behind the solution is to break down the problem into smaller subproblems. For each position in the string, we have two choices:

1. Decode the current digit as a single letter. This is represented by the substring `s.substr(idx, 1)`. If this substring is valid (i.e., it represents a letter), we recursively call the `decoding` function with `idx + 1` to find the number of ways to decode the rest of the string.
    
2. Decode the current digit and the next digit as a double letter. This is represented by the substring `s.substr(idx, 2)`. If this substring is valid, we recursively call the `decoding` function with `idx + 2`.
    

The total number of ways to decode the string is the sum of the number of ways for these two choices.


The base case is when `idx` equals the size of the string, which means we have reached the end of the string. In this case, we return 1 because there is only one way to decode an empty string (i.e., do nothing).

The `isValid` function checks if a substring is valid. A substring is valid if it's not empty, its first digit is not '0', and its value is between 1 and 26.

This solution uses a top-down dynamic programming approach, also known as memoization, to solve the problem. It has a time complexity of O(n) and a space complexity of O(n), where n is the size of the string.



Unwrapping the loops:
```cpp
class Solution {

public:

int numDecodings(string s) {

int n = s.size();

vector<int> dp(n + 1, -1);

return decoding(s, 0, dp);

}

  

int decoding(string& s, int idx, vector<int>& dp) {

// we have reached the end and therefore this decoding

// contributes to 1.

  

if (dp[idx] != -1)

return dp[idx];

  

if (idx == s.size())

return 1;

int totalDecodings = 0;

// take one letter

if (idx + 1 <= s.size()) {

string segment1 = s.substr(idx, 1);

if (isValid(segment1)) {

totalDecodings += decoding(s, idx + 1, dp);

}

}

  

// take 2 letters

if (idx + 2 <= s.size()) {

string segment1 = s.substr(idx, 2);

if (isValid(segment1)) {

totalDecodings += decoding(s, idx + 2, dp);

}

}

return dp[idx] = totalDecodings;

}

bool isValid(string& s) {

if (s.empty())

return false;

if (s[0] == '0')

return false;

int value = stoi(s);

return value >= 1 and value <= 26;

}

};
```