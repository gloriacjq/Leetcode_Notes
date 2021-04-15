# Fibonacci Number

**Link: [Leetcode 509 - Easy](https://leetcode.com/problems/fibonacci-number/)**



## Desciption

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

Given `n`, calculate `F(n)`.

 

**Example 1:**

```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**Example 2:**

```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**Example 3:**

```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

 

**Constraints:**

- `0 <= n <= 30`



## Solution

Recursion.

```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        return fib(n-1) + fib(n-2);    
    }
};
```

Iteration.

```c++
class Solution { 
public:
    int fib(int n) {
        int a = 0, b = 1;
        for(int i = 0; i < n; i++){
            int c = a + b;
            a = b;
            b = c;
        }
        return a;
    }
};
```

Divide and conquer. Thank dj for telling me the existence of Binary Exponentiation which can also be used in matrix multiplication.

```c++
class Solution {
    struct Matrix{
        int val[2][2];
    };
    
    Matrix base = {
        .val = {{1, 1}, {1, 0}}
    };
    
    Matrix multiply(Matrix a, Matrix b, int n){
        Matrix res;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                res.val[i][j] = 0;
            }
        }        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                for(int k = 0; k < n; k++){
                    res.val[i][j] += a.val[i][k] * b.val[k][j];
                }
            }
        }
        return res;
    }
    Matrix quickPower(Matrix m, int N){
        Matrix ans = {
            .val = {{1, 0}, {0, 1}}
        };
        while(N){
            if(N & 1){
                ans = multiply(ans, m, 2);
            }
            m = multiply(m, m, 2);
            N >>= 1;
        }
        return ans;
    }
    
public:
    int fib(int n) {
        Matrix res = {
            .val = {{1, 0}, {0, 0}}
        };
        res = multiply(res, quickPower(base, n), 2);
        return res.val[0][1];
    }
};
```

