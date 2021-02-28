# Maximum Frequency Stack

**Link: [Leetcode 895 - Hard](https://leetcode.com/problems/maximum-frequency-stack/)**



## Desciption

Design a stack-like data structure to push elements to the stack and pop the most frequent element from the stack.

Implement the `FreqStack` class:

- `FreqStack()` constructs an empty frequency stack.

- `void push(int val)` pushes an integer `val` onto the top of the stack.

- ```
  int pop()
  ```

   

  removes and returns the most frequent element in the stack.

  - If there is a tie for the most frequent element, the element closest to the stack's top is removed and returned.

 

**Example 1:**

```
Input
["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"]
[[], [5], [7], [5], [7], [4], [5], [], [], [], []]
Output
[null, null, null, null, null, null, null, 5, 7, 5, 4]

Explanation
FreqStack freqStack = new FreqStack();
freqStack.push(5); // The stack is [5]
freqStack.push(7); // The stack is [5,7]
freqStack.push(5); // The stack is [5,7,5]
freqStack.push(7); // The stack is [5,7,5,7]
freqStack.push(4); // The stack is [5,7,5,7,4]
freqStack.push(5); // The stack is [5,7,5,7,4,5]
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,5,7,4].
freqStack.pop();   // return 7, as 5 and 7 is the most frequent, but 7 is closest to the top. The stack becomes [5,7,5,4].
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,4].
freqStack.pop();   // return 4, as 4, 5 and 7 is the most frequent, but 4 is closest to the top. The stack becomes [5,7].
```

 

**Constraints:**

- `0 <= val <= 109`
- At most `2 * 104` calls will be made to `push` and `pop`.
- It is guaranteed that there will be at least one element in the stack before calling `pop`.



## Solution

map.

```c++
class FreqStack {
public:
    FreqStack() {
        
    }
    
    void push(int x) {
        freq[x] += 1;
        num[freq[x]].push_back(x);
        maxFreq = max(maxFreq, freq[x]);
    }
    
    int pop() {
        int val = num[maxFreq].back();
        num[maxFreq].pop_back();
        freq[val] -= 1;
        if(num[maxFreq].empty())
            maxFreq -= 1;
        return val;
    }
private:
    unordered_map<int, int> freq;
    unordered_map<int, vector<int> > num;
    int maxFreq = 0;
};

/**
 * Your FreqStack object will be instantiated and called as such:
 * FreqStack* obj = new FreqStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 */
```

multimap.

```c++
class FreqStack {
public:
    FreqStack() {
        
    }
    
    void push(int x) {
        freq[x] += 1;
        num.insert({freq[x], x});
    }
    
    int pop() {
        int val = num.begin()->second;
        num.erase(num.begin());
        freq[val] -= 1;
        return val;
    }
private:
    unordered_map<int, int> freq;
    multimap<int, int, greater_equal<int>> num;
};

/**
 * Your FreqStack object will be instantiated and called as such:
 * FreqStack* obj = new FreqStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 */
```

