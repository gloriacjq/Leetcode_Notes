# Binary Tree Cameras

**Link: [Leetcode 968 - Hard](https://leetcode.com/problems/binary-tree-cameras/)**



## Desciption

Given a binary tree, we install cameras on the nodes of the tree. 

Each camera at a node can monitor **its parent, itself, and its immediate children**.

Calculate the minimum number of cameras needed to monitor all nodes of the tree.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_01.png)

```
Input: [0,0,null,0,0]
Output: 1
Explanation: One camera is enough to monitor all nodes if placed as shown.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_02.png)

```
Input: [0,0,null,0,null,0,null,null,0]
Output: 2
Explanation: At least two cameras are needed to monitor all nodes of the tree. The above image shows one of the valid configurations of camera placement.
```


**Note:**

1. The number of nodes in the given tree will be in the range `[1, 1000]`.
2. **Every** node has value 0.





## Solution

Use 0,1,2 to represent different states, detailed notes are in the code comment.

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    /* 0 -- leaf node, monitored by its parent,
       1 -- leaf's parent(as long as one of the children is leaf), monitored by itself,
       2 -- leaf's grandparent, monitored by its children */
    int dfs(TreeNode* root, int& sum) {
        if(!root) return 2;
        int l = dfs(root->left, sum), r = dfs(root->right, sum);
        if (l == 0 || r == 0) {
            sum++;
            return 1;
        } else if (l == 1 || r == 1) {
            return 2;
        } else {
            return 0;
        }
    }
public:
    int minCameraCover(TreeNode* root) {
        int sum = 0;
        sum += dfs(root, sum)==0 ;
        return sum;
    }
};
```

