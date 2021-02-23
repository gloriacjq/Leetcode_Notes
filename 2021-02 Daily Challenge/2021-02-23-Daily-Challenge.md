# Search a 2D Matrix II

**Link: [Leetcode 240 - Medium](https://leetcode.com/problems/search-a-2d-matrix-ii/)**



## Desciption

Write an efficient algorithm that searches for a `target` value in an `m x n` integer `matrix`. The `matrix` has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= n, m <= 300`
- `-109 <= matix[i][j] <= 109`
- All the integers in each row are **sorted** in ascending order.
- All the integers in each column are **sorted** in ascending order.
- `-109 <= target <= 109`



## Solution

Search from top-right to bottom-left.

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row = matrix.size(), col = matrix.front().size();
        int r = 0, c = col - 1;
        while(r < row && c >= 0){
            if(matrix[r][c] == target) return true;
            if(matrix[r][c] < target) r++;
            else c--;
        }
        return false;
    }
};
```

