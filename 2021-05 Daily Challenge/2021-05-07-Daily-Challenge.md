# title

**Link: [Leetcode 583 - Medium](https://leetcode.com/problems/delete-operation-for-two-strings/)**



## Desciption

Given two strings `word1` and `word2`, return *the minimum number of **steps** required to make* `word1` *and* `word2` *the same*.

In one **step**, you can delete exactly one character in either string.

 

**Example 1:**

```
Input: word1 = "sea", word2 = "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

**Example 2:**

```
Input: word1 = "leetcode", word2 = "etco"
Output: 4
```

 

**Constraints:**

- `1 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of only lowercase English letters.



## Solution

Toooo tired today. Will optimize it later.

```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n1 = word1.size(), n2 = word2.size();
        vector<vector<int>> dp(n1 + 1, vector<int>(n2 + 1, 0));
        for (int i = 1; i <= n1; ++i) {
            for (int j = 1; j <= n2; ++j) {
                if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return n1 + n2 - 2 * dp[n1][n2];
    }
};
```

