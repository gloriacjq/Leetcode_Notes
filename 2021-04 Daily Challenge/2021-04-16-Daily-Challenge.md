# Remove All Adjacent Duplicates in String II

**Link: [Leetcode 1209 - Medium](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)**



## Desciption

Given a string `s`, a *k* *duplicate removal* consists of choosing `k` adjacent and equal letters from `s` and removing them causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make `k` duplicate removals on `s` until we no longer can.

Return the final string after all such duplicate removals have been made.

It is guaranteed that the answer is unique.

 

**Example 1:**

```
Input: s = "abcd", k = 2
Output: "abcd"
Explanation: There's nothing to delete.
```

**Example 2:**

```
Input: s = "deeedbbcccbdaa", k = 3
Output: "aa"
Explanation: 
First delete "eee" and "ccc", get "ddbbbdaa"
Then delete "bbb", get "dddaa"
Finally delete "ddd", get "aa"
```

**Example 3:**

```
Input: s = "pbbcggttciiippooaais", k = 2
Output: "ps"
```

 

**Constraints:**

- `1 <= s.length <= 10^5`
- `2 <= k <= 10^4`
- `s` only contains lower case English letters.



## Solution

Use vector as stack (Doing this way rather than using the original stack will make it more convenient to construct the result string after making k-duplicate removals)

```c++
class Solution {
public:
    string removeDuplicates(string s, int k) {
        vector<pair<char, int> > st;
        string res;
        for(auto c : s){
            if(st.empty() || st.back().first != c){
                st.push_back(make_pair(c, 1));
            }else{
                st.back().second += 1;
                if(st.back().second == k) st.pop_back();
            }
        }
        for(auto p : st){
            res += string(p.second, p.first);
        }
        return res;
    }
};

// Runtime: 8 ms, beats 91.41% of cpp submission.
// Memory Usage: 8.2 MB, beats 46.26% of cpp submission.
```



Here's another problem which is similar to the problem above.



# Remove All Adjacent Duplicates in String

**Link: [Leetcode 1047 - Easy](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)**



## Desciption

Given a string `S` of lowercase letters, a *duplicate removal* consists of choosing two adjacent and equal letters, and removing them.

We repeatedly make duplicate removals on S until we no longer can.

Return the final string after all such duplicate removals have been made. It is guaranteed the answer is unique.

 

**Example 1:**

```
Input: "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```

 

**Note:**

1. `1 <= S.length <= 20000`
2. `S` consists only of English lowercase letters.



## Solution

stack.

```c++
class Solution {
public:
    string removeDuplicates(string S) {
        stack<char> st;
        string res;
        for(auto c : S){
            if(st.empty() || st.top() != c){
                st.push(c);
            }else{
                st.pop();
            }
        }
        int n = st.size();
        res.resize(n);
        for(int i = n - 1; i >= 0; i--){
            res[i] = st.top();
            st.pop();
        }
        return res;
    }
};

// Runtime: 24 ms
// Memory Usage: 10.2 MB
```

vector.

```c++
class Solution {
public:
    string removeDuplicates(string S) {
        vector<char> v;
        for(auto c : S){
            if(v.empty() || v.back() != c){
                v.push_back(c);
            } else {
                v.pop_back();
            }
        }
        string ans(v.begin(),v.end());
        return ans;
    }
};

// Runtime: 12 ms, beats 96.05% of cpp submission.
// Memory Usage: 10.8 MB, beats 26.68% of cpp submission.
```

directly operate on string.

```c++
class Solution {
public:
    string removeDuplicates(string S) {
        string res;
        for(char c : S){
            if(res.size() > 0 && res[res.size()-1]==c) {
                res.pop_back();
            }else{
                res.push_back(c);  
            }
        }
        return res;
    }
};

// Runtime: 8 ms, faster than 99.57% of C++ online submissions.
// Memory Usage: 10 MB, less than 84.21% of C++ online submissions.
```







