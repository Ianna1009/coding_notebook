## Two-pointer Technique

There are two typical problems involving two-pointer technique:

**1. One slow-runner and the other fast runner**

     ``Example: Remove duplicates from a sorted array.``

**2. One pointer starts from the beginning while the other pointer starts from the end.** They move toward each other until they both meet.

      ``Example: Reverse the characters in a string ``
      
#### Example_1: Remove duplicates from a sorted array

Details see: [LeetCode 26. Remove Duplicates from Sorted Array](https://www.gitbook.com/book/ianna1009/leectcode-solution/edit#/edit/master/26.%20remove_duplicates_from_sorted_array.md) 

#### Example_2: Reverse the characters in a string

Suppose we've already had the ``swap`` function defined below in Python, note that in Python string is immutable (i.e. they can't be changed):

    def swap(str, i, j):
        str = list(str)
        tmp = str[i]
        str[i] = str[j]
        str[j] = tmp
        return "".join(str)
        
Then the idea to swap the first character with the end, advance to the next character and swapping repeatedly until it reaches the middle position. We calculated the middle position as ``[n/2]``. The middle position works for both odd and even size of array.

Basic algorithm:

    def reverse(str):
        n = len(str)
        for i in xrange(n/2):
        swap(str, i, j)
    
Or by two-pointer technique:

    def reverse(str):
        i = 0  # i points at beginning
        j = len(str) -1   # j points at ending
        while i<j:   # i, j can't meet each other
            swap(str, i, j)
            i += 1
            j -= 1
          
          
#### Example_3 Two_sum2 - input array is sorted

Details see: [LeetCode 167. Two Sum 2 - Input array is sorted](https://www.gitbook.com/book/ianna1009/leectcode-solution/edit#/edit/master/167.%20two_sum_2_-_input_array_is_sorted.md)

#### Example_4 Reverse Words in a String 2 (Similar to Example_2)

Details see: [LeetCode 186. Reverse Words in a String 2](https://www.gitbook.com/book/ianna1009/leectcode-solution/edit#/edit/master/186.%20reverse_words_in_a_string_2.md)

        
        