# Deepest Leaves Sum

**Link: [Leetcode 1302 - Medium](https://leetcode.com/problems/deepest-leaves-sum/)**



## Desciption

Given the `root` of a binary tree, return *the sum of values of its deepest leaves*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/07/31/1483_ex1.png)

```
Input: root = [1,2,3,4,5,null,6,7,null,null,null,null,8]
Output: 15
```

**Example 2:**

```
Input: root = [6,7,8,2,7,1,3,9,null,1,4,null,null,null,5]
Output: 19
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `1 <= Node.val <= 100`



## Solution

Record each level's sum. 

A dreamlike weekend, happy, comfortable. I feel much better after getting hugs from my friend. Just go ahead and get things done, fighting!

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
    map<int, int> m;
public:
    int deepestLeavesSum(TreeNode* root) {
        if(!root) return 0;
        int max_level = 0;
        dfs(root, 0, max_level);
        return m[max_level];   
    }
    
    void dfs(TreeNode* root, int level, int &max_level){
        if(!root) return;
        m[level] += root->val;
        max_level = max(level, max_level);
        dfs(root->left, level + 1, max_level);
        dfs(root->right, level + 1, max_level);
    }
};
```

Or you can just keep the sum of current maximun level.

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
    int sum = 0;
    int height = 0;
public:
    int deepestLeavesSum(TreeNode* root) {
        dfs(root, 0);
        return sum;   
    }
    
    void dfs(TreeNode* root, int level){
        if(!root) return;
        if(level > height){
            sum = 0;
            height = level;
        }
        if(level == height){
            sum += root->val;
        }
        dfs(root->left, level + 1);
        dfs(root->right, level + 1);
    }
};
```

