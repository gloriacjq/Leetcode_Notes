# Shortest Distance to a Character

**Link: [Leetcode 821 - Easy](https://leetcode.com/problems/shortest-distance-to-a-character/)**



## Desciption

Given a string `s` and a character `c` that occurs in `s`, return *an array of integers `answer` where* `answer.length == s.length` *and* `answer[i]` *is the shortest distance from* `s[i]` *to the character* `c` *in* `s`.

 

**Example 1:**

```
Input: s = "loveleetcode", c = "e"
Output: [3,2,1,0,1,0,0,1,2,2,1,0]
```

**Example 2:**

```
Input: s = "aaab", c = "b"
Output: [3,2,1,0]
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s[i]` and `c` are lowercase English letters.
- `c` occurs at least once in `s`.



## Solution

Update the result by sequential and reverse traversal.

```c++
class Solution {
public:
    vector<int> shortestToChar(string s, char c) {
        int n = s.size();
        vector<int> res(n, n);
        res[0] = s[0] == c ? 0 : n;
        for(int i = 1; i < n; i++){
            res[i] = s[i] == c ? 0 : (res[i-1] + 1);
        }
        for(int j = n-2; j >= 0; j--){
            res[j] = min(res[j], res[j+1] + 1);
        }
        return res;
    }
};
```
