# Score of Parentheses

**Link: [Leetcode 856 - Medium](https://leetcode.com/problems/score-of-parentheses/)**



## Desciption

Given a balanced parentheses string `S`, compute the score of the string based on the following rule:

- `()` has score 1
- `AB` has score `A + B`, where A and B are balanced parentheses strings.
- `(A)` has score `2 * A`, where A is a balanced parentheses string.

 

**Example 1:**

```
Input: "()"
Output: 1
```

**Example 2:**

```
Input: "(())"
Output: 2
```

**Example 3:**

```
Input: "()()"
Output: 2
```

**Example 4:**

```
Input: "(()(()))"
Output: 6
```

 

**Note:**

1. `S` is a balanced parentheses string, containing only `(` and `)`.
2. `2 <= S.length <= 50`



## Solution

```c++
class Solution {
public:
    int scoreOfParentheses(string S) {
        int res = 0;
        stack<int> st;
        for (char c : S) {
            if (c == '(') {
                st.push(res);
                res = 0;
            } else {
                res = st.top() + max(res * 2, 1); 
                st.pop();
            }
        }
        return res;
    }
};
```

