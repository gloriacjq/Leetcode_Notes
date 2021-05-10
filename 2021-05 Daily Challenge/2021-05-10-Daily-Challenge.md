# Count Primes

**Link: [Leetcode 204 - Easy](https://leetcode.com/problems/count-primes/)**



## Desciption

Count the number of prime numbers less than a non-negative number, `n`.

 

**Example 1:**

```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

**Example 2:**

```
Input: n = 0
Output: 0
```

**Example 3:**

```
Input: n = 1
Output: 0
```

 

**Constraints:**

- `0 <= n <= 5 * 106`



## Solution

Just follow the hints to use `The Sieve of Eratosthenes`. (actually hint 8 has already give us a quite detailed solution).

Seems it can be optimized, like we can only consider about odd numbers.

```c++
class Solution {
public:
    int countPrimes(int n) {
        bitset<5000005> bst;
        for(int i = 2; i < n; i++){
            bst.set(i);
        }
        int nSqrt = ceil(sqrt(n));
        for(int i = 2; i < nSqrt; i++){
            if(bst[i]){
                for(int j = i*i; j < n; j += i)
                    bst[j] = 0;
            }
        }
        return bst.count();
    }
};
```

