## 10.5 Sparse Search

Given a sorted array of strings that is interspersed with empty strings, write a method to find the location of a given string.

For example:

    Input: 
          ball,
          {"at", "", "", "", "ball", "", "", "car", "", "", "dad", "", ""},
    
    Output: 4
    
**Ideas:**

This problem is clearly gonna be solved by binary search. But we need to make some modification in order that binary search will be more efficient. Since:

First Thought:

midpoint can be empty, "", you can never choose left or right by making a comparison between "" and a string. Thus when making comparison with midpoint, we need to move it to the closest non-empty string.

How to move it to the closest non-empty string?
Probably we can use a pointer, every time it moves one step to left or right until it hits a non-empty string.

---

**Solution:**

    # Improved Binary Search:
    def bsearch(self, strings, l, h, target):
        if l > h:
            return -1
        mid = (l + h) / 2
        if strings[mid] == "":
            left, right = mid - 1, mid + 1
            while True:
            # means all strings in the list are empty.
                if left < l and right > h:
                    return -1
                elif right <= h and strings[right] != "":
                    mid = right
                    break
                elif left >= l and strings[left] != "":
                    mid = left
                    break
                left -= 1
                right += 1
        if target == strings[mid]:
            return mid
        # target is neither in the middle, nor on the left, search the right:
        elif strings[mid] < target:
            return self.bsearch(strings, mid+1, h, target)
        else:
            return self.bsearch(strings, l, mid-1, target)
            
    def search(self, strings, target):
        if len(strings) == 0 or len(target) == 0:
            return -1
        return self.bsearch(strings, 0, len(strings), target)
        
The worst-case runtime for this algorithm is O(n). In fact, it's impossible to have an algorithm for this problem that is better than O(n) in the worst case. After all, you could gave an array of all empty strings except for one non-empty string. There is no "smart" way to find this non-empty string. In the worst case, you will need to look at every element in the array.

Careful consideration should be given to this situation** when someone searches for the empty string**. Should we find the location (which is an O(n) operation)? Or should we handle this as an error?

There's no correct answer here. This is an issue you should raise with you interviewer. Simply asking this question will demonstrate that you are a careful coder.


