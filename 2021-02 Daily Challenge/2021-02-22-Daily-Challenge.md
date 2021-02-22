# Longest Word in Dictionary through Deleting

**Link: [Leetcode 524 - Medium](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/)**



## Desciption

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```



**Example 2:**

```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```



**Note:**

1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.



## Solution

Check each word and update the longest result.

```c++
class Solution {
public:
    string findLongestWord(string s, vector<string>& d) {
        string res = "";
        int len = 0;
        for (string str : d) {
            int i = 0, strLen = str.size();
            for (char c : s) {
                if (i < str.size() && c == str[i]) i++;
            }
            if (i == strLen && strLen >= len) {
                if (strLen > len || str < res) {
                    res = str;
                    len = strLen;
                }
            }
        }
        return res;
    }
};
```

