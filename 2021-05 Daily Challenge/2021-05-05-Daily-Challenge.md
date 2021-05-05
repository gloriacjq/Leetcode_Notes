# Jump Game II

**Link: [Leetcode 45 - Hard](https://leetcode.com/problems/jump-game-ii/)**



## Desciption

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

 

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```
Input: nums = [2,3,0,1,4]
Output: 2
```

 

**Constraints:**

- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 105`



## Solution

Get the farthest index that each jump can reach. 

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int res = 0, cur = 0;
        int n = nums.size(), i = 0; 
        while(cur < n - 1){
            res++;
            int last = cur;
            for (; i <= last; i++) {
                cur = max(cur, i + nums[i]);
            }
        }
        return res;
    }
};

// Runtime: 4 ms, beats 47.54% of cpp submissions.
// Memory Usage: 7.9 MB, beats 96.45% of cpp submissions.
```

Another solution without `while`.

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int res = 0, cur = 0, last = 0;
        int n = nums.size();
        for(int i = 0; i < n - 1; i++){
            cur = max(cur, i + nums[i]);
            if(i == last){
                last = cur;
                res++;
                if(cur >= n - 1) break;
            }
        }
        return res;
    }
};

// Runtime: 0 ms, beats 100% of cpp submissions.
// Memory Usage: 8.2 MB, beats 45.31% of cpp submissions.
```

