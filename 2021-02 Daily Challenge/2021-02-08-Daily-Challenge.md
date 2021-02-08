# Peeking Iterator

**Link: [Leetcode 284 - Medium](https://leetcode.com/problems/peeking-iterator/)**



## Desciption

Given an Iterator class interface with methods: `next()` and `hasNext()`, design and implement a PeekingIterator that support the `peek()` operation -- it essentially peek() at the element that will be returned by the next call to next().

**Example:**

```
Assume that the iterator is initialized to the beginning of the list: [1,2,3].

Call next() gets you 1, the first element in the list.
Now you call peek() and it returns 2, the next element. Calling next() after that still return 2. 
You call next() the final time and it returns 3, the last element. 
Calling hasNext() after that should return false.
```

**Follow up**: How would you extend your design to be generic and work with all types, not just integer?



**Hint**: For a clean implementation, check out [Google's guava library source code](https://github.com/google/guava/blob/703ef758b8621cfbab16814f01ddcc5324bdea33/guava-gwt/src-super/com/google/common/collect/super/com/google/common/collect/Iterators.java#L1125).



## Solution

Actually not very sure about the meaning of `without advancing the iterator` , the example from **Hint** is confusing.

Will review it later.

```c++
/*
 * Below is the interface for Iterator, which is already defined for you.
 * **DO NOT** modify the interface for Iterator.
 *
 *  class Iterator {
 *		struct Data;
 * 		Data* data;
 *		Iterator(const vector<int>& nums);
 * 		Iterator(const Iterator& iter);
 *
 * 		// Returns the next element in the iteration.
 *		int next();
 *
 *		// Returns true if the iteration has more elements.
 *		bool hasNext() const;
 *	};
 */

class PeekingIterator : public Iterator {
public:
	PeekingIterator(const vector<int>& nums) : Iterator(nums) {
	    // Initialize any member here.
	    // **DO NOT** save a copy of nums and manipulate it directly.
	    // You should only use the Iterator interface methods.
	    hasPeeked = false;
	}
	
    // Returns the next element in the iteration without advancing the iterator.
	int peek() {
        if(!hasPeeked){
            num = Iterator::next();
            hasPeeked = true;
        }
        return num;
	}
	
	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	int next() {
	    if(!hasPeeked){
            return Iterator::next();
        }
        int res = num;
        hasPeeked = false;
        return res;
	}
	
	bool hasNext() const {
	    return hasPeeked || Iterator::hasNext();
	}
    
private:
    bool hasPeeked;
    int num;
};
```

