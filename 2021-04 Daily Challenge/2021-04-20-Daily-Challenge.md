# N-ary Tree Preorder Traversal

**Link: [Leetcode 589 - Easy](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)**



## Desciption

Given the `root` of an n-ary tree, return *the preorder traversal of its nodes' values*.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
Input: root = [1,null,3,2,4,null,5,6]
Output: [1,3,5,6,2,4]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [1,2,3,6,7,11,14,4,8,12,5,9,13,10]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `0 <= Node.val <= 104`
- The height of the n-ary tree is less than or equal to `1000`.

 

**Follow up:** Recursive solution is trivial, could you do it iteratively?



## Solution

Recursive way.

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    vector<int> res;
    void helper(Node* root){
        if(!root) return;
        res.push_back(root->val);
        for(auto child : root->children){
            helper(child);
        }
    }
public:
    vector<int> preorder(Node* root) {
        helper(root);
        return res;
    }
};
```

Iterative way.

It seems that a multiway tree cannot be traversed using the Morris Traversal like what we did in a binary tree.

```c++
class Solution {
public:
    vector<int> preorder(Node* root) {
        vector<int> res;
        stack<Node*> st;
        if(!root) return res;
        st.push(root);
        while(!st.empty()){
            Node* tmp = st.top();
            st.pop();
            res.push_back(tmp->val);
            for(int i = tmp->children.size() - 1; i >= 0; i--){
                st.push(tmp->children[i]);
            }
        }
        return res;
    }
};
```

