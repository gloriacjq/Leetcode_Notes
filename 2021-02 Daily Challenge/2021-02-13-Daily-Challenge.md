# Shortest Path in Binary Matrix

**Link: [Leetcode 1091 - Medium](https://leetcode.com/problems/shortest-path-in-binary-matrix/)**



## Desciption

In an N by N square grid, each cell is either empty (0) or blocked (1).

A *clear path from top-left to bottom-right* has length `k` if and only if it is composed of cells `C_1, C_2, ..., C_k` such that:

- Adjacent cells `C_i` and `C_{i+1}` are connected 8-directionally (ie., they are different and share an edge or corner)
- `C_1` is at location `(0, 0)` (ie. has value `grid[0][0]`)
- `C_k` is at location `(N-1, N-1)` (ie. has value `grid[N-1][N-1]`)
- If `C_i` is located at `(r, c)`, then `grid[r][c]` is empty (ie. `grid[r][c] == 0`).

Return the length of the shortest such clear path from top-left to bottom-right. If such a path does not exist, return -1.

 

**Example 1:**

```
Input: [[0,1],[1,0]]


Output: 2
```

**Example 2:**

```
Input: [[0,0,0],[1,1,0],[1,1,0]]


Output: 4
```



**Note:**

1. `1 <= grid.length == grid[0].length <= 100`
2. `grid[r][c]` is `0` or `1`



## Solution

BFS to solve the single-source unweighted shortest path problem.

The struct Cell can be replaced by pair<pair<int, int>, int>.

```c++
class Solution {
    struct Cell{
        int x, y, dis;
    };
    
    int mov[8][2] = {{-1,-1}, {-1,0}, {-1,1}, {0,-1}, {0,1}, {1,-1}, {1,0}, {1,1}};

public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        if(grid.front().front() || grid.back().back()) return -1;
        int n = grid.size();
        vector<vector<bool>> isVisited(n, vector<bool>(n,false));
        queue<Cell> q;
        Cell start = {0, 0, 1};
        isVisited[0][0] = true;
        q.push(start);
        while(!q.empty()){
            Cell cell = q.front();
            q.pop();
            if(cell.x == n-1 && cell.y == n-1) return cell.dis;
            for(int i = 0; i < 8; i++){
                int row = cell.x + mov[i][0];
                int col = cell.y + mov[i][1];
                if(row >= 0 && row < n && col >= 0 && col < n 
                   && grid[row][col] == 0 && !isVisited[row][col]){
                    Cell next = {row, col, cell.dis + 1};
                    isVisited[row][col] = true;
                    q.push(next);
                }
            }
        }
        return -1;
    }
};
```

An example solution with better space efficiency.

```c++
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int N = grid.size();
        if(grid[0][0]==1 || grid[N-1][N-1]==1) return -1;
        
        int dr[8] = {1,0,-1,0,1,-1,-1,1};
        int dc[8] = {0,1,0,-1,1,-1,1,-1};
        
        queue<int> q;//1D indices
        q.push(0);//top-left corner
        int res = INT_MAX;
        grid[0][0]=1;
        
        while(!q.empty()){
            int pos = q.front();q.pop();
            int r = pos/N;
            int c = pos%N;
            int dist = grid[r][c];
            if(r==N-1 && c==N-1) return dist;
            
            for(int k=0;k<8;k++){
                int nr = r+dr[k];
                int nc = c+dc[k];
                if(nr>=0 && nr<N && nc>=0 && nc<N && grid[nr][nc]==0){
                    q.push(nr*N+nc);
                    grid[nr][nc]=dist+1;
                }
            }
        }
        
        return -1;
    }
};
```

