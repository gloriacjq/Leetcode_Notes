# Furthest Building You Can Reach

**Link: [Leetcode 1642 - Medium]()**



## Desciption

You are given an integer array `heights` representing the heights of buildings, some `bricks`, and some `ladders`.

You start your journey from building `0` and move to the next building by possibly using bricks or ladders.

While moving from building `i` to building `i+1` (**0-indexed**),

- If the current building's height is **greater than or equal** to the next building's height, you do **not** need a ladder or bricks.
- If the current building's height is **less than** the next building's height, you can either use **one ladder** or `(h[i+1] - h[i])` **bricks**.

*Return the furthest building index (0-indexed) you can reach if you use the given ladders and bricks optimally.*

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/27/q4.gif)

```
Input: heights = [4,2,7,6,9,14,12], bricks = 5, ladders = 1
Output: 4
Explanation: Starting at building 0, you can follow these steps:
- Go to building 1 without using ladders nor bricks since 4 >= 2.
- Go to building 2 using 5 bricks. You must use either bricks or ladders because 2 < 7.
- Go to building 3 without using ladders nor bricks since 7 >= 6.
- Go to building 4 using your only ladder. You must use either bricks or ladders because 6 < 9.
It is impossible to go beyond building 4 because you do not have any more bricks or ladders.
```

**Example 2:**

```
Input: heights = [4,12,2,7,3,18,20,3,19], bricks = 10, ladders = 2
Output: 7
```

**Example 3:**

```
Input: heights = [14,3,19,3], bricks = 17, ladders = 0
Output: 3
```

 

**Constraints:**

- `1 <= heights.length <= 105`

- `1 <= heights[i] <= 106`

- `0 <= bricks <= 109`

- `0 <= ladders <= heights.length`You are given an integer array `heights` representing the heights of buildings, some `bricks`, and some `ladders`.

  You start your journey from building `0` and move to the next building by possibly using bricks or ladders.

  While moving from building `i` to building `i+1` (**0-indexed**),

  - If the current building's height is **greater than or equal** to the next building's height, you do **not** need a ladder or bricks.
  - If the current building's height is **less than** the next building's height, you can either use **one ladder** or `(h[i+1] - h[i])` **bricks**.

  *Return the furthest building index (0-indexed) you can reach if you use the given ladders and bricks optimally.*

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2020/10/27/q4.gif)

  ```
  Input: heights = [4,2,7,6,9,14,12], bricks = 5, ladders = 1
  Output: 4
  Explanation: Starting at building 0, you can follow these steps:
  - Go to building 1 without using ladders nor bricks since 4 >= 2.
  - Go to building 2 using 5 bricks. You must use either bricks or ladders because 2 < 7.
  - Go to building 3 without using ladders nor bricks since 7 >= 6.
  - Go to building 4 using your only ladder. You must use either bricks or ladders because 6 < 9.
  It is impossible to go beyond building 4 because you do not have any more bricks or ladders.
  ```

  **Example 2:**

  ```
  Input: heights = [4,12,2,7,3,18,20,3,19], bricks = 10, ladders = 2
  Output: 7
  ```

  **Example 3:**

  ```
  Input: heights = [14,3,19,3], bricks = 17, ladders = 0
  Output: 3
  ```

   

  **Constraints:**

  - `1 <= heights.length <= 105`
  
  - `1 <= heights[i] <= 106`
  
- `0 <= bricks <= 109`
  
  - `0 <= ladders <= heights.length`
  
    
  
  **Hint:**
  
  -  Assume the problem is to check whether you can reach the last building or not.
  - You'll have to do a set of jumps, and choose for each one whether to do it using a rope or bricks. It's always optimal to use ropes in the largest jumps.
  - Iterate on the buildings, maintaining the largest r jumps and the sum of the remaining ones so far, and stop whenever this sum exceeds b.



## Solution

Use priority_queue to maintain the largest r jumps (ladders will be used on them).

```c++
class Solution {
public:
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        priority_queue<int, vector<int>, greater<int> > q;
        int leftBricks = bricks;
        for(int i = 1; i < heights.size(); i++){
            int h = heights[i] - heights[i-1];
            if(h > 0){
                q.push(h);
                if(q.size() > ladders){
                    leftBricks -= q.top();
                    q.pop();
                }
                if(leftBricks < 0) return i-1;
            }
        }
        return heights.size() - 1;
    }
};

// Runtime: 104 ms
// Memory Usage: 53.6 MB
```

After optimization, this one uses less push operations.

```c++
class Solution {
public:
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        priority_queue<int, vector<int>, greater<int> > q;
        int i;
        for(i = 0; i < heights.size() - 1; i++){
            int diff = heights[i+1] - heights[i];
            if(diff <= 0) continue;
            if(q.size() < ladders){
                q.push(diff);
            }else{
                if(!q.empty() && diff > q.top()){
                    q.push(diff);
                    diff = q.top();
                    q.pop();
                }              
                if(bricks < diff) break;
                bricks -= diff;
            }
        }
        return i;
    }
};

// Runtime: 96 ms, beats 70.40% of cpp submissions
// Memory Usage: 53.5 MB, beats 95.50% of cpp submissions
```

