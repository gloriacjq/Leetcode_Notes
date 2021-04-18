# Remove Nth Node From End of List

**Link: [Leetcode 19 - Medium](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)**



## Desciption

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Follow up:** Could you do this in one pass?

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```
Input: head = [1,2], n = 1
Output: [1]
```

 

**Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`



## Solution

Maintain two pointers and update one with a delay of n steps.

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *cur = head, *n_cur = head;
        while(n--){
            n_cur = n_cur->next;
        }
        if(!n_cur) return head->next;
        while(n_cur->next){
            cur = cur->next;
            n_cur = n_cur->next;
        }        
        cur->next = cur->next->next;
        return head;
    }
};
```

