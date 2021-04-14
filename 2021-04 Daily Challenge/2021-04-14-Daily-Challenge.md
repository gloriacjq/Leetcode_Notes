# Partition List

**Link: [Leetcode 86 - Medium](https://leetcode.com/problems/partition-list/)**



## Desciption

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

**Example 2:**

```
Input: head = [2,1], x = 2
Output: [1,2]
```

 

**Constraints:**

- The number of nodes in the list is in the range `[0, 200]`.
- `-100 <= Node.val <= 100`
- `-200 <= x <= 200`



## Solution

Find the first node greater than or equal to x, then go through the list, link the nodes less than x before that node.

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode *newHead = new ListNode(-201, head);
        ListNode *pre = newHead, *cur = head;
        while(pre->next && pre->next->val < x) pre = pre->next;
        cur = pre;
        while(cur->next){
            if(cur->next->val < x){
                ListNode *tmp = cur->next;
                cur->next = tmp->next;
                tmp->next = pre->next;
                pre->next = tmp;
                pre = pre->next;
            }else{
                cur = cur->next;
            }
        }
        return newHead->next;
        
    }
};

```

Or we can construct two lists called left and right, link the nodes separately acoording to their value, and link these two lists together.

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode* dummy1 = new ListNode(0);
        ListNode* dummy2 = new ListNode(0);
        ListNode* left = dummy1, *right = dummy2, *cur = head;
        while(cur){
            if(cur->val < x){
                left->next = cur;
                left = cur;
            }else{
                right->next = cur;
                right = cur;
            }
            cur = cur->next;
        }
        left->next = dummy2->next;
        right->next = nullptr;
        return dummy1->next;
    }
};
```



