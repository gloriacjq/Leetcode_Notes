# Palindrome Linked List

**Link: [Leetcode 234 - Easy](https://leetcode.com/problems/palindrome-linked-list/)**



## Desciption

Given the `head` of a singly linked list, return `true` if it is a palindrome.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false
```

 

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

 

**Follow up:** Could you do it in `O(n)` time and `O(1)` space?



## Solution

THANKS for reminder from dj, back to daily challenge again.

Find the middle of the list then reverse the later half.

P.S. Don't know why the runtime and memory usage are not very efficient, will figure it out on weekend.

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
    bool isPalindrome(ListNode* head) {        
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode *pre = nullptr;
        ListNode *cur = slow;
        ListNode *next = nullptr;
        while(cur){
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        
        ListNode *cur1 = head;
        ListNode *cur2 = pre;
        while(cur2){
            if(cur1->val != cur2->val)
                return false;
            cur1 = cur1->next;
            cur2 = cur2->next;
        }
        return true;
    }
    
    
};


// Runtime: 176 ms
// Memory Usage: 114.1 MB
```

