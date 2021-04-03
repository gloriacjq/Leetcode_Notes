# Longest Valid Parentheses

**Link: [Leetcode 32 - Hard](https://leetcode.com/problems/longest-valid-parentheses/)**



## Desciption

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

 

**Example 1:**

```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```

**Example 2:**

```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```

**Example 3:**

```
Input: s = ""
Output: 0
```

 

**Constraints:**

- `0 <= s.length <= 3 * 104`
- `s[i]` is `'('`, or `')'`.



## Solution

Think carefully and use stack to solve it. (This problem seems not worth the Hard tag)

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        int left = 0, ans = 0;
        for(int i = 0; i < s.length(); i++){
            if(s[i] == '('){
                st.push(i);
            } else {
                if(st.empty()){
                    left = i + 1;
                }else{
                    st.pop();
                    ans = st.empty() ? max(ans, i - left + 1) : max(ans, i - st.top());
                }
            }  
        }
        return ans;
    }
};

// Runtime: 4 ms
// Memory Usage: 7.1 MB
```

After optimization (still track the left boundary, but the codes are more clear and elegant).

Official solution shows that this one gets a 0ms runtime, but I did't.

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        st.push(-1);
        int ans = 0;
        for(int i = 0; i < s.length(); i++){
            if(s[i] == '('){
                st.push(i);
            } else {
                st.pop();
                if(st.empty()){
                    st.push(i);
                }else{
                    ans = max(ans, i - st.top());
                }
            }  
        }
        return ans;
    }
};

// Runtime: 4 ms
// Memory Usage: 7.3 MB
```

Probably because there are less stack operations, time efficiency of this solution is great.

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        int cur = 0, ans = 0;
        for(char c : s){
           if(c == '('){
               st.push(cur);
               cur = 0;
           } else {
               if(st.empty()){
                   cur = 0;
               } else {
                   cur += st.top() + 2;
                   st.pop();
                   ans = max(ans, cur);
               }
           }
        }
        return ans;
    }
};

// Runtime: 0 ms
// Memory Usage: 7.2 MB
```

