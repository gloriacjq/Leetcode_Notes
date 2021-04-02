# Ones and Zeroes

**Link: [Leetcode 474 - Medium](https://leetcode.com/problems/ones-and-zeroes/)**



## Desciption

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return *the size of the largest subset of `strs` such that there are **at most*** `m` `0`*'s and* `n` `1`*'s in the subset*.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

 

**Example 1:**

```
Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4
Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.
```

**Example 2:**

```
Input: strs = ["10","0","1"], m = 1, n = 1
Output: 2
Explanation: The largest subset is {"0", "1"}, so the answer is 2.
```

 

**Constraints:**

- `1 <= strs.length <= 600`
- `1 <= strs[i].length <= 100`
- `strs[i]` consists only of digits `'0'` and `'1'`.
- `1 <= m, n <= 100`



## Solution

A dp question. Not difficult but also not easy for me to solve it quickly, I should practice more.

```c++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        int size = strs.size();
        vector<vector<int> > cnts(size, vector<int>(2, 0));
        for(int i = 0; i < size; i++){
            for(char c : strs[i]){
                ++cnts[i][c-'0'];
            }
        }
        
        vector<vector<int> > dp(m+1, vector<int>(n+1, 0));
        for(auto cnt : cnts){
            for(int i = m; i >= cnt[0]; i--)
                for(int j = n; j >= cnt[1]; j--)
                    dp[i][j] = max(dp[i][j], dp[i-cnt[0]][j-cnt[1]] + 1);
        }
        return dp[m][n];
    }
};

// Runtime: 268 ms
// Memory Usage: 10.2 MB
```

After optimization.

```c++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        int size = strs.size();
        int dp[m+1][n+1];
        memset(dp, 0, sizeof(dp));
        dp[0][0]=0;
        for(int i = 0; i < size; i++){
            int zeros = 0, ones = 0;
            for(char c : strs[i]){
                if(c == '0') zeros++;
                else ones++;
            }
            for(int i = m; i >= zeros; i--){
                for(int j = n; j >= ones; j--){
                    dp[i][j] = max(dp[i][j], dp[i-zeros][j-ones] + 1);
                }
            }
        }

        return dp[m][n];
    }
};

// Runtime: 52 ms
// Memory Usage: 8.7 MB
```

One of the official solutions, quite clear.

```c++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1));
        for (const string &s : strs) {
            int cnt0 = count(s.begin(), s.end(), '0');
            int cnt1 = count(s.begin(), s.end(), '1');
            for (int i = m; i >= cnt0; --i) {
                for (int j = n; j >= cnt1; --j) {
                    dp[i][j] = max(dp[i][j], 1 + dp[i-cnt0][j-cnt1]);
                }
            }
        }
        return dp[m][n];
    }
};
```

