## 10.4 Sorted Search, No sizes


You are given an array-like data structure `Listy` which lacks a size method. It does, however, have an `elemnetAt(i)` method that returns the element at index i in O(1) time. If i is beyond the bounds of the data structures, it returns -1. (For this reason, the data structure onlu supports positive integers.) 

Given a Listy which contains sorted, positive integers, find the index at which an element x occurs. If x occurs multiple times, you may return any index.

Follow up from [here](http://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/): Find position of an element in a sorted array of **infinite numbers**.

**Idea:**

Since this Listy is sorted, Binary Search will be come up with. The problem is that binary search requires us knowing the length of the list, so that we compare it to the midpoint. We don't have it here.

Compute the length first! Yes!

We know that elementAt will return -1 when i is too large. We can therefore just try bigger and bigger values until we exceed the size of the list.

But how much bigger? If we just went through the list through the list linearly -- 1, then 2, then 3, then 4, and so on -- we'd wind up with a linear time algorithm. We probably want something faster than this. Otherwise, why would the interviewer have specified the list is sorted?

It's better to back off exponentially. Try 1, then 2, then 4, then 8, then 16, and so on. This ensures that, if the list has length n, we'll find the length in at most O(lgn) time.

---
**Solution:**

    def bsearch(self, nums, taget, l, h):
        while l <= h:
            mid = (l + h) / 2
            middle = nums.elementAt(mid)
            if middle > target or middle == -1:
                h = mid - 1
            elif middle < target:
                l = mid + 1
            else:
                return mid
        return -1
        
        
    def serach(self, nums, target):
        i = 1
        while nums.elementAt(i) != -1 and nums.elementAt(i) < target:
            i *= 2
        return self.bsearch(nums, target, i/2, i)
        
It turns out that not knowing the length didn't impact the runtime of the search algorithm. We find the length in O(lgn) time and then do the search in **O(lgn) time**. Our overall runtime is O(lgn), just as it would be a normal array.

---
**Follow-up:**

Suppose you have a sorted array of infinite numbers, how would you search an element in the array?

    # Python Program to demonstrate working of an algorithm that finds
    # an element in an array of infinite size

    # Binary search algorithm implementation
    def binary_search(arr,l,r,x):

        if r >= l:
            mid = l+(r-l)/2

            if arr[mid] == x:
                return mid

            if arr[mid] > x:
                return binary_search(arr,l,mid-1,x)

            return binary_search(arr,mid+1,r,x)

        return -1

    # function takes an infinite size array and a key to be
    # searched and returns its position if found else -1.
    # We don't know size of a[] and we can assume size to be
    # infinite in this function.
    # NOTE THAT THIS FUNCTION ASSUMES a[] TO BE OF INFINITE SIZE
    # THEREFORE, THERE IS NO INDEX OUT OF BOUND CHECKING
    def findPos(a, key):

        l, h, val = 0, 1, arr[0]

        # Find h to do binary search
        while val < key:
            l = h            #store previous high
            h = 2*h          #double high index
            val = arr[h]       #update new val

        # at this point we have updated low and high indices,
        # thus use binary search between them
        return binary_search(a, l, h, key)
        
