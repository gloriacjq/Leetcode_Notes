# Binary Tree Right Side View

**Link: [Leetcode 199 - Medium](https://leetcode.com/problems/binary-tree-right-side-view/)**



## Desciption

Given a binary tree, imagine yourself standing on the *right* side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```



## Solution

Here are two solutions.

A bfs one, typical level traversal.

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
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            res.push_back(q.back()->val);
            int size = q.size();
            for(int i = 0; i < size; i++){
                TreeNode *node = q.front();
                q.pop();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
        }
        return res;
    }
};
```

A dfs one that tracking the layer, worse time efficiency but better space efficiency.

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
    vector<int> res;
    int curHeight = 0;
    void dfs(TreeNode* node, int height){
        if(!node) return;
        if(height > curHeight){
            res.push_back(node->val);
            curHeight++;
        }
        dfs(node->right, height + 1);
        dfs(node->left, height + 1);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        dfs(root, 1);
        return res;
    }
};
```

