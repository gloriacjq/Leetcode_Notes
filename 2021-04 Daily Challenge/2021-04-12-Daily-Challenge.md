# Beautiful Arrangement II

**Link: [Leetcode 667 - Medium](https://leetcode.com/problems/beautiful-arrangement-ii/)**



## Desciption

Given two integers `n` and `k`, you need to construct a list which contains `n` different positive integers ranging from `1` to `n` and obeys the following requirement:
Suppose this list is [a1, a2, a3, ... , an], then the list [|a1 - a2|, |a2 - a3|, |a3 - a4|, ... , |an-1 - an|] has exactly `k` distinct integers.

If there are multiple answers, print any of them.

**Example 1:**

```
Input: n = 3, k = 1
Output: [1, 2, 3]
Explanation: The [1, 2, 3] has three different positive integers ranging from 1 to 3, and the [1, 1] has exactly 1 distinct integer: 1.
```



**Example 2:**

```
Input: n = 3, k = 2
Output: [1, 3, 2]
Explanation: The [1, 3, 2] has three different positive integers ranging from 1 to 3, and the [2, 1] has exactly 2 distinct integers: 1 and 2.
```



**Note:**

1. The `n` and `k` are in the range 1 <= k < n <= 104.



## Solution

It's somehow like a puzzle game.

Take 1~7 as a example.

k = 6 : 7 - 1 - 6 - 2 - 5 - 3  | 4

k = 5 : 1 - 7 - 2 - 6 - 3  | 4  5

k = 4 : 7 - 1 - 6 - 2 | 3  4  5

k = 3 : 1 - 7 - 2 | 3  4  5  6

k = 2 : 7 - 1 | 2  3  4  5  6

Chose left or right as the start side according to K (odd or even).

Create the first K-1 nums of th array by inserting numbers from the left and right side in turn.

Insert the rest of the numbers by their original order.

```c++
class Solution {
public:
    vector<int> constructArray(int n, int k) {
        int l = 1, r = n;
        vector<int> res(n);
        for(int i = 0; i < n; i++){
            if(k > 1){
                res[i] = k%2 ? l++ : r--;
                k--;
            }else{
                res[i] = l++;
            }
        }
        return res;    
    }
};

// Runtime: 0 ms - beats 100.00 % of cpp submissions.
// Memory Usage: 7.3 MB - beats 97.48 % of cpp submissions.
```

