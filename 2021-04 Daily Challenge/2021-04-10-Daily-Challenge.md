# Longest Increasing Path in a Matrix

**Link: [Leetcode 329 - Hard](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)**



## Desciption

Given an `m x n` integers `matrix`, return *the length of the longest increasing path in* `matrix`.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/05/grid1.jpg)

```
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: The longest increasing path is [1, 2, 6, 9].
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/27/tmp-grid.jpg)

```
Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
Output: 4
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```

**Example 3:**

```
Input: matrix = [[1]]
Output: 1
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- `0 <= matrix[i][j] <= 231 - 1`



## Solution

dfs, dp. It's soooo great to meet my friends!

```c++
class Solution {
    const int moves[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        int res = 1, m = matrix.size(), n = matrix[0].size();
        vector<vector<int> >dp(m, vector<int>(n, 0));
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                res = max(res, dfs(matrix, dp, i, j));
            }
        }
        return res;
    }
    
    int dfs(vector<vector<int> > &matrix, vector<vector<int> > &dp, int i, int j){
        if(dp[i][j]) return dp[i][j];
        int mx = 1, m = matrix.size(), n = matrix[0].size();
        for(auto move : moves){
            int x = i + move[0], y = j + move[1];
            if(x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] <= matrix[i][j]) continue;
            int len = 1 + dfs(matrix, dp, x, y);
            mx = max(mx, len);
        }
        dp[i][j] = mx;
        return mx;
    }
};
```

