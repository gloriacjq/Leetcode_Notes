#  Container With Most Water

**Link: [Leetcode 11 - Medium](https://leetcode.com/problems/container-with-most-water/)**



## Desciption

Given `n` non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` is at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

**Example 3:**

```
Input: height = [4,3,2,1,4]
Output: 16
```

**Example 4:**

```
Input: height = [1,2,1]
Output: 2
```

 

**Constraints:**

- `n == height.length`
- `2 <= n <= 3 * 104`
- `0 <= height[i] <= 3 * 104`



## Solution

**Hint**: Start with the maximum width container and go to a shorter width container if there is a vertical line longer than the current containers shorter line. This way we are compromising on the width but we are looking forward to a longer length container.

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int len = height.size();
        int left = 0, right = len - 1;
        int ans = (right - left) * min(height[left], height[right]);
        

        while(left < right){
            if(height[left] < height[right]){
                int tmp = height[left];
                while(left < right && height[left] <= tmp)
                    left++;
                ans = max(ans, (right - left) * min(height[left], height[right]));
            } else{
                int tmp = height[right];
                while(left < right && height[right] <= tmp)
                    right--;
                ans = max(ans, (right - left) * min(height[left], height[right]));
            }
        }
        return ans;
    }

};
```

