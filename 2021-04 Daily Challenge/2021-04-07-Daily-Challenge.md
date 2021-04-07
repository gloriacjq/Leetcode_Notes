# Determine if String Halves Are Alike

**Link: [Leetcode 1704 - Easy](https://leetcode.com/problems/determine-if-string-halves-are-alike/)**



## Desciption

You are given a string `s` of even length. Split this string into two halves of equal lengths, and let `a` be the first half and `b` be the second half.

Two strings are **alike** if they have the same number of vowels (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`, `'A'`, `'E'`, `'I'`, `'O'`, `'U'`). Notice that `s` contains uppercase and lowercase letters.

Return `true` *if* `a` *and* `b` *are **alike***. Otherwise, return `false`.

 

**Example 1:**

```
Input: s = "book"
Output: true
Explanation: a = "bo" and b = "ok". a has 1 vowel and b has 1 vowel. Therefore, they are alike.
```

**Example 2:**

```
Input: s = "textbook"
Output: false
Explanation: a = "text" and b = "book". a has 1 vowel whereas b has 2. Therefore, they are not alike.
Notice that the vowel o is counted twice.
```

**Example 3:**

```
Input: s = "MerryChristmas"
Output: false
```

**Example 4:**

```
Input: s = "AbCdEfGh"
Output: true
```

 

**Constraints:**

- `2 <= s.length <= 1000`
- `s.length` is even.
- `s` consists of **uppercase and lowercase** letters.



## Solution

Easy one. SAD RAINY DAY :-(

```c++
class Solution {
    unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
public:
    bool halvesAreAlike(string s) {
        int len = s.size();
        int lcnt = 0, rcnt = 0;
        for(int i = 0; i < len/2; i++){
            if(vowels.count(s[i])) lcnt++;
            if(vowels.count(s[i + len/2])) rcnt++;
        }
        return lcnt == rcnt;
    }
};
```

Also can only use one variable to control the result. 

``` C++
class Solution {
    unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
public:
    bool halvesAreAlike(string s) {
        int len = s.size();
        int res = 0;
        for(int i = 0, j = len / 2; j < len; i++, j++){
            if(vowels.count(s[i])) res++;
            if(vowels.count(s[j])) res--;
        }
        return !res;
    }
};
```

