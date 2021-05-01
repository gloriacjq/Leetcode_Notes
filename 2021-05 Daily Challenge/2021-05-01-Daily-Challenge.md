# Prefix and Suffix Search

**Link: [Leetcode 745 - Hard](https://leetcode.com/problems/prefix-and-suffix-search/)**



## Desciption

Design a special dictionary which has some words and allows you to search the words in it by a prefix and a suffix.

Implement the `WordFilter` class:

- `WordFilter(string[] words)` Initializes the object with the `words` in the dictionary.
- `f(string prefix, string suffix)` Returns *the index of the word in the dictionary* which has the prefix `prefix` and the suffix `suffix`. If there is more than one valid index, return **the largest** of them. If there is no such word in the dictionary, return `-1`.

 

**Example 1:**

```
Input
["WordFilter", "f"]
[[["apple"]], ["a", "e"]]
Output
[null, 0]

Explanation
WordFilter wordFilter = new WordFilter(["apple"]);
wordFilter.f("a", "e"); // return 0, because the word at index 0 has prefix = "a" and suffix = 'e".
```

 

**Constraints:**

- `1 <= words.length <= 15000`
- `1 <= words[i].length <= 10`
- `1 <= prefix.length, suffix.length <= 10`
- `words[i]`, `prefix` and `suffix` consist of lower-case English letters only.
- At most `15000` calls will be made to the function `f`.



**Hint:**

* For a word like "test", consider "#test", "t#test", "st#test", "est#test", "test#test". Then if we have a query like prefix = "te", suffix = "t", we can find it by searching for something we've inserted starting with "t#te".



## Solution

The initialization seems toooo time and space consuming, but I have no idea how to optimize it.

```c++
class WordFilter {
    unordered_map<string, int> idx;
public:
    WordFilter(vector<string>& words) {
        for(int k = 0; k < words.size(); k++){
            for(int i = 1; i <= words[k].size(); i++){
                for(int j = 0; j < words[k].size(); j++){
                    idx[words[k].substr(0, i) + "#" + words[k].substr(j)] = k;
                }
            }
        }
    }
    
    int f(string prefix, string suffix) {
        return idx.count(prefix + "#" + suffix) ? idx[prefix + "#" + suffix] : -1;
    }
};

/**
 * Your WordFilter object will be instantiated and called as such:
 * WordFilter* obj = new WordFilter(words);
 * int param_1 = obj->f(prefix,suffix);
 */
```

This one is even worse.

```c++
class WordFilter {
    unordered_map<string, vector<int>> pre, suf;
public:
    WordFilter(vector<string>& words) {
        for (int k = 0; k < words.size(); ++k) {
            for (int i = 0; i <= words[k].size(); ++i) {
                pre[words[k].substr(0, i)].push_back(k);
                suf[words[k].substr(i)].push_back(k);
            }
        }
    }
    
    int f(string prefix, string suffix) {
        if (!pre.count(prefix) || !suf.count(suffix)) return -1;
        vector<int> preIdx = pre[prefix], sufIdx = suf[suffix];
        int i = preIdx.size() - 1, j = sufIdx.size() - 1;
        while (i >= 0 && j >= 0) {
            if (preIdx[i] < sufIdx[j]) j--;
            else if (preIdx[i] > sufIdx[j]) i--;
            else return preIdx[i];
        }
        return -1;
    }
};

/**
 * Your WordFilter object will be instantiated and called as such:
 * WordFilter* obj = new WordFilter(words);
 * int param_1 = obj->f(prefix,suffix);
 */
```

Maybe I'll try Trie Tree later.