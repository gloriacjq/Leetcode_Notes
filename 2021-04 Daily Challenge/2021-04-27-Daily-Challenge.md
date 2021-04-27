# Power of Three

**Link: [Leetcode 326 - Easy](https://leetcode.com/problems/power-of-three/)**



## Desciption

Given an integer `n`, return *`true` if it is a power of three. Otherwise, return `false`*.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.

 

**Example 1:**

```
Input: n = 27
Output: true
```

**Example 2:**

```
Input: n = 0
Output: false
```

**Example 3:**

```
Input: n = 9
Output: true
```

**Example 4:**

```
Input: n = 45
Output: false
```

 

**Constraints:**

- `-231 <= n <= 231 - 1`

 

**Follow up:** Could you solve it without loops/recursion?



## Solution

Iterative way:

```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        while(n && n % 3 == 0){
            n /= 3;
        }
        return n == 1;
    }
};
```

The biggest qualified number in the constraint is 1162261467.

```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        return n > 0 && 1162261467 % n == 0;
    }
};
```

Another solution I saw from the Internet, according to the formula `log3(n) = log10(n) / log10(3)`. Clever one.

```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        return n > 0 && int(log10(n) / log10(3)) - log10(n) / log10(3) == 0;
    }
};
```

