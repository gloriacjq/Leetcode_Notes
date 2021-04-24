# Critical Connections in a Network

**Link: [Leetcode 1192 - Hard](https://leetcode.com/problems/critical-connections-in-a-network/)**



## Desciption

There are `n` servers numbered from `0` to `n-1` connected by undirected server-to-server `connections` forming a network where `connections[i] = [a, b]` represents a connection between servers `a` and `b`. Any server can reach any other server directly or indirectly through the network.

A *critical connection* is a connection that, if removed, will make some server unable to reach some other server.

Return all critical connections in the network in any order.

 

**Example 1:**

**![img](https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png)**

```
Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
```

 

**Constraints:**

- `1 <= n <= 10^5`
- `n-1 <= connections.length <= 10^5`
- `connections[i][0] != connections[i][1]`
- There are no repeated connections.



**Hint:** Use Tarjan's algorithm.



## Solution

Today's challenge is a bit difficult for me, I'm too tired to write notes in English. Let's change a writing language XD.

dfn[x] ：时间戳，标记图中每个节点在进行深度优先搜索时被访问的时间顺序。

low[x] ：追溯值，表示从当前节点 x 作为搜索树的根节点出发，能够访问到的所有节点中，时间戳最小的值。

对每个节点 i，第一次访问时用全局变量index赋值给dfn[i] 和 low[i]，然后dfs访问其子节点，其子节点 j 有下列两种情况：

1. 未访问过

   对孩子节点 j 进行dfs；

   对孩子节点 j dfs结束后，比较dfn[i] 和 low[j]的关系。若dfn[i] < low[j] ，说明 j 节点无法连接到 i 的前继节点，该边为桥。

2. 访问过（由于是无向图，访问的子节点不能是它的父节点）

   比较dfn[j] 和 low[i]，若low[i] > dfn[j]，更新 low[i] = dfn[j]，此时出现back edge，在节点 i 有另一条路径到出现时间为j的节点，形成环。

**Reference:**  [Blog - Critical Connections in a Network](https://www.cnblogs.com/yaoyudadudu/p/11724056.html) , [Wikipedia - Tarjan's strongly connected components algorithm](https://en.wikipedia.org/wiki/Tarjan%27s_strongly_connected_components_algorithm) , [Zhihu - Tarjan algorithm](https://zhuanlan.zhihu.com/p/101923309)

```c++
class Solution {
    vector<vector<int>> neighbors;
    vector<int> dfn;
    vector<int> low;
    int index;
    void init(int n, vector<vector<int>>& connections){
        index = 0;
        dfn.resize(n);
        low.resize(n);
        neighbors.resize(n);
        for(auto c : connections){
            neighbors[c[0]].push_back(c[1]);
            neighbors[c[1]].push_back(c[0]);
        }
    }
    void tarjan(int curNode, int parentNode, vector<vector<int>>& ans){
        dfn[curNode] = low[curNode] = ++index;
        for(auto child : neighbors[curNode]){
            if(child == parentNode) continue;
            if(!dfn[child]){
                tarjan(child, curNode, ans);
                low[curNode] = min(low[curNode], low[child]);
                if(low[child] > dfn[curNode]){
                    ans.push_back({curNode, child});
                }
            }else{
                low[curNode] = min(low[curNode], dfn[child]);
            }
        }
    }
public:
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        vector<vector<int>> ans;
        init(n, connections);
        tarjan(0, 0, ans);
        return ans;
    }
};
```

