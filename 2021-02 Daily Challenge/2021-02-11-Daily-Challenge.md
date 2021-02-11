# Valid Anagram

**Link: [Leetcode 242 - Easy](https://leetcode.com/problems/valid-anagram/)**



## Desciption

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?



## Solution

Easy one, happy to be with family today.

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()) return false;
        int cnt[26] = {0};
        for(char c : s){
            ++cnt[c - 'a'];
        }
        for(char c : t){
            if(--cnt[c - 'a'] < 0)
                return false;
        }
        return true;
    }
};
```

