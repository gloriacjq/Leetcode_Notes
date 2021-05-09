# Construct Target Array With Multiple Sums

**Link: [Leetcode 1354 - Hard](https://leetcode.com/problems/construct-target-array-with-multiple-sums/)**



## Desciption

Given an array of integers `target`. From a starting array, `A` consisting of all 1's, you may perform the following procedure :

- let `x` be the sum of all elements currently in your array.
- choose index `i`, such that `0 <= i < target.size` and set the value of `A` at index `i` to `x`.
- You may repeat this procedure as many times as needed.

Return True if it is possible to construct the `target` array from `A` otherwise return False.

 

**Example 1:**

```
Input: target = [9,3,5]
Output: true
Explanation: Start with [1, 1, 1] 
[1, 1, 1], sum = 3 choose index 1
[1, 3, 1], sum = 5 choose index 2
[1, 3, 5], sum = 9 choose index 0
[9, 3, 5] Done
```

**Example 2:**

```
Input: target = [1,1,1,2]
Output: false
Explanation: Impossible to create target array from [1,1,1,1].
```

**Example 3:**

```
Input: target = [8,5]
Output: true
```

 

**Constraints:**

- `N == target.length`
- `1 <= target.length <= 5 * 10^4`
- `1 <= target[i] <= 10^9`



## Solution

The use of variables is not very elegant, but it's time to sleep.

A key point is using mod operation in `max_num %= rest;` , think about it :

array {max, num_1, num_2, ... , num_n} can eventually get {max%rest, num_1, num_2, ...} by doing `max -= rest;` several times, so just simplify the process.

P.S. Pay attention to the situation where all the numbers in the target array are equal but not 1, like {3} or {2, 2}. 

```c++
class Solution {
public:
    bool isPossible(vector<int>& target) {
        priority_queue<int> q(target.begin(), target.end());
        long sum = 0, rest = 0;
        for(int num : target){
            sum += num;
        }
        while(true){
            long max_num = q.top();
            q.pop();
            rest = sum - max_num;
            sum -= max_num;
            if(max_num == 1 || rest == 1){
                return true;
            }else if(max_num < rest || rest == 0){
                return false;
            }else{
                max_num %= rest;
                if(max_num == 0) return false;
                q.emplace(max_num);
                sum += max_num;
            }
        }
    }
};

// Runtime: 32 ms, beats 92.73% of cpp submissions.
// Memory Usage: 28.5 MB, beats 84.24% of cpp submissions.
```

