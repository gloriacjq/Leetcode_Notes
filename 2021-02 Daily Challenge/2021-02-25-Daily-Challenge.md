# Shortest Unsorted Continuous Subarray

**Link: [Leetcode 581 - Medium](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)**



## Desciption

Given an integer array `nums`, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return *the shortest such subarray and output its length*.

 

**Example 1:**

```
Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: 0
```

**Example 3:**

```
Input: nums = [1]
Output: 0
```

 

**Constraints:**

- `1 <= nums.length <= 104`
- `-105 <= nums[i] <= 105`

 

**Follow up:** Can you solve it in `O(n)` time complexity?



## Solution

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n = nums.size();
        int maxNum = nums[0], minNum = nums[n-1];
        int start = -1, end = -2;
        for(int i = 0; i < n; i++){
            if(nums[i] < maxNum){
                end = i;
            }else{
                maxNum = nums[i];
            }
            
            if(nums[n-i-1] > minNum){
                start = n - i - 1;
            }else{
                minNum = nums[n-i-1];
            }
        }
        return end - start + 1;
    }
};
```

